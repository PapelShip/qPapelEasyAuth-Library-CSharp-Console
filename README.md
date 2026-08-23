# easyauth c# sdk & example

c# client wrapper and example console application for the qpapel easyauth system.

## requirements

- .net sdk 8.0 or later
- windows x64

## structure

- `qPapelLibCsharp/`: c# wrapper library (.net standard 2.0 / .net 8 / .net 9 compatible nuget package).
- `EasyAuth-CS-Example/`: example application with automated post-build packer integration.
- `qPapelTools/`: native core dll and pe section packer tool.

## usage

```csharp
using qPapelEasyAuth;

// 1. initialize in-memory pe engine
qPapelEasyAuth.Initialize();

// 2. configure
qPapelEasyAuth.SetConfig(new EasyAuthConfig
{
    DefaultApiKey = "pk_00000073_0c492fbfaad6c9ff99a9a3b8da76c8c4",
    ClientVersion = "2.0.0",
    WatchdogIntervalMs = 500
});

// 3. connect and authenticate
if (qPapelEasyAuth.Connect())
{
    var session = qPapelEasyAuth.InitSession();
    var auth = qPapelEasyAuth.Authenticate("USER_LICENSE_KEY");
    if (auth.Success)
    {
        Console.WriteLine($"auth success: {auth.ExpireDate}");
        string val = qPapelEasyAuth.GetVariable("var_id");
    }
}
```

## build and distribution

build the project in release mode:

```cmd
dotnet build -c Release
```

distribute only the `EasyAuth-CS-Example_packed.exe` generated in `bin/Release/net8.0/`. no external dll files are required.
