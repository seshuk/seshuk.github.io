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

This can be achived via C# code using the classes in **System.Management.Automation** namespace. Especially the Runspace, PowerShell and PSCommand classes.

**[Runspace:](https://msdn.microsoft.com/en-us/library/system.management.automation.runspaces.runspace(v=vs.85).aspx)**
 - Provides options to open connection pipeline to Remote powershell so that PS Commands could be executed.

**[PowerShell:]( https://msdn.microsoft.com/en-us/library/system.management.automation.powershell(v=vs.85).aspx)**

- Provides methods that are used to create a pipeline of commands and invoke those commands either synchronously or asynchronously within a runspace

**[PSCommand:](https://msdn.microsoft.com/en-us/library/system.management.automation.pscommand(v=vs.85).aspx)**

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


