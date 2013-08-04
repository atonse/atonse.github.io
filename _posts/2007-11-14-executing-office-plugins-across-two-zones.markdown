---
author: Ashish
comments: true
date: 2007-11-14 20:51:04+00:00
layout: post
slug: executing-office-plugins-across-two-zones
title: Executing Office Plugins Across Two Zones
wordpress_id: 12
tags:
- csharp
- dotnet
- microsoft
- office
- security
---

When building Office plugins, you have to give the right permissions so that the plugins can execute. Depending on your situation, you will have to touch upon multiple security concepts.

One is a Zone. A zone is like the "area" of interest. There are two zones involved in doing this:



	
  * The location of your plugin (the dll files, etc)

	
  * The location of the Word/Excel file being opened (*.doc, *.xls, etc)


These zones usually match up (if your plugin is installed on your computer, and you're accessing an Office document on your hard drive, both locations are the "My Computer" zone).

For my situation, I had the plugin installed in my computer, but the file being accessed was over an untrusted network share, hence the file was placed in the "Internet" zone.

I had my assemblies in C:\Program Files\InstalledAppDir\*
My Word Doc was in: \\networkserver\sharename\something.doc

It triggered the following error:

`The customization does not have the required permissions to execute.`
`
************** Exception Text **************
System.Security.SecurityException: The customization does not have the required permissions to execute.
at Microsoft.VisualStudio.Tools.Applications.Runtime.DomainFactory.CreateDomain(Uri evidenceUri, String domainName, String codeBase, String configFileName, IAddinSecurityManager secman)
at Microsoft.VisualStudio.Tools.Applications.Runtime.AppDomainManagerInternal.CreateCustomizationDomainInternal(Uri uriFullDocumentDirectory, Uri uriFullDocFilePath, String documentName, IHostServiceProvider hostCallback, IAddinSecurityManager secman, AppManifest& applicationManifest, Boolean& manifestDirty, IAppInfo& appInfo)
at Microsoft.VisualStudio.Tools.Applications.Runtime.AppDomainManagerInternal.CreateCustomizationDomain(String applicationDomainPath, String documentName, IHostServiceProvider hostCallback, IExecuteCustomization& executor)
at Microsoft.VisualStudio.Tools.Applications.Runtime.AppDomainManager.CreateCustomizationDomain(String applicationDomainPath, String documentName, IHostServiceProvider hostCallback, IExecuteCustomization& executor)
The Zone of the assembly that failed was:
MyComputer
`
I followed [this guide](http://msdn2.microsoft.com/en-us/library/9w6bd8f1(vs.80).aspx) and tweaked the following policies a little and it now works:

MyComputer zone:
"FullTrust" permissions to the url: C:\Program Files\InstalledAppDir\*
Internet zone:
"Nothing" permission to the url: \\networkserver\sharename
"FullTrust" permissions to the OfficeDocumentMembershipCondition

Make sure you add the membership collection to the internet zone, even if you are accessing a network share. The easiest way to know the zone (and how I found out) is to look at your status bar when you go to the network share. It'll tell you what security zone that path is seen as.
