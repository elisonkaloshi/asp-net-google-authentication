# asp-net-google-authentication
### Documentation how to add external login in aspnet core

### Create project

1. Open Visual Studio 2022 and click on `create new project`

2. Select `ASP.NET Core Web App`

![alt text](images/create-project-type.png)

3. Give project details

![alt text](images/project-details.png)

4. Select framework to `.NET 6.0` and Authentication type to `Individual Accounts`

![alt text](images/individual-accounts.png)

### Add migrations

1. Open `Tools -> Nuget Packaget Manager -> Package Manager Console`

![alt text](images/nuget.png)

2. Add migration using the command: `add-migration <Name Of Migration>`

![alt text](images/add-migration.png)

3. Update database using the following command: `update-database`

![alt text](images/update-database.png)

4. To see the result navigate to Views -> `SQL Server Object Explorer`

![alt text](images/sql-server-object-explorer.png)

5. Find the database which is similar with the name of the project

![alt text](images/database.png)

### Add Google Authentication Package

1. Open `Tools -> Nuget Packaget Manager -> Package Manager Console`

![alt text](images/nuget.png)

2. Install Google Authentication package using this command: `Install-Package Microsoft.AspNetCore.Authentication.Google -Version 6.0.4`

![alt text](images/package.png)

### Add secret keys

1. Open `Tools -> Command Line -> Developer Command Prompt`

![alt text](images/cmd.png)

2. Init secret keys by using this command: `dotnet user-secrets init`

![alt text](images/init-secret-keys.png)


### Google Api
1. To get the credentials visit: `https://console.cloud.google.com/apis/credentials`


2. Click on the `CREATE PROJECT`

![alt text](images/create-project-google.png)

3. Add project details and `create` the project

![alt text](images/project-details-google.png)

4. Navigate to `Configure consent screen`

![alt text](images/configure-consent-screen.png)

5. Choose user type `(I have selected the Internal)`

![alt text](images/consent-screen-details.png)

6. Add your app details

![alt text](images/consent-screen-details-app.png)

7. Set your app domain information: `https://localhost:{port}`

![alt text](images/app-domain.png)

8. Add your developer information

![alt text](images/developer-info.png)


9. Navigate to `Credentials` and click on `CREATE CREDENTIALS` and select OAuth client ID

![alt text](images/create-credentials.png)

10. Select as an Application Type the `Web application` option

![alt text](images/application-type-credentials.png)

11. Add `Authorized Javascript origins` and `Authorized redirect URIs` and click `create`

![alt text](images/authorized-origins.png)

12. See your secret keys

![alt text](images/credentials.png)

### Add secret keys in the app

1. Open `Tools -> Command Line -> Developer Command Prompt`

![alt text](images/cmd.png)

2. Type the following commands:

`dotnet user-secrets set "Authentication:Google:ClientId" <Client Id thay you get from Google>`

![alt text](images/cmd-clientid.png)

`dotnet user-secrets set "Authentication:Google:ClientSecret" <Client Secret thay you get from Google>`

![alt text](images/cmd-clientsecret.png)

3. Edit Program.cs file and add the following content

```
var services = builder.Services;
var configuration = builder.Configuration;
 
services.AddAuthentication().AddGoogle(googleOptions =>
{
    googleOptions.ClientId = configuration["Authentication:Google:ClientId"];
    googleOptions.ClientSecret = configuration["Authentication:Google:ClientSecret"];
});

```

![alt text](images/edit-programcs.png)


### Run the app

`1. Click on green icon`

![alt text](images/run.png)

`2. Navigate to register and click on the Google button`

![alt text](images/external-in-register.png)

3. Choose account

![alt text](images/choose-account.png)

4. Click on register

![alt text](images/give-email.png)

5. Click on: `Click here to confirm your account`

![alt text](images/confirm-your-account.png)

6. Navigate to login and click on `Google`

![alt text](images/navigate-login.png)

7. You will be automatically logged in 

![alt text](images/logged-in.png)






