## Using TeamMentor 3.4 TBot admin pages to load and sync a Library hosted on GitHub

Serge asked me to help making some changes to the [TeamMentor](https://teammentor.net/)'s Asp.NET 3.5 library, and since we need a test server to look at what might be changed (and run some scripts) this is a good time to show about how to use the TeamMentor's 3.4 Tbot pages to load a Library hosted on GitHub

I will also show, how once the TM server is configured with a library using a Git url,  changes can be auto committed/pushed to that Git server, every-time there is a content edition using TM's web editors.

**Step 1: Preparing the target TM server**  

Lets start with an Azure hosted TeamMentor server, for example this one:  

![](images/Screen_Shot_2014-01-29_at_11_01_02.png)

Since we don't need all those libraries in there (and in fact we want to make changes to the .NET 3.5 Library), lets remove them all.

The easiest way to do it is to change the backend location of the TeamMentor XML files, which can easily be done by going into TBot:

![](images/Screen_Shot_2014-01-29_at_11_01_22.png)

... changing the **_TMConfig.config_** file **_XmlLibrariesPath_** value:

![](images/Screen_Shot_2014-01-29_at_11_02_46.png)

... and now, after the cache is reloaded:

![](images/Screen_Shot_2014-01-29_at_11_03_07.png)

... there will be no articles on this instance of TM:

![](images/Screen_Shot_2014-01-29_at_11_03_23.png)

TIP: If you want to quickly add a test Library to TM, you can use the old **_/admin_** panel option to install Libraries from a link or zip. Here is how I quickly installed the OWASP Library, by clicking on the OWASP link in this page:

![](images/Screen_Shot_2014-01-29_at_11_04_08.png)

... which makes my test TM instance now look like this:

![](images/Screen_Shot_2014-01-29_at_11_04_43.png)

**Step 2. Create a Fork of the Target Library**

In this case the TM Library I want to make changes to is the private repo  [tm-sme/Lib_.NET_3.5](https://github.com/tm-sme/Lib_.NET_3.5) which is the one used by SI's SME team to make changes into the next version of TM (the idea is that I will make changes in my Fork which I will then issue a Pull Request to this version)

![](images/Screen_Shot_2014-01-29_at_11_11_07.png)

Next, logged in as **_DinisCruz-Dev_** (which is my day-to-day GitHub not-very-privileged account), I clicked on the Fork link:

![](images/Screen_Shot_2014-01-29_at_11_11_20.png)

... chose the  **_DinisCruz-Dev_** as the Fork target:

![](images/Screen_Shot_2014-01-29_at_11_11_27.png)


... and after a couple seconds I had a Fork of the [tm-sme/Lib_.NET_3](https://github.com/tm-sme/Lib_.NET_3.5) repo at [DinisCruz-Dev/Lib_.NET_3.5](https://github.com/DinisCruz-Dev/Lib_.NET_3.5)

![](images/Screen_Shot_2014-01-29_at_11_11_42.png)

**Step 3: Configuring TeamMentor to load a Library from GitHub**

This next step is a bit different if the IIS user account of the target server is configured to use SSH, but since Azure doesn't seem to support it, we will need to use HTTPS and hardcoded passwords to do this.


The good news is that GitHub now provides a nice way to create temp hard passwords, so I can use that on this blog post :)

On the GitHub's Account Settings for the **_DinisCruz-Dev_** user:

![](images/Screen_Shot_2014-01-29_at_11_18_42.png)

I clicked on the **_Create new Token_** button from the  _Personal Access Tokens_ section (part the **_Applications_** area)

![](images/Screen_Shot_2014-01-29_at_11_18_54.png)

... entered a name for it (the text in this page provides a good explanation for how this token should be used)  
![](images/Screen_Shot_2014-01-29_at_11_19_13.png)

 ... and after it was created:

![](images/Screen_Shot_2014-01-29_at_11_19_19.png)

 ... I copied it into the clipboard:

![](images/Screen_Shot_2014-01-29_at_11_19_27.png)

In this case it the token is **_124f9ce43f8cecd7f56b2a9e412118b01f72cef7_**  

Back in the [DinisCruz-Dev/Lib_.NET_3.5](https://github.com/DinisCruz-Dev/Lib_.NET_3.5) main page I clicked on _copy to clipboard_ button that is close to the clone URL:

![](images/Screen_Shot_2014-01-29_at_11_27_13.png)

... which is this case is **https://github.com/DinisCruz-Dev/Lib_.NET_3.5.git**

Since we need to use this from the Azure instance, we need to hard-code the username and password using the syntax _https://**{username}**:**{passwordOrToken}**@github.com/DinisCruz-Dev/Lib.NET_3.5.git_

... which in this case will be  

**https://DinisCruz-Dev:124f9ce43f8cecd7f56b2a9e412118b01f72cef7@github.com/DinisCruz-Dev/Lib_.NET_3.5.git**

Next step is to go into TBot's **_Edit SecretData_** page:

![](images/Screen_Shot_2014-01-29_at_11_31_38.png)

... enter the Git url in the _Libraries_Git_Repositores_ field, click Save:

![](images/Screen_Shot_2014-01-29_at_11_32_08.png)

... go into the _Reload Server Objects_, click on the **_ Reload Cache_** button  

![](images/Screen_Shot_2014-01-29_at_11_32_22.png)


... which should take a little bit (depending on the size of the Library and server-side network connection speed)

.. until a message shows up that says how many libraries and GuidanceItems/Articles exist in the current server (which means that the git clone was successful and the TM server cache was reloaded)

![](images/Screen_Shot_2014-01-29_at_11_34_19.png)

Opening up TeamMentor shows that we now have the new Library installed in this Azure server:

![](images/Screen_Shot_2014-01-29_at_11_35_46.png)

**Step 4: Configuring server to auto push commit changes into GitHub**  

By default changes made on the server are not immediately pushed into the host server.

That behavior can be changed by setting to **_true_** the _AutoCommit_LibraryData_ setting from the **_TMConfig.config_** file:

![](images/Screen_Shot_2014-01-29_at_11_40_35.png)

Once that is set (and after a server restart or TMConfig settings reload) changes made to TM articles will be auto-commited locally and pushed to GitHub as soon as possible (i.e. there is a bit of a delay in case there are multiple edits going on at the same time).

So see this in action, lets open an article:

![](images/Screen_Shot_2014-01-29_at_11_42_15.png)

... click on the **_Edit WYISWYG_** link:

![](images/Screen_Shot_2014-01-29_at_11_42_35.png)

... and make a change to the article (see **_'THIS TEST'_** below) and click on the **_Save Changes_** button

![](images/Screen_Shot_2014-01-29_at_11_43_04.png)

Once that is done, go back into the GitHub repo site, open the Commits page ([https://github.com/DinisCruz-Dev/Lib_.NET_3.5/commits/master](https://github.com/DinisCruz-Dev/Lib_.NET_3.5/commits/master)) and notice that there is an extra commit done _just now_ (note: in TM 3.4 the commit is done under the server IIS user Git settings, which is usually not set, hence the value 'unknown user', in TM 3.6 there is already a fix to use the current TM Logged in user)  

![](images/Screen_Shot_2014-01-29_at_11_45_59.png)

To really see the 'real time' commits and pushes, go back to the TM Article and make another change (this time around I'm using the **_'Notepad'_** editor):

![](images/Screen_Shot_2014-01-29_at_11_46_35.png)

After a couple seconds from Saving the changes, another commit will exist in GitHub:

![](images/Screen_Shot_2014-01-29_at_11_47_13.png)

... which is made of the user changes (i.e the diff of the changes made on the TM web interface)

![](images/Screen_Shot_2014-01-29_at_11_47_28.png)

**Bonus Feature: Quick restore of an TeamMentor website**  

Not sure if it obvious by now, but what we have created here is a live version of TM whose content changes are being automatically synced (i.e backed up) into an external Git repository.

This means that if we completely lost the current website (let's say that Azure went down, or we had another episode of [AzureGate - how Azure's 'subscription upgrade' crazy mode caused us to stop using Azure for VM Hosting (and Git+GitHub saved the day)](http://blog.diniscruz.com/2013/05/azuregate-how-azures-subscription.html) ), we could create a new instance of this TM website by just:  

1. Creating a new Website using the latest release version from **https://github.com/TeamMentor/Master**
2. Logging in as Admin and in TBot configure add adding the GitRepo Url to the SecretData's _Libraries_Git_Repositores_ value
3. Reload the cache or restart the server

That's it :)

And with Azure's APIs, this could all be scripted, which would make it even faster :)
