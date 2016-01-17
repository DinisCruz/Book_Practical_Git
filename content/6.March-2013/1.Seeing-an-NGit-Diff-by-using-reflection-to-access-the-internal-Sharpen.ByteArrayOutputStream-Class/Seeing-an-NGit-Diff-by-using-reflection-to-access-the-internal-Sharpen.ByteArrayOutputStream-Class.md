## Seeing an NGit Diff by using reflection to access the internal Sharpen.ByteArrayOutputStream Class

I was trying to get the NGif diff output stream, but hit on an issue that the **_Sharpen.ByteArrayOutputStream_** class is internal

  
Here is an example from NGit UnitTests on how to use the NGI Diff Command:

[![image](images/image_thumb.png)](http://lh4.ggpht.com/-Hnga22TKBlQ/USIqZ41qnRI/AAAAAAAAJto/ZMk7BFIUI8M/s1600-h/image%25255B2%25255D.png)

The key part is:

[![image](images/image_thumb_25255B1_25255D.png)](http://lh6.ggpht.com/-JHV2TCPzDus/USIquXaSvNI/AAAAAAAAJt4/yqyfGSYUSyw/s1600-h/image%25255B5%25255D.png)

Note how the **_Sharpen.ByteArrayOutputStream_** was created and used on** _Diff.SetOutputStream , _**but (as we will see below), we will have a problem because  this class is **_internal_**:

[![image](images/image_thumb_25255B3_25255D.png)](http://lh4.ggpht.com/-Nykw1k_3YrM/USIq6Rw0bEI/AAAAAAAAJuI/fRhVfV4azrI/s1600-h/image%25255B9%25255D.png)

On an [O2 Platform](http://blog.diniscruz.com/p/owasp-o2-platform.html) [C# REPL script](http://blog.diniscruz.com/p/c-repl-script-environment.html), lets create a quick repo and a valid Diff result:

[![image](images/image_thumb_25255B8_25255D.png)](http://lh5.ggpht.com/-IubxNVI0yrQ/USIrJEoS_-I/AAAAAAAAJuY/3fXu0wvd4p0/s1600-h/image%25255B20%25255D.png)

Our objective is to get the Diff formatted output shown in the NGit Unit test.

A quick look at the Diff class, shows no public fields, properties or methods that expose it:

[![image](images/image_thumb_25255B10_25255D1.png)](http://lh3.ggpht.com/-GNs9xEIVvS8/USIrYpsy_JI/AAAAAAAAJuo/0AiePTu_DD4/s1600-h/image%25255B24%25255D.png)

And by default the **_out _**field is null:

[![image](images/image_thumb_25255B11_25255D1.png)](http://lh6.ggpht.com/-bjg0QhjvdzU/USIsbxJ8PaI/AAAAAAAAJu4/xhT6pMeozag/s1600-h/image%25255B27%25255D.png)

Basically what we need to do is this:

[![image](images/image_thumb_25255B12_25255D1.png)](http://lh3.ggpht.com/-sBiTLxpIlIk/USIsn8EllmI/AAAAAAAAJvI/J5B8TUy-r9Q/s1600-h/image%25255B30%25255D.png)

But as you can see, we can't create an instance of the **_Sharpen.ByteArrayOutputStream _**  
**_  
_**Well, we can't create it directly, but we can easily create it using reflection :)

To do that, lets start by getting an reference to the **_Sharpen.dll _**assembly

[![image](images/image_thumb_25255B13_25255D1.png)](http://lh3.ggpht.com/-iPq46qYuthQ/USIs2V9bJoI/AAAAAAAAJvY/uvIuScqzCcw/s1600-h/image%25255B33%25255D.png)

then add a reference to the **_ByteArrayOutputStream_**  type

[![image](images/image_thumb_25255B15_25255D1.png)](http://lh3.ggpht.com/-o8cPydhiGx8/USIwb4P5TgI/AAAAAAAAJxw/Twz0d_gdsv8/s1600-h/image%25255B39%25255D.png)

invoke its constructor to create a live instance of it:

[![image](images/image_thumb_25255B16_25255D1.png)](http://lh4.ggpht.com/-fRdY6U5Pats/USIw3s43qiI/AAAAAAAAJz8/QkdtI2X8gaQ/s1600-h/image%25255B42%25255D.png)

since the Sharpen.OutputStream class is public, we can cast our **_ByteArrayOutputStream_**  object into it:

[![image](images/image_thumb_25255B17_25255D.png)](http://lh5.ggpht.com/-wXuQn8bC5bk/USIxNDwKokI/AAAAAAAAJ0M/OInnyB1FaSo/s1600-h/image%25255B45%25255D.png)

we then assign it to the NGit command, which will give us the diff log we wanted

![image](images/image_thumb_25255B18_25255D1.png)

Note that the out field is now not null:

[![image](images/image_thumb_25255B19_25255D.png)](http://lh5.ggpht.com/-PyS96CKXwq4/USIybbAdJhI/AAAAAAAAJ0k/kpXyVw8iSc4/s1600-h/image%25255B51%25255D.png)

Here is the Source code of the C# code snippet created:  

    
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

