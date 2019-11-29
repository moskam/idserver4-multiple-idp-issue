# idserver4-multiple-idp-issue

To run project, run in PowerShell:
```
dotnet build;

Start-Process -NoNewWindow dotnet -Args 'run --project .\src\IdentityServer\IdentityServer.csproj';
Start-Process -NoNewWindow dotnet -Args 'run --project .\src\JsAuthCode\JsAuthCode.csproj';
Start-Process -NoNewWindow dotnet -Args 'run --project .\src\JsAuthCodeGoogle\JsAuthCodeGoogle.csproj';

start-process http://localhost:5002;
start-process http://localhost:5003;
```

We used .NET Core SDK version 2.2.203 with VS 2019, if needed, SDK version can be changed in global.json file.

### Steps to reproduce logout issue
1. Run application
2. Open, in the same browser in different tabs, client website (tested in Chrome):
  - http://localhost:5002
  - http://localhost:5003
3. On both tabs open dev tools (F12)
4. Login to first website using identity server demo provider, use suggested credentials (eg. bob/bob)
	![Logged In Imange](https://raw.githubusercontent.com/moskam/idserver4-multiple-idp-issue/master/images/01_first_logged_in.png "Logged in image")
5. Copy value of `idsrv.session` cookie
6. Switch to other tab and login using any Google account
7. Look at value of that cookie `idsrv.session`, it was overwritten with new value.
	![Logged In Imange](https://raw.githubusercontent.com/moskam/idserver4-multiple-idp-issue/master/images/02_first_after_google_login.png "After seconfg gogged in image")
8. Go back to first tab and logout from website. The result is that you've been logged out from second client session from other tab.
9. Try to login again on first tab, you will be logged in automatically, without prompting for credentials again.
10. To compare, logout again from first tab, right after log in. Then try to login again, you will be prompted to give credentials again.
