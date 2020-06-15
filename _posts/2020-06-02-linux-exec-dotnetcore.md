---
layout: post
title: "Executing processes in Linux via C#"
subtitle: "Useful for integrating legacy app in .NET Core"
categories: ["Programming"]
tags:
  - .NET Core
  - C#
  - linux
---

.NET Core is a great way to target multiple platforms using C#. However, there could be situations where one needs to execute a process or integrate with 3rd party app or even perform some kind of batch processing with native apps. While it is similar to how it is done using .NET on Windows, there are few details to keep in mind.

Here are basic notes on how to start processes from C# with .NET Core applications:

This can be achieved via C# code using the classes in **System.Diagnostics** namespace, Process and ProcessStartInfo classes.

**[Process:](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.process?view=netcore-3.1)**

- Provides access to local and remote processes and enables you to start and stop local system processes.

**[ProcessStartInfo:](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.processstartinfo?view=netcore-3.1)**

- Specifies a set of values that are used when you start a process.

The steps to execute the process would be:

1.  Create ProcessStartInfo object and set required properties.
2.  Create Process object with the above startInfo
3.  call process.Start on the process object.

```c#

var startInfo = new ProcessStartInfo()
        {
            FileName = "<Full Path to the linux exe>",
            Arguments = "<Arguments if any>",
            UseShellExecute = false, //Import in Linux environments
            CreateNoWindow = false,
            RedirectStandardOutput = true,
            RedirectStandardError = true
        };

var process = new Process()
        {
            StartInfo = startInfo,

        };

        process.OutputDataReceived += (sender, data) => {
            System.Console.WriteLine( data.Data);
        };

        process.ErrorDataReceived += (sender, data) => {
            System.Console.WriteLine(data.Data);
        };

        try{
            process.Start();
            process.WaitForExit();
        }
        catch(Exception ex)
        {
            System.Console.WriteLine(ex);
        }
```

Note: Its important to pass the full path of the executable to the startInfo.FileName property on Linux. If the executable resides in the same location as the .NET Core app, then the below can be used to retrieve the path.

```C#
System.IO.Path.GetDirectoryName(System.Reflection.Assembly.GetEntryAssembly().Location)
```
