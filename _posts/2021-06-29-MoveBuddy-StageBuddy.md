---
Layout: post
title: StageBuddy - MoveBuddy 
Author_profile: true
Tags: 'Powershell, ActiveDirectory'
published: true
date: '2021-06-29'
---
Over the past 18 months, I’ve been working on one big project with a main focus on Group Policy.<br/>
Without getting into sensitive details, our AD had too many OU's.<br/>
Each OU had its own GPO's, AD-Groups, etc etc.<br/>
Many of those items were basically the same for each OU but with a different prefix in the name.<br/>

The project I’ve been working on, tries to merge as much Group Policy objects as possible. <br/>
This meant analyzing every existing policy to the last detail and then try to define what needs to stay and what needs to go.<br/>
What is specific to a branch, what do we need to keep (e.g. printer-handling might differ per branch) and what can we merge into a company-wide solution?<br/>
We wrote a GPO-proposal where the new logic was explained, naming conventions were decided on, a governance system was put in place, ... .<br/>
Powershell was used to gather the information about the existing group policy objects.<br/>
<br/>
Based off of this huge project, smaller projects derived, these are the ones I’d briefly want to touch on in this post.<br/>
<br/>
In the new AD structure, we only have a few OU's left. Each computer needs to get some metadata written into its properties.<br/>
This is important because the metadata will be used in the future to retrieve a specific set of objects by querying AD. <br/>
That means that the data needs to be uniform, up-to-date and above all, very accurate.<br/>
<br/>
To relief our staff of doing this tedious job manually, but also exclude typo's or other human errors, StageBuddy was created.<br/>
This is basically a rework from an earlier post i made :  [A-Powershell-GUI-for-staging-computers](https://kristofstroobants.github.io/A-Powershell-GUI-for-staging-computers/) <br/>
<br/>
![StageBuddy]({{site.baseurl}}/assets/images/StageBuddyMoveBuddy/stagebuddy.png)
<br/>
It allows for computer creation via a Powershell GUI. V2 just got a lot more complexity behind it because of certain pre-defined conditions.<br/>
You choose your desired OU (each OU has its own prefix for groups and computer names), the device type (Laptop\Desktop) and the location.<br/>
The locations are the physical branches\divisions that exist in our firm. <br/>
Based on your selection, StageBuddy will calculate all free computer names within its range.<br/>
Choosing the location helps StageBuddy to decide which users to display and figures out the associated computer groups.<br/>
<br/>
When you press create, StageBuddy will:<br/>
<br/>
- Create the computer-object in AD in the correct OU
- Add the computer to the desired computer group(s) in AD
- Fill in the meta-data files (extention-attributes,decription,location, ...)
<br/>
Next came MoveBuddy. MoveBuddy allows to assign an already existing computer to a different user.<br/>
This when an already existing uses changes jobs internally or when an existing computer gets assigned to a new user.<br/>
In both cases the metadata on the computer-object needs to be updated.<br/>
The procedure is basically the same as StageBuddy, it just modifies\updates existing devices instead of creating new ones.<br/>
<br/>
![MoveBuddy]({{site.baseurl}}/assets/images/StageBuddyMoveBuddy/MoveBuddy.png)<br/>
<br/>
Both MoveBuddy & StageBuddy are currently being used by 50 IT-employees across the corporation.<br/>
<br/>
It simplifies the whole process immensely!<br/>
<br/>
The biggest lesson learned in this one was how to use a simple C# function into a Powershell project.<br/>
On the rich
