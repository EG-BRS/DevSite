# .Net core MVC QuickStart

Complete the steps described in the rest of this page to create a simple MVC application that makes requests to the Xena API.

## Prerequisites

To run this QuickStart, you need the following prerequisites:

* .Net core 2.0 or greater
* A Xena account with Xena developer plug-in installed.


## Step 1: Create an application


* Create an application in [Xena Developer](Fundamentals/CreateApplication.md)
* On the OAuth tab click "connect"
* Click the "create" button to create new client credentials.
* In your project page, create hybrid credentials.
* Give your credentials a name and description this will be displayed to the user on on the consent screen and should be descriptive of your application. 
* under grant type select "hybrid"
* click Create
* Under Redirect uri click manage and add http://localhost:8000/signin-oidc  (click the client id at the top to return to the client edit page)
* In the Post Logout Redirect URI click manage add https://localhost:8000/signout-callback-oidc (click the client id at the top to return to the client edit page)
* Under Secrets click manage leave settings as is and click create. Download the file and save it someplace secure. (click the client id at the top to return to the client edit page)
* Take note of the client ID in the resulting dialog. You need it in a later step.
* Click update 



## Step 2: Add settings

Open the appsettings.json file in your project add the following settings


```json
{
  "Xena": {
    "Authority": "https://login.xena.biz",
	"XenaAPIEndpoint": "https://my.xena.biz",
    "ClientId": "[Your Client id from step 1]",
    "ClientSecret": "[Your client secret from step 1]"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Warning"
    }
  },
  "AllowedHosts": "*"
}
```

## Step 3: Configure authentication 


In startup.cs add the following to your ConfigureServices method.

```csharp
public void ConfigureServices(IServiceCollection services)
        {
            ...            

            JwtSecurityTokenHandler.DefaultInboundClaimTypeMap.Clear();

            services.AddAuthentication(options =>
                {
                    options.DefaultScheme = "Cookies";
                    options.DefaultChallengeScheme = "oidc";
                })
                .AddCookie("Cookies")
                .AddOpenIdConnect("oidc", options =>
                {
                    options.SignInScheme = "Cookies";

                    options.Authority = Configuration["Xena:Authority"];
                    options.RequireHttpsMetadata = false;

                    options.ClientId = Configuration["Xena:ClientId"];
                    options.ClientSecret = Configuration["Xena:ClientSecret"];
                    options.ResponseType = "code id_token";

                    options.SaveTokens = true;
                    options.GetClaimsFromUserInfoEndpoint = true;

                    options.Scope.Add("testapi");
                    options.Scope.Add("offline_access");

                    options.ClaimActions.MapJsonKey("website", "website");
                });
        }


```

In startup.cs add app.UseAuthentication(); your Configure method as seen below.   

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            else
            {
                app.UseExceptionHandler("/Home/Error");
                app.UseHsts();
            }
            app.UseAuthentication();   //Xena: Add this line
            app.UseHttpsRedirection();
            app.UseStaticFiles();
            app.UseCookiePolicy();

            app.UseMvc(routes =>
            {
                routes.MapRoute(
                    name: "default",
                    template: "{controller=Home}/{action=Index}/{id?}");
            });
        }
```		

## Step 4: Create an authorized action in your controller.

Add the [Authorize] attribute to an action in your controller, this will tell MVC that your user must be authorized to access it. 


```csharp
[Authorize]
public IActionResult Xena()
    {
            ViewData["Message"] = "Secure page.";

            return View();
    }

```		


The view for this action should contain some JavaScript at the top which will ensure that this page opens in a new window and then closes after it has logged your user in.

>Note: You cant open the login in the plugin iFrame in Xena you will need to open this in a new window.  Then refresh the login.


```csharp
@using Microsoft.AspNetCore.Authentication
<script type="text/javascript">
    window.opener.location.href = window.location.href   
    close();
</script>
<h2>Claims</h2>

<dl>
    @foreach (var claim in User.Claims)
    {
        <dt>@claim.Type</dt>
        <dd>@claim.Value</dd>
    }
</dl>

<h2>Properties</h2>

<dl>
    @foreach (var prop in (await Context.AuthenticateAsync()).Properties.Items)
    {
        <dt>@prop.Key</dt>
        <dd>@prop.Value</dd>
    }
</dl>

```		


## Step 5: Run your application and it should now log into xena

You should now have your first Xena app 



