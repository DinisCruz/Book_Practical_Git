## Creating a new TeamMentor test site using TeamCity, GitHub and Azure

Serge just asked me to create a new TeamMentor (TM) website for him using a particular TM library, so here are the steps I took (note: some of this will be automated in the next TM release)  

**In Azure ....**  

It all started by going into Azure and creating a new website:

![](images/creating-a-new-1.png)

In this case called tm-hashes

![](images/creating-a-new-2.png)

in a couple secs it was available

![](images/creating-a-new-3.png)

next I set-up git publishing:

![](images/creating-a-new-4.png)

using  'Local Git' since that works well with TeamCity and doesn't require that Azure is given pull privileges into the target repo:

![](images/creating-a-new-5.png)

Azure worked for a bit, and after a couple secs I had:

![](images/creating-a-new-6.png)

**In TeamCity ...**

Next, in the TeamCity server, to make it easier on next deployments, I added this site to one of the builds that already pushes other sites into Azure:

![](images/creating-a-new-7.png)

Specifically I added another build-step similar to the ones already there for tm-vulnerabilities and tm-DennisGroves

![](images/creating-a-new-8.png)

The easiest way to do it, was to create a copy of one of the existing steps:

![](images/creating-a-new-9.png)

After editing the 'copied build step', called _Publish to Azure (tm-Hashes)_, I quickly reordered the build steps

from:

![](images/creating-a-new-10.png)

to:  

![](images/creating-a-new-11.png)

Next, I clicked on Run:

![](images/creating-a-new-12.png)

in order to trigger a TeamCity build:

![](images/creating-a-new-13.png)

That build will:

* do a git pull from the latest version of the TM code (currently at 3.3 RC3.01),
* build the VisualStudio main project,
* and push to Azure


Here are the build logs during the 'push to Azure' step:  

![](images/creating-a-new-14.png)

At this moment the Azure admin page for the tm-hashes site, will show a **_Deploying_** message

![](images/creating-a-new-15.png)

which becomes **_Active Deployment_** once it is completed:

 ![](images/creating-a-new-16.png)

One of the nice hacks the Azure team did with their git implementation is to provide good messages/info in the git data sent back on pushes (the lines in dark-orange below where created by Azure):

![](images/creating-a-new-17.jpg)

Once the push in complete, we can browse the Azure site:

![](images/creating-a-new-18.png)

And see an empty TeamMentor installation:

![](images/creating-a-new-19.png)

**In TM Control panel using GitHub zip file ...**  

The final step is to add the library that Serge wants (note: for this example I'm going to install the library via drag and drop of zip files.)

To get the library files, I went to its private Github repository, and clicked on the **_zip_** button

![](images/creating-a-new-20.png)

which downloaded the zip file into my current vm:

![](images/creating-a-new-21.png)

back in TeamMentor,

I logged in:

![](images/creating-a-new-22.png)

as admin

![](images/creating-a-new-23.png)

went to the control panel:

![](images/creating-a-new-24.png)

clicked on **_Advanced Admin Tools_** and **_Install/Upload Libraries_**

![](images/creating-a-new-25.png)

![](images/creating-a-new-26.png)

drag-n-dropped the local zip file into the **_Upload a file_** red box

![](images/creating-a-new-27.png)

Depending on the network speed, this can take a couple seconds or minutes:

![](images/creating-a-new-28.png)

Once the upload was completed,

I clicked on the 'Lib_Hashes-master.zip' link that appeared at the top:

![](images/creating-a-new-29.png)

waited a little bit:

![](images/creating-a-new-30.png)

and once I saw the success message:

![](images/creating-a-new-31.png)

I clicked on _**Open Main Page**_  

![](images/creating-a-new-32.png)

and the main TeamMentor GUI showed the imported libraries:

![](images/creating-a-new-33.png)

The final step was to remove the original temp library (created by TeamMentor on first install)

![](images/creating-a-new-34.png)

![](images/creating-a-new-35.png)

![](images/creating-a-new-36.png)

And finally, I sent Serge an email with the link to his brand new install of TeamMentor :)

![](images/creating-a-new-37.png)
