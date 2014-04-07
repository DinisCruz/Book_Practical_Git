##  Adding Tags to TeamMentor Master repository 

With 3.2 out, its time to add some [Git Tags](http://git-scm.com/book/en/Git-Basics-Tagging) to the main [TeamMentor/Master](https://github.com/TeamMentor/Master/) repository (which at the moment has none):  
  
[![](images/CropperCapture_5B10_5D1.jpg)](http://1.bp.blogspot.com/-rHYfla9Q9Rc/UIvGminyqsI/AAAAAAAAA0U/8G6ycjL-Dyk/s1600/CropperCapture%5B10%5D.jpg)

  
In a local Git Bash of this repository, we can create a tag using **$ git tag -a v3.2  -m '3.2 Release'**

[![](images/CropperCapture_5B9_5D.jpg)](http://2.bp.blogspot.com/-1N60bQy8Pnc/UIvG0kMOXbI/AAAAAAAAA0c/GEQOKY7405A/s1600/CropperCapture%5B9%5D.jpg)

  
Next we push that tag into GitHub using **$ git push tm_master v3.2**

[![](images/CropperCapture_5B11_5D1.jpg)](http://2.bp.blogspot.com/-gEwgHdCj388/UIvHI5hSbXI/AAAAAAAAA0k/-mbbo6zWCq4/s1600/CropperCapture%5B11%5D.jpg)

And if we look back in GitHub's Tag page, we will see that our **v3.2 **tag is in there:

[![](images/CropperCapture_5B12_5D1.jpg)](http://4.bp.blogspot.com/-xxFkp25rlvM/UIvHgQQX9YI/AAAAAAAAA0s/yU5gufcHTFc/s1600/CropperCapture%5B12%5D.jpg)

  


At the moment we are keeping track of the previous versions using Git Branches (but I think that tags will do a better job)

[![](images/CropperCapture_5B13_5D1.jpg)](http://1.bp.blogspot.com/-3kqtpxlYh90/UIvIEEOlCkI/AAAAAAAAA00/KMERtlRKspU/s1600/CropperCapture%5B13%5D.jpg)

  
For example here is 3.1 release (with the _f71b016241 _id)

[![](images/CropperCapture_5B14_5D1.jpg)](http://2.bp.blogspot.com/-W3hnl4NRNKo/UIvIEg36PcI/AAAAAAAAA08/2WnLna1-z6E/s1600/CropperCapture%5B14%5D.jpg)

We can use this ID value to create the 3.1 tag

[![](images/CropperCapture_255B15_255D.jpg)](http://1.bp.blogspot.com/-95YJ09Ov3W0/UIvIpgIRI6I/AAAAAAAAA1E/TMQSilUKWJw/s1600/CropperCapture%255B15%255D.jpg)

[![](images/CropperCapture_255B16_255D.jpg)](http://1.bp.blogspot.com/-V53tIoskGpk/UIvIqayi0UI/AAAAAAAAA1I/Mzp4oK8YejE/s1600/CropperCapture%255B16%255D.jpg)

  
Use **gitk **to find the SHA1 ID of the 3.0 release

[![](images/CropperCapture_255B18_255D.jpg)](http://3.bp.blogspot.com/-3MMOcVo7hJA/UIvJjCj3xEI/AAAAAAAAA1k/mLrhkTN7ik0/s1600/CropperCapture%255B18%255D.jpg)

  
Which we use to create the 3.0 tag:

[![](images/CropperCapture_255B19_255D.jpg)](http://1.bp.blogspot.com/-5mOeGVDE3r4/UIvJjyK4FSI/AAAAAAAAA1o/4v5cEqGYW7Y/s1600/CropperCapture%255B19%255D.jpg)

After pushing to GitHub, the Tag page looks like this:

[![](images/CropperCapture_255B20_255D.jpg)](http://4.bp.blogspot.com/-flasZE9Sqnw/UIvJkh7UKNI/AAAAAAAAA1w/VhEIWned38I/s1600/CropperCapture%255B20%255D.jpg)

What is really cool about these Git Tags is that they also provide a nice location to download a particular release :) 






- - - 
[Table of Contents](../Table_of_Contents.md)
