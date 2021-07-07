---
layout: post
title: "Testing Singleton classes in C#"
subtitle: "Useful for testing with test data"
categories: ["Programming"]
tags:
  - .NET
  - C#
  - TDD
---

Singleton object is a design pattern solves the need as stated below in [GOF design patterns](https://en.wikipedia.org/wiki/Singleton_pattern)

> 'Ensure a class has one instance, and provide a global point of access to it.'

I like many also feel that this an anti-pattern. However there are situations where we might need to design a singleton. Something like below:

```csharp
public class Logger
    {
        
        private static Logger _instance;
        private static Object _mutex = new Object();
      
        private TelemetryRecorder(ISomeDependency dep)
        {
           // ...
        }

        public static Logger CreateInstance(ISomeDependency dep)
        {
            if (_instance != null)
                throw new InvalidOperationException("Instance already created");
            lock (_mutex)
            {
                _instance = new Logger(info);
            }
            return _instance;
        }

        public static Logger Instance
        {
            get
            {
                if (_instance == null)
                    throw new InvalidOperationException("Instance not created");
                return _instance;
            }
        }
        // More methods.... as per the design.
        public void SomeMethod()
        {
        }
}
```

While this is basic implementation it does solve the design pattern problems that was mentioned above. There can be more that needs to be added depending on the context it is used.

This however has a problem for writing unit tests. If you want to test against different test data, it won't work because of the single instance. It would be the same instance for all test methods, which defeats the purpose of unit testing with different test data.

While there can be different approaches to solve the problem, here is one approach using .NET Reflection. The idea is to set the instance to null at the beginning of each test method execution/run, so that every time a test method is executed it would create a new instance. 

```csharp

[TestClass]
public class LoggerTests
{
    [TestInitialize]
    public void TestInit()
    {
            new PrivateType(typeof(Logger)).SetStaticField("_instance", null);
    }
    
    [TestMethod]
    public void TestSomething1()
    {
            var concretDependency = GetTestData(1)
            Logger.CreateInstance(concretDependency);
    Logger.Instance.SomeMethod();
    }

    [TestMethod]
    public void TestSomething2()
    {
        var concretDependency = GetTestData(2)
        Logger.CreateInstance(concretDependency);
        Logger.Instance.SomeMethod();
    }
}

```
