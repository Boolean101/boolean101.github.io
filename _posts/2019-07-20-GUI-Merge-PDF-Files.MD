---
Layout: post
title:  GUI - Merge PDF files with PowerShell and PDSSHarp.DLL library 
Author_profile: true
published: true
date: '2019-07-20'
---

Back in May 2019 I was at a colleague's desk for a technical intervention.

While debugging the issue at hand, the user showed me his work-process.

He was manually exporting 5 to 10 PDF-files from an email and merging them one by one into a new PDF-file. 
I asked him how many times he would do this and it turned out that he was doing this several times a day, taking up a lot of time.

A little baffled of the boring and time consuming process, I went back to my own workplace. 
I started Googling and I came across several open source projects for merging PDF-files.
The ones that got mentioned most, were PDFSharp and ITextSharp. I went for [PDFSharp](http://www.pdfsharp.com/PDFsharp/ "PDFSharp").

I designed a small GUI in PowerShell Studio 2019. It allows you to choose a root-folder.

![1]({{site.baseurl}}/assets/images/MergePDF/1.png)  


The application will then recursively search through all folders in search for PDF-files.
You would then check all the files you wish to merge and press "Merge".

A second thread will spin up and will do the merging.
This allows for the GUI to remain responsive while doing the merge.

![2]({{site.baseurl}}/assets/images/MergePDF/2.gif)  
*the green does not happen IRL, for some reason while recording it added this.*

The newly merged file is automatically stored on the user's desktop.
The filename will have the prefix "MergePDF_" followed by the datetime. This will make sure that each merge has a unique filename.
After saving the file the application will automatically open the newly created PDF so that the user can visually confirm all is well.

# Updated in July #

The application has been in use for about 3 months and people had a request to add the full path into the PDF file.
This was more for a visual verification than anything else.

I added an option named "Annotation". This will add the location of the PDF-file into the newly merged PDF.
It will print this in a red color so that users can spot it with ease.

![3]({{site.baseurl}}/assets/images/MergePDF/3.png)  

# Updated in July V2#

So it seems that some PDF-files can has a "corrupt structure". Because of that, the PDFSharp library isn't able to process the file and will fail.
This rarely happens but it does. Upon failure, the user is shown a textfile with all the filenames that would not have been included in the merge.
