---
layout: post
title: "Wix Toolset - Custom Actions - Elevated privileges"
subtitle: "Microsoft Certified Azure Security Engineer"
categories: ["Windows Installer", ".NET", "C#"]
tags:
  - .NET
  - Wix
  - Windows Installer
  - C#
---

Windows Installer custom actions are useful when the developers of an installation package needs implement scenarios that are not provided by default. For example validating user input, encrypting user input or showing custom progress information (time remaining) on the installation UI.

The `CustomAction` element with its various combination of elements provides this option for developers in Wix Toolset.

Documentation for this element can be found [here](https://wixtoolset.org/documentation/manual/v3/xsd/wix/customaction.html)

Custom action example:

```xml
 <Fragment>
    <CustomAction Id='FooAction' BinaryKey='FooBinary' DllEntry='FooEntryPoint' Execute='immediate' Return='check' impersonate='no'/>
    <Binary Id='FooBinary' SourceFile='foo.dll'/>
 </Fragment>
```

The property that is on focus is Execute. This property specifies how, when and what context the action shall be executed. It has different values but most popular or frequently used ones are

- ***immediate:*** Indicates that the custom action will run during normal processing time with user privileges. This is the default.
- ***deferred:*** Indicates that the custom action runs in-script (possibly with elevated privileges).

More info can be found [here](https://wixtoolset.org/documentation/manual/v3/xsd/wix/customaction.html)

Based on documentation the it should be set to deferred in case the action needs to be executed with elevated privileges (for ex: writing to registry).

Also, need to be noted that this will be executed after the Windows UAC dialogue.

The custom action is a simple C# method with in the specified assembly (see above). If the developer needs to access any data from Wix installer the session object can be used. Properties defined in wix can be access via `session["PROPERTY"]` syntax. where PROPERTY is the name of Wix properties.

However, this only works with Custom actions that have Execute set to immediate. For deferred a special property named session`session.["CustomActionData"]` needs to be used. To pass this data from wix to C#, the name of the property and action should match:

```xml
<SetProperty Id="FooAction" Before="FooAction" Value="data" Sequence="execute"/>
<CustomAction Id="FooAction" BinaryKey="BinaryId" DllEntry="FooEntryPoint" Execute="deferred"/>
```

**Note about impersonate:** There is another property named `impersonate`, this specifies if the action need to run as normal user or admin user. For elevated privileges it should be set to 'no'. From my experience this only works when the `Execute` attribute is set to `'deferred'`.
