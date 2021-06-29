---
Layout: post
title: StageBuddy - MoveBuddy 
Author_profile: true
Tags: 'Powershell, ActiveDirectory'
published: true
date: '2021-06-29'
---
Over the past 18 months, I’ve been working on one big project with a main focus on Group Policy.
Without getting into sensitive details, our AD had too many OU's.
Each OU had its own GPO's, AD-Groups, etc etc.
Many of those items were basically the same for each OU but with a different prefix in the name.

The project I’ve been working on, tries to merge as much Group Policy objects as possible. 
This meant analyzing every existing policy to the last detail and then try to define what needs to stay and what needs to go.
What is specific to a branch, what do we need to keep (e.g. printer-handling might differ per branch) and what can we merge into a company-wide solution?
We wrote a GPO-proposal where the new logic was explained, naming conventions were decided on, a governance system was put in place, ... .
Powershell was used to gather the information about the existing group policy objects.

Based off of this huge project, smaller projects derived, these are the ones I’d briefly want to touch on in this post.

In the new AD structure, we only have a few OU's left. Each computer needs to get some metadata written into its properties.
This is important because the metadata will be used in the future to retrieve a specific set of objects by querying AD. 
That means that the data needs to be uniform, up-to-date and above all, very accurate.

To relief our staff of doing this tedious job manually, but also exclude typo's or other human errors, StageBuddy was created.
This is basically a rework from an earlier post i made :  [A-Powershell-GUI-for-staging-computers](https://kristofstroobants.github.io/A-Powershell-GUI-for-staging-computers/) 

![StageBuddy]({{site.baseurl}}/assets/images/StageBuddyMoveBuddy/stagebuddy.png)

It allows for computer creation via a Powershell GUI. V2 just got a lot more complexity behind it because of certain pre-defined conditions.
You choose your desired OU (each OU has its own prefix for groups and computer names), the device type (Laptop\Desktop) and the location.
The locations are the physical branches\divisions that exist in our firm. 
Based on your selection, StageBuddy will calculate all free computer names within its range.
Choosing the location helps StageBuddy to decide which users to display and figures out the associated computer groups.

When you press create, StageBuddy will:

- Create the computer-object in AD in the correct OU
- Add the computer to the desired computer group(s) in AD
- Fill in the meta-data files (extention-attributes,decription,location, ...)

Next came MoveBuddy. MoveBuddy allows to assign an already existing computer to a different user.
This when an already existing uses changes jobs internally or when an existing computer gets assigned to a new user.
In both cases the metadata on the computer-object needs to be updated.
The procedure is basically the same as StageBuddy, it just modifies\updates existing devices instead of creating new ones.

![MoveBuddy]({{site.baseurl}}/assets/images/StageBuddyMoveBuddy/movebuddy.png)

Both MoveBuddy & StageBuddy are currently being used by 50 IT-employees across the corporation.

It simplifies the whole process immensely!
