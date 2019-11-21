---
description: Essentials on OAuth integration.
---

# Using OAuth

{% hint style="info" %}
See [Identity.Server.Sample.Dotnet](https://github.com/EG-BRS/Identity.Server.Sample.Dotnet/tree/master/) for a sample project.
{% endhint %}

Please refer to the github repository for the code in its entirety. This sample is written in C\# .NET core 2 and can be run via Docker.

First off we need to add the OpenId middleware to authentication configuration in `startup.cs`:

{% code title="startup.cs" %}
```csharp
 .AddOpenIdConnect(AuthenticationConstants.XenaOidcAuthenticationScheme, options =>
    {
        options.SignInScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        options.ResponseType = AuthenticationConstants.OidcResponseType;

        options.SignedOutRedirectUri = "/Home/LogoutRedirect";

        options.Authority = authConfiguration.Authority;
        options.ClientId = authConfiguration.ClientId;
        options.ClientSecret = authConfiguration.ClientSecret;

        options.SaveTokens = true;
        options.RequireHttpsMetadata = false;
        options.GetClaimsFromUserInfoEndpoint = true;

        options.Scope.Add("profile"); 
        options.Scope.Add("testapi");
        options.Scope.Add("offline_access");

        options.ClaimActions.MapJsonKey(JwtClaimTypes.PreferredUserName, JwtClaimTypes.PreferredUserName);
    }
```
{% endcode %}

All the configuration is set in `appsettings.Development.json`

When user hit any method/controller with `[Authorize]` attribute he will be forced to authenticate. In our examples default challenge scheme is Xena. The user will be transfered to login page and after correct login will return to your app with tokens.

To communicate with the Xena API you will need to send access\_token with each call in headers.

Application `access_token` lifetime is set to 60 minutes but cookie for your app can be different. For better user experience the app can use `refresh_token` to get new `access_tokens`.

In the sample we use automatic silent renew middleware that checks and refreshes the token if needed with each call.

## API call

In sample in `XenaService.cs` we show three API calls. The user can get data about his fiscal, Xena membership and apps that he is subscribed to.

{% code title="XenaService.cs" %}
```csharp
[Authorize]
public async Task<IActionResult> ApiExample()
{
    HttpClient client = await SetupClientWithToken();
    var result = await client.GetStringAsync($"{_apiEndpoints.Xena}/User/FiscalSetup?forceNoPaging=true");
    return result;
}
```
{% endcode %}

