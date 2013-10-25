---
layout: post
title: "WebDev Turmoil"
description: "Path of the Web Developer Episode I"
category:
tags: [Databases, Startups]
---

Repeat after me...

####"DATABASE MIGRATION IS AS IMPORTANT AS HAVING A VCS."
If you're a newbie who's into WebDev like me, the above mantra should be the 1st of your 108 mantras. 

I'm currently working as a developer in a small startup. We're a team of four and we are working with the LAMP technology stack. Let me tell you why I'm writing this post..

I did a feature implementation few days back and had created a couple of models and did a whole lot of tweaking in that process to the Database. Had this been just a code change which had to do with the Controllers or Views, we could've easily version-ed the code using GIT or any other VCS. But this Database tweak needed a Migration to be done and we didn't have that in our code. Result? I pushed my code yesterday and my boss is still finding out the differences in the Database. We are due to do a Beta Release by EOD today and at this rate I think it's highly unlikely that it'll happen. So here I am, sitting at my desk just blinking at the monitor for the last four hours, ranting why it's a thumb rule or a best practice to create a Migration immediately after you create your Database.

Almost every framework today, supports Migration. So, whichever framework you're working on, make sure you create and update your Migration whenever you play around with your Database. Happy developing!  

May the Force be with You!