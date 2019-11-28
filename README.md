# idserver4-multiple-idp-issue

To run project, run in PowerShell:
```
dotnet build;

Start-Process -NoNewWindow dotnet -Args 'run --project .\src\IdentityServer\IdentityServer.csproj';
Start-Process -NoNewWindow dotnet -Args 'run --project .\src\JsAuthCode\JsAuthCode.csproj';
Start-Process -NoNewWindow dotnet -Args 'run --project .\src\JsAuthCodeGoogle\JsAuthCodeGoogle.csproj';
```
