# qpapeltools

this directory contains tools used to protect and pack the target executable after build.

## files

- `qPapelEasyAuth.dll`: core security engine (do not distribute to end users).
- `qPapelPacker.exe`: standalone packer that encrypts and embeds the dll into the target executable.
- `pack_release.bat`: convenience script to pack the release build.

## usage

1. build the project in `Release` configuration (`dotnet build -c Release`).
2. pack the generated executable:
```cmd
qPapelPacker.exe --dll qPapelEasyAuth.dll --input ..\bin\Release\net8.0\EasyAuth-CS-Example.exe --output ..\bin\Release\net8.0\EasyAuth-CS-Example_packed.exe
```
3. distribute only `EasyAuth-CS-Example_packed.exe`. you do not need to ship `qPapelEasyAuth.dll`; it is decrypted and mapped directly in memory at runtime.
