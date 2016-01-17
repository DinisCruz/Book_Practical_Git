## Creating a version TeamMentor which uses the new GitUserData.config file

Introduced in the 3.3 version of TM is a new feature to load the UserData repository from an external location (GitHub or local folder).

This post shows how to set it up.

First step is to get the latest version of TeamMentor from GitHub, where we can clone it locally or download the zip file

![](images/creating-version-1.png)

Using the Zip file has an example, unzip the 10Mb file into a local folder, and click on **_start_TeamMentor.bat_**  

![](images/creating-version-2.png)

This will open an empty TM site, and a new Library_Data folder should had been created:

![](images/creating-version-3.png)

With this default structure:

![](images/creating-version-4.png)

Now in GitHub (or on a local folder), create a new Git Repository (which should be marked as private, since security sensitive data will be stored here)

![](images/creating-version-5.png)

Once the repository is created, copy its git url (in this case [git@github.com:TMClients/Site_vulnerabilities.teammentor.net.git](mailto:git@github.com:TMClients/Site_vulnerabilities.teammentor.net.git) )

![](images/creating-version-6.png)

Back in the local copy of TeamMentor, open the TBot page:

![](images/creating-version-7.png)

which will require an admin account:

![](images/creating-version-8.png)

After login, open the **_Edit GitUserLocation_**  

![](images/creating-version-9.png)

And enter the Git url copied from GitHub:

![](images/creating-version-10.png)

After the data is saved, go back to the commands list:

![](images/creating-version-11.png)

Go to the **Reload Server Objects**  

![](images/creating-version-12.png)

And click on 'Reload UserData':

![](images/creating-version-13.png)

After that step is completed, if you look at the **_Library_** Data folder, you should see a new UserData folder in there (that uses the git repository name as part of its path)

![](images/creating-version-14.png)

Inside it, you will see the README.md that was received from GitHub, and a new TMSecretData.config and Users folder

![](images/creating-version-15.png)

Back in TBot's page, if you click on any link you should be redirected to the login page, and you will need to login again using the default admin credentials (this happens because the current browser cookie is pointing  
to the admin user that is in **_XmlDatabase\User_Data_** and not in the newly created **_XmlDatabase\User_Data_Git_Site_vulnerabilities.teammentor.net_**:

![](images/creating-version-16.png)

After logging in, open the **_Edit SecretData_** command:

![](images/creating-version-17.png)

Which should look like this (with correct values for the Rijndael and SMTP fields):

![](images/creating-version-18.png)

The value that we want to change is the **_Libraries_Git_Repositories_**, which should point to the Git repo we want to add to this TM instance. In this case:

![](images/creating-version-19.png)

Add the git url as an item in the **_Libraries_Git_Repositories_** Javascript array:

![](images/creating-version-20.png)

After the data is saved, open the **_Reload Server Objects_** again:

![](images/creating-version-21.png)

And this time around click on the **_Reload Cache_** button:

![](images/creating-version-22.png)

Once that is completed, if your open the **_XmlDatabase/TM_Libraries_** folder, you should see a new **_Vulnerabilities_** subfolder

![](images/creating-version-23.png)

Which is in fact a git clone:

![](images/creating-version-24.png)

of the git repository configured on the **_Libraries_Git_Repositories_** value

![](images/creating-version-25.png)

Quickly opening the main TM page, will now show the **_Vulnerabilities_** Library:

![](images/creating-version-26.png)

Final step is to do manually commit the changes made to the **_User_Data_Git_Site_vulnerabilities.teammentor.net_** local repository (note: auto commit and push is disabled on the UserData when running TM from localhost)

![](images/creating-version-27.png)

Which will put those updates in GitHub

![](images/creating-version-28.png)

Now that we have this GitHub repository configured, we can configure the **_Git UserLocation_** of live QA server:

![](images/creating-version-29.png)

And after reloading the cache:  

![](images/creating-version-30.png)

The [https://tm-vulnerabilities.azurewebsites.net](https://tm-vulnerabilities.azurewebsites.net/) will now have the **_Lib_Vulnerabilities_** library

 ![](images/creating-version-31.png)
