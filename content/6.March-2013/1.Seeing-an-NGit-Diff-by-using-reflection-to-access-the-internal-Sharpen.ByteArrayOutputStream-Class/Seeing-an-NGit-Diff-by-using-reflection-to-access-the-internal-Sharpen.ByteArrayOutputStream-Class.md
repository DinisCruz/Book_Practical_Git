## Seeing an NGit Diff by using reflection to access the internal Sharpen.ByteArrayOutputStream Class

I was trying to get the NGif diff output stream, but hit on an issue that the **_Sharpen.ByteArrayOutputStream_** class is internal

Here is an example from NGit UnitTests on how to use the NGI Diff Command:

![](images/seeing-ngit-diff-1.png)

The key part is:

![](images/image_thumb_25255B1_25255D.png)

Note how the **_Sharpen.ByteArrayOutputStream_** was created and used on** _Diff.SetOutputStream_, but (as we will see below), we will have a problem because this class is **_internal_**:

![](images/image_thumb_25255B3_25255D.png)

On an [O2 Platform](http://blog.diniscruz.com/p/owasp-o2-platform.html) [C# REPL script](http://blog.diniscruz.com/p/c-repl-script-environment.html), lets create a quick repo and a valid Diff result:

![](images/image_thumb_25255B8_25255D.png)

Our objective is to get the Diff formatted output shown in the NGit Unit test.

A quick look at the Diff class, shows no public fields, properties or methods that expose it:

![](images/seeing-ngit-diff-2.png)

And by default the **_out_** field is null:

![](images/seeing-ngit-diff-3.png)

Basically what we need to do is this:

![](images/seeing-ngit-diff-4.png)

But as you can see, we can't create an instance of the **_Sharpen.ByteArrayOutputStream_**  

Well, we can't create it directly, but we can easily create it using reflection :)

To do that, lets start by getting an reference to the **_Sharpen.dll_** assembly

![](images/seeing-ngit-diff-5.png)

then add a reference to the **_ByteArrayOutputStream_**  type

![](images/seeing-ngit-diff-6.png)

invoke its constructor to create a live instance of it:

![](images/seeing-ngit-diff-7.png)

since the Sharpen.OutputStream class is public, we can cast our **_ByteArrayOutputStream_**  object into it:

![](images/seeing-ngit-diff-8.png)

we then assign it to the NGit command, which will give us the diff log we wanted

![](images/seeing-ngit-diff-9.png)

Note that the out field is now not null:

![](images/seeing-ngit-diff-10.png)

Here is the Source code of the C# code snippet created:  

{lang="csharp"}    
    var outputStream = "Sharpen.dll".assembly()  
                                    .type("ByteArrayOutputStream")  
                                    .ctor()  
                                    .cast<OutputStream>();


    var tempRepo = "tempRepo".tempDir();  
    var nGit = tempRepo.git_Init();

    var file = "testFile.txt";  
    nGit.writeFile (file, "some content\naaaa\n");  
    nGit.add (".",false).commit_using_Status();  
    nGit.writeFile (file, "some content\naa Change\n");

    var diff = nGit.Git.Diff();

    diff.SetOutputStream(outputStream).Call();  
    return outputStream.str();

    //using Sharpen  
    //O2Ref:FluentSharp.NGit.DLL  
    //O2Ref:NGit.dll  
    //O2Ref:Sharpen.dll  
