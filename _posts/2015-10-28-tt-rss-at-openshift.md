---
layout: post
title: TT-RSS at OpenShift
date: '2015-10-28 21:13:59'
tags:
- tech
---

I actually started to like OpenShift (Git flavored). But that's not what I want to write about here. This post is about the Reader... 
Since Google Reader died (two years ago, though it feels already like eons) I tried all sorts of alternatives but always came back to one and the same: [**tt-rss**](https://tt-rss.org/gitlab/fox/tt-rss/wikis/home). It works well, it is reliable and has been collecting and serving me news each and every day for the past couple of years. Until now, the instance I used was somewhere on a server in France, which, although it never let me down, was not under my control and if the guys there one day decide to put an end to it, there will be nothing I could do about it. 
Options? 
I did not even try to put it on a Raspberry Pi (apparently, from what I read, performance is quite bad) and I never came across a similar server on the web (I must confess, though, I did not try too hard). 
But there is another option. OpenShift has a **tt-rss** application cartridge which is easy to install: find it, name it and deploy it. 
Done. 
Well, not quite. 
The last version they have is 1.9 and even if you clone it with git and modify config.php so that the *updater* plug-in could run and push it back and run the updater it will not go past that version. The French server I used has v1.12 as standard, which you, as user, cannot modify in any way. Is that the last version, the most up-to-date version?, I asked myself. Nope! The last *tt-rss* version is 15.7. Don't know exactly how it develops but it does seem quite a span between them. 
So, how to get there? 
*tt-rss* moved to Gitlab and the update process is different. 

What you can do however is this: 

* clone your *tt-rss* instance

        git clone ssh://YOURAPPNUMBER@YOURAPP.rhcloud.com/~/git/APP.git/ ttrss

(You can see and copy and then paste exactly what you have to use on the right side of the screen when managing your app.)

* go to the directory where you put your cloned stuff 

        cd ttrss

*  look for config.php and save a copy (you'll need it later). 
*  now run these two commands: 

        git remote rm origin
        git remote add origin https://tt-rss.org/git/tt-rss.git 

*  you are ready to upgrade *tt-rss* to its latest version 

        git pull origin master 
*  the command will update the *tt-rss* instance at OpenShift but it will also wreck havoc on the config file and will delete a couple of directories. Do not worry. When it's done updating, clone it again, this time in another directory. 

        git clone ssh://YOURAPPNUMBER@YOURAPP.rhcloud.com/~/git/APP.git/ ttrss-1

*  move to this new directory 

        cd ttrss-1

*  and look for config.php. Its content will be quite different from the content of the config.php file you saved before. Replace the new config.php with the version you saved previously. Or, if you do not feel comfortable just replacing it, open them both side by side and decide which settings you want to keep and which you want to overwrite. 

*  in ttrss open the *php* directory and remove everything in it. In ttrss-1 copy its content and put it in the now empty *php* from ttrss.  

*  *push* it back to OpenShift

        git add -A
        git commit -m "Upgrade"
        git push

* Done! 

It might look a bit too cumbersome but it is easier than you would think. 

Now, import your OPML file with your feeds, set them as you wish, change the admin password and... that's it! 

Happy reading! 


Update: you should remember though that you only get 1GB of traffic with OpenShift. If you go over it, the app will stop working properly. 
