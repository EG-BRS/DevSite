# .Net core MVC QuickStart

Complete the steps described in the rest of this page to create a simple MVC application that makes requests to the Xena API.

## Prerequisites

To run this QuickStart, you need the following prerequisites:

* .Net core 2.0 or greater
* A Xena account with Xena developer plug-in installed.


## Step 1: Create an application


* Create an application in Xena Developer 
* On the Oauth tab click "connect"
* Click the "create" button to create new client credentials.
* in your project page, create hybrid credentials.
* Give your credentials a name and description this will be displayed to the user on on the consent screen and should be descriptive of your application. 
* under grant type select "hybrid"
* click Create
* Under Redirect uri click manage and add http://localhost:8000/signin-oidc  (click the client id at the top to return to the client edit page)
* In the Post Logout Redirect URI click manage add https://localhost:8000/signout-callback-oidc (click the client id at the top to return to the client edit page)
* Under Secrets click manage leave settings as is and click create. Download the file and save it someplace secure. (click the client id at the top to return to the client edit page)
* Take note of the client ID in the resulting dialog. You need it in a later step.
* Click update 



## Step 2: Set up the sample


In startup.cs  add the following to your ConfigureServices method.

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