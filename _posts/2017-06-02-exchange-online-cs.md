---
layout: post
title: "Executing PowerShell commands on Exchange inline via C#"
subtitle: "Useful for automating Exchange Online tasks."
categories: ['Programming']
tags:
 - Exchange Online
 - C#
 - Office365
 - PowerShell
---

The default or easy way to manage Exchange Online for administrators would still be the Excahgne management protal. However there are situations where one might want to automate the process or execute scripts remotely. Following article explains how this can be done using PowerShell manually: https://technet.microsoft.com/library/jj984289(v=exchg.160).aspx

This can be achived via C# code using the classes in ** System.Management.Automation ** namespace. Especially the Runspace, PowerShell and PSCommand classes.

** [Runspace:](https://msdn.microsoft.com/en-us/library/system.management.automation.runspaces.runspace(v=vs.85).aspx) **
 - Provides options to open connection pipeline to Remote powershell so that PS Commands could be executed.

** [PowerShell:]( https://msdn.microsoft.com/en-us/library/system.management.automation.powershell(v=vs.85).aspx) **

- Provides methods that are used to create a pipeline of commands and invoke those commands either synchronously or asynchronously within a runspace

** [PSCommand:] (https://msdn.microsoft.com/en-us/library/system.management.automation.pscommand(v=vs.85).aspx) **

 - Defines a pipeline that can be run by a PowerShell object.

The steps to connect and execute commands would be:

 1. Create Runspace - using Exchange online admin credentials.
 2. Create PowerShell object with the above Runspace
 3. Create and pass PSCommand object to Powershell object to execute the same.
 4. Close the Runspace object.


```c#

PSCredential credential = new PSCredential(email, pwdSecString); // Admin email and pwd

wsEOConnInfo = new WSManConnectionInfo((new Uri(https://outlook.office365.com/powershell-liveid/)),
"http://schemas.microsoft.com/powershell/Microsoft.Exchange", credential);

wsEOConnInfo.AuthenticationMechanism = AuthenticationMechanism.Basic;

using (Runspace runspace = RunspaceFactory.CreateRunspace(wsEOConnInfo))
{
    runspace.Open();

    if (runspace.RunspaceStateInfo.State == RunspaceState.Opened)
    {
        PowerShell ps = PowerShell.Create();

        var command = new PSCommand();
        command.AddCommand("Get-Mailbox");
        command.AddParameter("Identity", name);


        ps.Commands = command;
        ps.Runspace = runspace;

        var results = ps.Invoke();

        //iterate thru the results object.
    }

    runspace.Close(); // Additional caution 
}

```


























### Automatically back-up to the Cloud:
Setup MS One Drive or Google Drive to automatically backup camera roll. And then delete photos as they back up. I used One Drive, but google drive gives you cool features like search images based on date, location etc.

### "There is an app for that" - and there lies the problem:

Apps eat up memory and it's not easy to clear that for most of them without uninstalling.

#### Uninstall that Facebook app:
It is a memory hog. I use the web interface. From Safari more options -> Add to Home screen.
The icon is same as the app and you won't even feel the difference. Added advantage of 'No notifications' - fewer distractions. 

WhatsApp is another application that you manually have to manage, the Android and Windows Phone versions are better, in the sense that they download the media directly to the camera roll folder and not a private appdata location. 

#### Use Online Music & Video apps:
I use Saavn and Gaana for most of the music when I want to search for something and listen. Use Manasu to and Radio kushi when I want to go Auto pilot. I don't miss iTunes at all. There are lots and lots of different free services that can be used depending on your liking.

Using YouTube on Chrome gives a way to listen to music on YouTube in the background, with that app you need to pay for that.

I soon hope that Microsoft comes up with so-called Surface Phone with external memory to connect and these will be no issues.

` Do you use any phone with tiny memory? How do you manage? ` 

