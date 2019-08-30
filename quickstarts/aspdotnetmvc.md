# Asp .Net MVC QuickStart

Complete the steps described in the rest of this page to create a simple MVC application that makes requests to the Xena API.

## Prerequisites

To run this QuickStart, you need the following prerequisites:

* .Net core 2.0 or greater
* A Xena account with Xena developer plug-in installed.

## Step 1: Create an application

* Create an application in [Xena Developer](https://github.com/EG-BRS/DevSite/tree/f65f6a98fe6cbdc3a44942a454484f130a4dc012/QuickStarts/Fundamentals/CreateApplication.md)
* On the OAuth tab click "connect"
* Click the "create" button to create new client credentials.
* In your project page, create hybrid credentials.
* Give your credentials a name and description this will be displayed to the user on on the consent screen and should be descriptive of your application. 
* under grant type select "hybrid"
* click Create
* Under Redirect uri click manage and add [http://localhost:8000/signin-oidc](http://localhost:8000/signin-oidc)  \(click the client id at the top to return to the client edit page\)
* In the Post Logout Redirect URI click manage add [https://localhost:8000/signout-callback-oidc](https://localhost:8000/signout-callback-oidc) \(click the client id at the top to return to the client edit page\)
* Under Secrets click manage leave settings as is and click create. Download the file and save it someplace secure. \(click the client id at the top to return to the client edit page\)
* Take note of the client ID in the resulting dialog. You need it in a later step.
* Click update 

