---
layout: post
title: Blogging with Ghost
date: '2015-10-06 11:55:33'
tags:
- scribbles
- digital-computer
- tech
- ghost-tag
- blogging
- digital-ocean
- jekyll
- tumblr
- wordpress
- nibbleblog
- pico
- git
- netlify
---

Perhaps this is just a way to avoid doing more important stuff, like writing or translating or, at least, reading. But I wanted to find a way to keep this blog without having to worry too much about server security, about upgrades, bugs, drive corruption and, last but not least, about enough credit toward my Digital Ocean account. 
There would be some free alternatives, although I would not really trust a free VPS provider, and that would still not spare me the time and worries about security and flawless deployment. 
I know, there are places like [Ghost foundation itself](https://ghost.org/pricing/) (rather expensive, I think, but if I would earn a living writing blogs, I can see myself using their platform), [RunKite](https://www.runkite.com/) and some other providers. Prices vary but they're never free. 
What other choices would I have, then? 
Well, what I knew was that I would not want to turn back to WordPress. Even if it... just works and you have little to worry about and there are I-don't-know-how-many-millions-of-users, I always found it too clunky, heavy and ungraceful. Yes, there are ways of promoting your writing (freshly pressed, random posts to read, etc.) but the thing is I never have too many readers anyway. I mostly write for myself. And if you want a custom domain, you have to pay a yearly fee. In turn, your scribbles will remain on their servers for a looong time and are relatively easy to export/import. But no! No WP for me. 
What's left? 
[Tumblr](http://tumblr.com)? It is worth considering... if you like being attacked by an army of GIFs each time you go to your Dashboard and want to post something. Yes, it is snappy, you can map your domain name for free with them, you have tons of themes to choose from and edit them to your heart's delight (you can even edit the HTML code and upload your own CSS) and there are all sorts of users (from *The Paris Review* to *Anthony Bourdain*, and from your next door neighbor to a teenage girl in Siberia) but... You cannot import or export any of your posts easily and thus you cannot migrate if they will get sold again or go out of business. And, let's face it, the bubbles and flashes and the glitz are a bit too much! It might be fun, but no thanks. 

[Blogger](https://www.blogger.com/)? Pass. 

Then, there are the minimalist platforms like [Svbtle](https://svbtle.com/) (paid service), [Medium](https://medium.com/) (no custom domains - correction: as of today, Oct.08/15, they seem to allow it). [Postach.io](http://postach.io) and rest? I'll pass, again. Medium and Svbtle (and [Silvrback](https://www.silvrback.com/), since I am at it) are pretty much the same. They are all clean and invite you to write but you have to pay and/or *join the club*. Otherwise, there's no playin'. And my writing is not important enough to compel me to pay for being hosted. No way. 

Putting the blog on Github, with [Jekyll](https://jekyllrb.com/)? Tried that too. Too much effort, again. Git adding, committing, pushing each time you want to make a post... Text in separate editor. Copy & Paste. Deploying. And moreover, everything is public, available for anyone to see (I do have a couple of private blogs and there is no way to password protect them - you need some sort of ServerSide script to make that work). And then, for a simple email form (a contact form, that is) you need a third party involved. Static sites are cool, indeed, but they do not come free from headaches. Headaches which I would gladly want to go through but only for a larger enterprise and perhaps a wider public. 

Blog-aware PHP applications came also under scrutiny. [Nibbleblog](http://www.nibbleblog.com/), [Pico](http://picocms.org/index.html), etc. They too are nice to play with. But sometimes I had the feeling they are so simple that they are almost rudimentary. They're low on resources, true, but they still need a hosting platform with PHP enabled. 

A one-pager (could one get any... simpler than that?) would have been something interesting. Perhaps. Keep a folder in your Dropbox, write in MarkDown, copy and paste in your index.html and then drag it into your... [Netlify](http://netlify.com) account, for example (they have a free tier, though with an inconspicuous Netlify badge on it). But it is relatively difficult to implement, with all the SEO issues and a DB-less posts archive. But you can have a password protected site too, if you so wish. And they are fast, no doubt about it. 

So... I kept coming back to Ghost. There is nothing out there today that is as simple, clear and fast as Ghost. Split-screen is good, MarkDown works, tags allow you to put up a website/blog in no time, you get password protection for your private blogging needs, you can make corrections on the fly just by typing /edit at the end of the post url (which will take you straight into editing mode), you can export all you ever wrote in a .json file, there are enough themes to play with, etc. etc. 
If I could only host it without having to worry about the infrastructure and take my domain name with me... I tried [OpenShift](https://openshift.redhat.com) a while ago but was not very happy. I found it rather slow and relatively difficult to work with behind the scenes (rhc console & Co.). But I returned to it and tried it once more. So far, no issues. It is easy to install (just set up a new application and choose Ghost and you're done). 

Then I realized it is easier to manage it via git: 

>git clone ssh://YOURAPPNUMBER@YOURAPP.rhcloud.com/~/git/APP.git/ PATH-IN-YOUR-PC

*You can see what you have to paste into your console on the right side of the screen when managing your app.*

>git add -A

>git commit -m "MESSAGE OF CHOICE"

>git push

Thus, you have your blog infrastructure on your PC, you can update it as and when you wish (or when an update is available) and modify it if you need to, then put it back in its OpenShift cartridge and let it live there in peace. 

*Since I am talking about updating here, I should mention that trying to import a .json file from Ghost 0.7.0 into Ghost 0.6.4 does not work. You'll get an error message and cannot do anything about it. Not even manipulating the archive works - their content is slightly differently coded. It seems the only explanation is that they are not backwards compatible. (Sigh!)* 

OpenShift does not seem to be significantly slower than Digital Ocean. I have only later realized that what I perceived as slow, was actually the application being set on *idle* and taking its time to wake-up again. With the free tier, any application will go to sleep after 24 hours of not being used. To solve this you only need to upgrade to Bronze. No costs involved as long as you keep your apps number down to three. No problems there!

The only caveat? I had to set up a redirect from cento.red to www.cento.red, which is a small price to pay, though for what you get. 

So long Digital Ocean! And thank you very much! I would happily come back if I were to blog on a larger scale but for now, I'll keep a low profile. Btw, what's with the Russian server? My dropplet should be on a server in Frankfurt, but whenever I launched a *Traceroute* on my IP, it seemed that the server was lost somewhere in Siberia. How come? 

