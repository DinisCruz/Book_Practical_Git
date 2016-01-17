## Handling content changes made on hosted site created by Git clone (with auto Git commits and pushes)

Here is the next interesting TeamMentor (TM) and GitHub problem to solve:  

**"How to deal with content changes made using TM's online editing capabilities"**

Here is the 'Problem description':

* TM is published from a Git Repository into a Server (let's call it from **REPOSITORY A** to **SITE A**)
* There are two deployment modes that already work well:
* Publish to cloud (Azure or AppHarbor): takes about 2 to 5 minutes
* Publish to EC2 server: takes between 10 to 30 minutes and includes custom DNS and IIS set-up/deployment
* In either mode the idea is that **REPOSITORY A** is the master version of the Code+Data
* This means that if we needed to rebuild that site, we could (ie. should) be able do it in minutes
* Upgrades and patches are made via a simple git pull (which gets the latest version from the **REPOSITORY A**) and no git merge activity should be needed
* But what happens when there is a content change on **SITE A**'s files?
* An automated solution is needed, since the option of _'RDPing into the server to do the commits/push'_ or _'trying to do the commits/push via TM's GitHub interface'_, not only don't scale but are as dangerous as replying on manual backups.

Here is what I have in mind:

* TM detects if git support exists on the deployed server (i.e git.exe is available) and:
* Git checkout (the deployed branch) into a special 'live_server' branch
* Auto git commit on every TM Content save (or creation) with the commit message being a mix of: Current user, its IP, the date and time and the file affected
* (if configured) auto-push the change to an GitHub repository
* This could be done by configuring an SSH key on the server, or by hardcoding the GitHub credentials into the 'Git remote' value
* If git.exe is not available, then these commits and pushes will need to be done manually (by zipping the whole content folder and moving it into a location with git.exe available)
* In terms of the repository to push, I think that we shouldn't push directly to the original **REPOSITORY A** (the one used to create **SITE A**), but we should push it to a fork/clone of **REPOSITORY A** which could be used as a staging location (one where Pull Requests into **REPOSITORY A** would be made)
* Of course that we could push into **REPOSITORY A** directly, but that would expose an account with git push privileges to an important repository, and could create a scenario where unauthorized changes were made into one a production repositories (also note that with git push privileges, it is possible to completely remove all history and commits from a repository (in effect deleting all information)).

What I like about this solution (the auto-commit with option to auto-push) is that it will provide TeamMentor with a state-of-the-art version control solution (at article level).

Every single change would be logged, and although this will most likely make that branch completely unreadable by humans we will be able to have really powerful (and cool) per-article version history (ie. for each file, see its complete change log, including 'who did the change').

Note that it is possible to combine a number of commits into one (not in GitHub, but in git.exe) so I think that for cases where a number of files were changed, we might want to consolidate them into larger commits (specially when pushing those changes to 'user consumable' repositories)

What do you think?

Any better ideas?
