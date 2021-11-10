# attempt-dotnet

Trying to get single file output for a Windows console app.

## Build output is not single file

`dotnet build src` produces a .exe and a .dll.  I can call the exe from CMD as well as the dll, using `dotnet Hello.dll`.  I see that the exe is a wrapper for the `dotnet` call.  

I think the two-file output at this point is expected behavior.  So I want to try `dotnet publish src`.

## Publish won't work

`dotnet publish src` gives me the following output

```
Microsoft (R) Build Engine version 17.0.0+c9eb9dd64 for .NET
Copyright (C) Microsoft Corporation. All rights reserved.   

  Determining projects to restore...
  All projects are up-to-date for restore.
  Hello -> C:\Users\swyant\code\attempt-dotnet\src\bin\Debug\net6.0\Hello.dll
C:\Program Files\dotnet\sdk\6.0.100\Sdks\Microsoft.NET.Sdk\targets\Microsoft.NET.Publish.targets(102,5): error NETSDK1097: It is not supported to publish an application to a single-file without specifying a RuntimeIdentifier. You must either specify a RuntimeIdentifier or set PublishSingleFile to false. [C:\Users\swyant\code\attempt-dotnet\src\Hello.csproj]
```

... and `dotnet publish -r win-x64 src` gives me

```
Microsoft (R) Build Engine version 17.0.0+c9eb9dd64 for .NET
Copyright (C) Microsoft Corporation. All rights reserved.

  Determining projects to restore...
C:\Users\swyant\code\attempt-dotnet\src\Hello.csproj : error NU1100: Unable to resolve 'Microsoft.NETCore.App.Runtime.win-x64 (= 6.0.0)' for 'net6.0'. [C:\Users\swyant\code\attempt-dotnet\src\Hello.sln]
C:\Users\swyant\code\attempt-dotnet\src\Hello.csproj : error NU1100: Unable to resolve 'Microsoft.WindowsDesktop.App.Runtime.win-x64 (= 6.0.0)' for 'net6.0'. [C:\Users\swyant\code\attempt-dotnet\src\Hello.sln]
C:\Users\swyant\code\attempt-dotnet\src\Hello.csproj : error NU1100: Unable to resolve 'Microsoft.AspNetCore.App.Runtime.win-x64 (= 6.0.0)' for 'net6.0'. [C:\Users\swyant\code\attempt-dotnet\src\Hello.sln]
  Failed to restore C:\Users\swyant\code\attempt-dotnet\src\Hello.csproj (in 141 ms).
```

I just installed the .NET 6.0 x64 this morning.  I don't have NuGet cli installed, was just planning on using the `dotnet` for package management.  Not sure if that's a factor here or not.

### References

- https://docs.microsoft.com/en-us/dotnet/core/deploying/single-file

- https://stackoverflow.com/q/60633397/7969520