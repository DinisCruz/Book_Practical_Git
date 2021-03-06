## Adding Tags to TeamMentor Master repository

With 3.2 out, its time to add some [Git Tags](http://git-scm.com/book/en/Git-Basics-Tagging) to the main [TeamMentor/Master](https://github.com/TeamMentor/Master/) repository (which at the moment has none):  

![](images/adding-tags-1.jpg)

In a local Git Bash of this repository, we can create a tag using **$ git tag -a v3.2  -m '3.2 Release'**

![](images/CropperCapture_5B9_5D.jpg)

Next we push that tag into GitHub using **$ git push tm_master v3.2**

![](images/adding-tags-2.jpg)

And if we look back in GitHub's Tag page, we will see that our **v3.2** tag is in there:

![](images/adding-tags-3.jpg)

At the moment we are keeping track of the previous versions using Git Branches (but I think that tags will do a better job)

![](images/CropperCapture_5B13_5D1.jpg)

For example here is 3.1 release (with the _f71b016241_ id)

![](images/CropperCapture_5B14_5D1.jpg)

We can use this ID value to create the 3.1 tag

![](images/CropperCapture_255B15_255D.jpg)

![](images/CropperCapture_255B16_255D.jpg)

Use **gitk** to find the SHA1 ID of the 3.0 release

![](images/CropperCapture_255B18_255D.jpg)

Which we use to create the 3.0 tag:

![](images/CropperCapture_255B19_255D.jpg)

After pushing to GitHub, the Tag page looks like this:

![](images/CropperCapture_255B20_255D.jpg)

What is really cool about these Git Tags is that they also provide a nice location to download a particular release :)
