## AzureGate - how Azure's 'subscription upgrade' crazy mode caused us to stop using Azure for VM Hosting (and Git+GitHub saved the day)

Late last night all the main TM hosted sites went down!

The reason is Azure's crazy 'subscription expired' workflow which  you can read what other Azure users had to say about it when I happened to them on [http://stackoverflow.com/questions/12791020/windows-azure-virtual-machine-deleted-after-spending-limit-reached-how-can-i-g](http://stackoverflow.com/questions/12791020/windows-azure-virtual-machine-deleted-after-spending-limit-reached-how-can-i-g) and Microsoft's view on it [http://blogs.msdn.com/b/narahari/archive/2012/10/18/windows-azure-virtual-machine-disappeared-or-gone-how-do-i-recover.aspx](http://blogs.msdn.com/b/narahari/archive/2012/10/18/windows-azure-virtual-machine-disappeared-or-gone-how-do-i-recover.aspx) (note how the crowd in the comments are not happy with it)

Below is the email I sent internally at SI, with my debrief on what happened:  

------------------------------------------------(start)

Ok so we are back online with  


  * [https://www.teammentor.net](https://www.teammentor.net/)
  * [https://services.teammentor.net](http://services.teammentor.net/)
  * [https://owasp.teammentor.net](https://owasp.teammentor.net/)
  * [https://tm4tm.teammentor.net](https://tm4tm.teammentor.net/)

Here are some notes:

* **The outage lasted about 14h**
* **This is an example of 'worse case scenario' where our 'Data center' effectively went down**
* **The good parts is that:**

* The prob was picked up quite quickly
* We had a 'fully working' [Teammentor.net](http://teammentor.net/) site (i.e. with the content and users configured) up in about 15m (namely the one I created which was available on a direct IP)
* Roman was able to create a replacement server (for all 4 sites) in about 2hours (and that could had been 30m if Roman had not hit on a permission issue (and had done this type of deployments before))
* The fact that TM's team spreads a multiple time-zones allowed us to react quickly
* Due to TM's current architecture, if we did had customers who NEEDED to have access to TM guidance ASAP (see comment below) we would had several solutions for them (including giving them a full download to run locally)
* This was the first time we really put the new 3.3. TeamMentor's _'auto commit and push to GitHub'_ architecture in action, and I'm happy that it worked quite well (we can still fine tune it a bit, BUT this could had been MUCH worse (note that than even now we still don't have access to the old TM VMs since the VM login accounts are not working as expected, so if the userdata was not on GitHub, we would had not been able to restore the users)

* **The bad parts is that:**

* Nobody really cared :(

* Where were the 'urgent call for TM to be up?', twitter hashtag of TM failure!!!, 'vulnerabilities not being fixed because TM is down'
* The sales guys were not 'up in arms', 'potentials sales were not affected'
* Ed or Jason were not woken up in the middle of the night with a "WTF, TM is down!!!" (note: I was about to go to bed when I noticed that something was wrong in TM's world)

* Like Roman was mentioned: "We drove for 14h on the wrong side of the road, and nothing happened"
* We found the hard way that we can't trust Azure for live sites
* Azure really fucked us up. Roman just confirmed that the Azure GUI a couple days where still saying something like '_your subscription is going to end in 20ish days_' (and destroying VMs and it's configuration is a very crazy way to handle 'account suspension for lack of payment or wrong subscription mode')
* We also found a 'single-point' of failure where MK was the only one that could change the DNS (this is the main reason that it took 14h vs 2h/30m)
* and since 'nobody was really complaining' about TM's MIA, there was no urgency to contact MK (who was dealing with a number of personal probs related to his _"car losing a wheel on the motorway!"_ )

Since we now have a fully working TM environment, we can spend a couple days thinking about the best place to host the TM VMS.

I like EC2, but we can go anywhere that give us good VM management

------------------------------------------------(end)
