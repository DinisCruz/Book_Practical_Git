## Extracting content files from a Azure deployed version of TeamMentor (pre 3.3 git support)

I was asked by Serge to retrieve some changes he made to a test version of TM hosted in Azure.

This site was hosted at [https://tm-hashes.azurewebsites.net](https://tm-hashes.azurewebsites.net/) and since this was a version before the built-in Git Support (where git TM Libraries are natively supported by TM), the only way to get the files was to copy them from the live server.

So my first attempt was to use SFTP (which Azure supports) to connect directly to the web root.

To get the STFP address, I went into Azure's control panel for the tm-hashes site:

![](images/extracting-content-1.png)
Copied the SFTP address and opened it in local windows explorer (which will require login into the **_tm-hashes\tmci_** account):

![](images/extracting-content-2.png)

Navigated to the site's webroot (which are the deployed files)

![](images/extracting-content-3.png)

Then into TM's **_Library_Data_** folder, which is located inside the **_App_Data_** folder (because this is the main location where this site's IIS account has 'write privileges')

![](images/extracting-content-4.png)

In there we can find the **_XmlDatabase\TM_Libraries_** folder which contains all libraries currently loaded in this server

![](images/extracting-content-5.png)

Back in my local VM, I have clone of the target git repository ([https://github.com/TMContent/Lib_Hashes](https://github.com/TMContent/Lib_Hashes)):

![](images/extracting-content-6.png)

into which I'm going to copy the folders from the SFTP live site:

![](images/extracting-content-7.png)

After some time of starting the drop ....

![](images/extracting-content-8.png)

.... I confirm the overwrite

![](images/extracting-content-9.png)

.... and it looks like it will take 1 hour

![](images/extracting-content-10.png)

or maybe 6 hours :

![](images/extracting-content-11.png)

After 38m of copying it is now down to 3h

![](images/extracting-content-12.png)

hummm..... damm  (after 1h and a bit of copying)

![](images/extracting-content-13.png)

That kinda sucks

I think I need to try a different approach :)

**Time to open up the C# REPL included in TM:**

![](images/extracting-content-14.png)

Get the path to the Xml Libraries folder:

![](images/extracting-content-15.png)

Confirm that the folders we want are in there:

![](images/extracting-content-16.png)

Lets first try to zip the forth library:

![](images/extracting-content-17.png)

Which is the Android one:

![](images/extracting-content-18.png)

After the script shown above executes, a quick look at the ftp site shows the expected Android.zip in there:

![](images/extracting-content-19.png)

Which contains the files we want to get:

![](images/extracting-content-20.png)

Next lets do the zip of the entire Libraries folder:

![](images/extracting-content-21.png)

It takes about 1m to create the 11Mb file

![](images/extracting-content-22.png)

Which can now be copied locally

![](images/extracting-content-23.png)

...note how this is much faster than the multiple hours wait we experienced above:

![](images/extracting-content-24.png)

Once the zip file is downloaded:

![](images/extracting-content-25.png)

I unzipped the files into the Lib_Hashes folder:

![](images/extracting-content-26.png)

Choosing to overwrite the existing files:

![](images/extracting-content-27.png)

After the copy, Git will pick up the changed files:

![](images/extracting-content-28.png)

Which we can commit:

![](images/extracting-content-29.png)

And push to GitHub:

![](images/extracting-content-30.png)
