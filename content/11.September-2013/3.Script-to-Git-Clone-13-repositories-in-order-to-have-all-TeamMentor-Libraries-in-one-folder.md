## Script to Git Clone 13 repositories in order to have all TeamMentor Libraries in one folder

Part of the push for the 3.4 release of [TeamMentor](https://teammentor.net/), I wanted to have a copy of all TeamMentor libraries locally (there are 13 libraries on the 3.4 release).

Since O2 Platform's FluentSharp has native Git support, I was able to do create the clones using this script (note how simple it is to create a clone from a GitHub repo):  

The script takes about 1m to run:

![](images/image_thumb1.png)

And the end result is a folder with all libraries cloned:

![](images/image_thumb_25255B1_25255D1.png)

With each folder containing the git repository for that library

![](images/image_thumb_25255B2_25255D1.png)

Next, I zipped all these files into the **SI Library --3.4.zip** file (note that they all must be on the root of the zip)

![](images/image_thumb_25255B3_25255D1.png)

Then, on a local QA TM instance, I:

  * went into the admin panel,
  * chose up upload the zip,
  * triggered the installation (i.e. unzip) of those libraries
  * rebuilt the cache:

![](images/image_thumb_25255B4_25255D1.png)

Once that was completed, a reload of the home page shows the 13 libraries:

![](images/image_thumb_25255B5_25255D1.png)

Including the new **_Html5_** library:

![](images/image_thumb_25255B6_25255D1.png)

... and the new **_Scala_** library

![](images/image_thumb_25255B7_25255D1.png)
