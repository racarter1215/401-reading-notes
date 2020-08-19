# Facebook, Google, and external provider authentication in ASP.NET Core

### How to create a APS.NET Core Project:
##### Create new project.
##### Select ASP.NET Core Web Application.
##### Make project name and confirm or change location, then select create.
##### Select the latest version of .Net Core then select web application.
##### Select Change and set the authentication to Individual User Accounts. click ok
##### In the Create a new ASP.NET Core Web Application window, select Create.

##### How to add mltiple authentication providers:
services.AddAuthentication()
    .AddMicrosoftAccount(microsoftOptions => { ... })
    .AddGoogle(googleOptions => { ... })
    .AddTwitter(twitterOptions => { ... })
    .AddFacebook(facebookOptions => { ... });

### Authenticate with OAuth 2.0 in ASP.NET Core 2.0

##### Link to step by step instructions:
https://www.jerriepelser.com/blog/authenticate-oauth-aspnet-core-2/
