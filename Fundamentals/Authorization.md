

# About Authorization

Every request your application sends to the Xena API must include an authorization token. The token also identifies your application to Xena.

# About authorization protocols

Your application must use OAuth 2.0 to authorize requests. No other authorization protocols are supported.

## Authorizing requests with OAuth 2.0

All requests to the Xena API must be authorized by an authenticated user.

The details of the authorization process, or "flow," for OAuth 2.0 vary somewhat depending on what kind of application you're writing. 

The following general process applies to all application types:

1. When you create your application, you register it in Xena developer and using the Xena Developer Console. Xena's Identity server then provides information you'll need later, such as a client ID and a client secret.
2. When your application needs access to user data, it asks Xena's Identity server for a particular scope of access. (see: scopes below)
3. Xena's Identity server then displays a consent screen to the user, asking them to authorize your application to access some of their data.
4. If the user approves your reuqest, then Xena's Identity server returns to your application a short-lived access token. Access tokens granted by the Xena's Identity server are valid for one hour.
5. Your application requests user data, attaching the access token to the request. All your requests to the Xena api should submit an authorization header bearer token.
6. If Xena's api determines that your request and the token are valid, it returns the requested data.
7. Some flows include additional steps, such as using refresh tokens to acquire new access tokens. For detailed information about flows for various types of applications, see [Xena's OAuth 2.0 documentation](Oauth2hybrid).

Here's the OAuth 2.0 scope information for the Xena API:

- testapi - Access to the Xena API

Standard identtiy scopes

- profile - User profile information not email
- email   - users email
- offline_access - returns refresh token.


| Scope          | Meaning |
| -------------  | ------------- |
| testapi        | Full, permissive scope to access all of a user's Xena data.  |
| profile        | users profile information,  name, culture, picture  |
| email          | users email  |
| offline_access | returns a refresh token  |


## Service account

The Xena identity server does support a method for server to server interaction.  We call this service accounts.  Service accounts are pre-authorized in the backend on the identity server.  This means that service accounts allow you to impersonate a single user without the need for consent authorization.  Currently the Last developer console does not allow you to create your own service account.  You can contact us and we would be happy discuss creating one for your appication.
