# Okta React + Okta Hosted Login Example

This example shows how to use the [Okta React Library][] and [React Router](https://github.com/ReactTraining/react-router) to login a user to a React application.  The login is achieved through the [PKCE Flow][], where the user is redirected to the Okta-Hosted login page.  After the user authenticates they are redirected back to the application with an ID token and access token.

## Prerequisites

Before you begin, you’ll need an Okta Integrator Free Plan account. To get one, sign up for an [Integrator account](https://developer.okta.com/login). Once you have an account, sign in to your [Integrator account](https://developer.okta.com/login). Next, in the Admin Console:

1. Go to **Applications > Applications**
2. Click **Create App Integration**
3. Select **OIDC - OpenID Connect** as the sign-in method
4. Select **Single-Page Application** as the application type, then click **Next**
5. Enter an app integration name
6. In the **Grant type** section, ensure both **Authorization Code** and **Refresh Token** are selected
7. Configure the redirect URIs:
  - **Sign-in redirect URIs:** `http://localhost:3000/callback`
  - **Sign-out redirect URIs:** `http://localhost:3000`
8. In the **Controlled access** section, select the appropriate access level
9. Click **Save**

### Where are my new app's credentials?

Creating an OIDC Single-Page App manually in the Admin Console configures your Okta Org with the application settings. You may also need to configure trusted origins for `http://localhost:3000` in **Security > API > Trusted Origins**.

After creating the app, you can find the configuration details on the app’s **General** tab:
- **Client ID**: Found in the **Client Credentials** section
- **Issuer**: Found in the **Issuer URI** field for the authorization server that appears by selecting **Security > API** from the navigation pane.

```text
Issuer:    https://dev-133337.okta.com
Client ID: 0oab8eb55Kb9jdMIr5d6
```

## Configure Okta resources

**Enable Refresh Tokens**

Sign into your [Okta Developer Edition account](https://developer.okta.com/login/) to add a required setting to your React Okta app to avoid third-party cookies. Navigate to **Applications** > **Applications** and select "okta-react-sample" application to edit. Find the **General Settings** and press **Edit**. Enable **Refresh Token** in the **Grant type** section. **Save** your changes.

**Verify Authorization Server**

This repo calls a custom resource server to demonstrate making a protected resource request using an access token. Ensure that your default custom authorization server has an access policy. Add an access policy if it's not there. See [Create access polices](https://help.okta.com/okta_help.htm?type=oie&id=ext-create-access-policies).

## Get the Code

Grab and configure this project using `okta start react`.

Follow the instructions printed to the console.

## Run the Example

To run this application, install its dependencies:

```
npm ci
```

With variables set, start your app:

```
npm start
```

Navigate to http://localhost:3000 in your browser.

If you see a home page that prompts you to login, then things are working!  Clicking the **Log in** button will redirect you to the Okta hosted sign-in page.

You can sign in with the same account that you created when signing up for your Developer Org, or you can use a known username and password from your Okta Directory.

> **Note:** If you are currently using your Developer Console, you already have a Single Sign-On (SSO) session for your Org.  You will be automatically logged into your application as the same user that is using the Developer Console.  You may want to use an incognito tab to test the flow from a blank slate.

## Integrating The Resource Server

If you were able to successfully login in the previous section you can continue with the resource server example. Please download and run one of these sample applications in another terminal:

* [Node/Express Resource Server Example](https://github.com/okta/samples-nodejs-express-4/tree/master/resource-server)
* [Java/Spring MVC Resource Server Example](https://github.com/okta/samples-java-spring/tree/master/resource-server)
* [ASP.NET](https://github.com/okta/samples-aspnet/tree/master/resource-server) and [ASP.NET Core](https://github.com/okta/samples-aspnetcore/tree/master/samples-aspnetcore-3x/resource-server) Resource Server Examples

Once you have the resource server running (it will run on port 8000) you can visit the `/messages` page within the React application to see the authentication flow. The React application will use its stored access token to authenticate itself with the resource server, you will see this as the `Authorization: Bearer <access_token>` header on the request if you inspect the network traffic in your browser.

[Okta React Library]: https://github.com/okta/okta-react
[OIDC SPA Setup Instructions]: https://developer.okta.com/docs/guides/sign-into-spa/react/before-you-begin
[PKCE Flow]: https://developer.okta.com/docs/guides/implement-auth-code-pkce
[Okta Sign In Widget]: https://github.com/okta/okta-signin-widget
