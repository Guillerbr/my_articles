# Useful for you, consider buying me a coffee. Thanks!

ETH:
0xdfaf8F1bCaaB513A14E5a0B8C2D0bF7EE6ECabbc 

<a href="https://www.bitcoinqrcodemaker.com"><img src="https://www.bitcoinqrcodemaker.com/api/?style=ethereum&amp;address=0xdfaf8F1bCaaB513A14E5a0B8C2D0bF7EE6ECabbc" alt="Ethereum QR Code Generator" height="300" width="300" border="0" /></a>

# Overview
The purpose of this article is to present, discuss, and provide specific mitigation techniques on user authentication and session best practices using *Cookies, Http Only, JWT, Session, LocalStorage, and other methods.*

## Http cookies
An HTTP cookie (a web cookie or browser cookie) is a small piece of data that a server sends to a user's browser. The browser can store this data and send it back on the next request to the same server. It is usually used to identify whether two requests came from the same browser — when keeping a user logged in, for example. It stores dynamic information for the stateless HTTP protocol.

#### Cookies are mainly used for three purposes:


##### Session Management:
Logins, shopping carts, game scores or any other activity that must be kept by a server.

##### Customization:
User preferences, themes and other settings.

##### Tracking:
Recording and analyzing a user's behavior.

- We can set the expiration time for each cookie

- The 4K limit is for the entire cookie, including name, value, expiration date, etc. To support most browsers, keep the name below 4000 bytes and the overall cookie size below 4093 bytes.

- Data is sent back to the server for each HTTP request (HTML, images, JavaScript, CSS, etc) — increasing the amount of traffic between the client and the server.

## Http Only

![Alt ​​Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/oqh0wmupnkvrq8vp8ig8.png)

#### What is HttpOnly?
According to the Microsoft Developer Network, HttpOnly is an additional flag included in an HTTP Set-Cookie response header. Using the HttpOnly flag when generating a cookie helps mitigate the risk of client-side script accessing the protected cookie (if the browser supports it).

To prevent cross-site scripting (XSS) attacks, *HttpOnly* cookies are inaccessible to the Document.cookie JavaScript API (en-US); they are sent only to the server. For example, cookies that persist server sessions do not need to be available to JavaScript, so the *HttpOnly* directive must be set.

```bash
_Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT; Secure; HttpOnly_
```

A *HttpOnly* cookie is a tag added to a browser cookie that prevents client-side scripts from accessing the data. It provides a port that prevents the specialized cookie from being accessed by anything other than the server. Using the HttpOnly tag when generating a cookie helps reduce the risk of client-side scripts accessing the protected cookie, making those cookies more secure.

##### The example below shows the syntax used in the HTTP response header:

```bash
Set-Cookie: `=“[; “=“]` `[; expires=“][; domain=“]` `[; path=“][; secure][; HttpOnly]`
```

If the **HttpOnly flag is included in the HTTP response header, the cookie cannot be accessed via client-side script.** As a result, even if there is a cross-site scripting (XSS) failure and a user accesses accidentally a link that exploits the flaw, the browser will not reveal the cookie to third parties.

Here's an example - let's say a browser detects a cookie containing the *HttpOnly* flag. If client-side code tries to read the cookie, the browser will return an empty string as a result. This helps *prevent malicious code (usually cross-site scripting (XSS))* from sending data to an attacker's website.


## JWT

![Alt ​​Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bjpz9k516q6cxhps8xo0.png)

#### User authentication using the mechanism called JWT (JSON Web Token)

Authentication strategy for simple and secure REST APIs. It is an open standard for web authentication and is based entirely on JSON requests between the client and server. Its authentication mechanism works as follows:

- The client makes a one-time request when sending the login and password credentials;

- The server validates the credentials and, if everything is correct, it returns to the client a JSON with a token that encodes data from a user logged into the system;

- After receiving the token, the client can store it in the way they prefer, either by LocalStorage, SessionStorage, Cookies and HTTP Only or other client-side storage mechanisms;

- Every time the client accesses a route that requires authentication, it just sends this token to the API to authenticate and release the consumption data;

- The server always validates this token to allow or block a client request.

###### JWT (JSON Web Token) is an industry-standard RCT 7519 method for performing authentication between two parties via a signed token that authenticates a web request. This token is a Base64 code that stores JSON objects with the data s that allow authentication of the request.

With a secure *token* built in, it is mathematically impossible to decode the signature without having the application's key secret. However, once in possession of the secret, any application can decode the signature and verify that it is valid. This is done by generating a *signature* using the header and *payload* provided by the client, and then we compare this *signature* generated with the one present in the *token* sent by the client. Once the signatures are identical, we can allow the client access to a restricted area of ​​our application.

https://jwt.io/

## SessionStorage and LocalStorage

#### SessionStorage

- **sessionStorage** is similar to localStorage , the only difference is that while the data stored in **localStorage does not expire, the data in sessionstorage has its data cleared when the page session expires.** The page session it lasts while the browser is open and keeps on reloading the page.


- Web storage can be simplistically seen as an improvement over cookies, offering much greater storage capacity. The available size is 5MB, which is considerably more space to work with than a typical 4KB cookie.


- Data is not sent back to the server for each HTTP request (HTML, images, JavaScript, CSS, etc) — reducing the amount of traffic between the client and the server.


- Data stored in localStorage persists until explicitly deleted. Changes made are saved and available for all current and future visits to the site.

- Works on same-origin policy. Therefore, stored data will only be available from the same source.


#### LocalStorage

Use *localStorage* to store temporary variables.

It is similar to localStorage.

- Changes are only available per window (or in browsers like Chrome and Firefox). Changes made are saved and made available for the current page as well as future visits to the site in the same window. Once the window is closed, the storage is deleted

- Data is only available within the window/tab in which it was defined.

- Data is not persistent, i.e. it will be lost when the window/tab is closed. Like localStorage, it works on the same origin policy. Therefore, stored data will only be available from the same source.

##### Local and Session Storage Considerations

Both *localStorage and sessionStorage* extend from *Storage*. There is no difference between them, except for the non-persistence of *sessionStorage*.

The non-persistence as described above is in the sense that *sessionStorage* is only available for the window that created the data until that window is closed, when opening another window (or tab) such data will not be available.

In contrast to *sessionStorage*, when creating data in *localStorage* this data will be available for any tab/window even if the user closes the window, restarts the system, etc.

For example, assuming you want to save the username and password to log in, you might choose to store this data in sessionStorage for security reasons and save the user settings in localStorage.



# Real World Application

Store a user token. In this step, you will store the user token. You will implement different *token* storage options and learn the security implications of each approach. Finally, you'll learn how different approaches will change the user experience as they open new tabs or close a session.

At the end of this step, you can choose a storage approach based on your application's goals.

There are several options for storing *tokens*. Each option has costs and benefits. Briefly, the options are: store in memory *JavaScript*, store *sessionStorage*, store *localStorage* and store in a cookie. The main tradeoff is security. Any information stored outside of the current application's memory is *vulnerable to Cross-Site Scripting (XSS)* attacks.

*The danger is that if a malicious user is able to load code into your application, they can access localStorage, sessionStorage, and any cookies that are also accessible to your application*.

- The benefit of memoryless storage methods is that you can reduce the number of times a user will need to log in to create a better user experience.

##### This tutorial will cover *sessionStorage, localStorage, Cookies and HTTP Only* as these are more modern.

- Session Storage
To test the benefits of out-of-memory storage, convert in-memory storage to *sessionStorage*. Open App.js:

# Using ReactJs frontend client for user interfaces.

- You must have basic and intermediate knowledge about *ReactJs* for cunderstand more easily the deployment of a *secure* and *modern* authentication service, widely recommended and used by the *open source community* to authenticate a user to a web system.

## What are the vulnerabilities?
Both methods come with potential related security issues:

##Vulnerability Method
XSS local storage - cross-site scripting
CSRF Cookies - Cross-Site Request Forgery

An XSS vulnerability allows an attacker to inject JavaScript into a website.
A CSRF vulnerability allows an attacker to take actions on a website through an authenticated user.

## How can I get around this?
If local storage can be exploited by third-party scripts (such as those found in browser extensions) and if authentication can be spoofed with cookies, where is it acceptable to put client state?

In single page app authentication using cookies in Auth0 docs, we learned that if your app:

- It is served to the customer using its own backend
- Has the same domain as your backend
- Makes API calls that require authentication to your backend
- So there is a way to use cookies for authentication securely.


# UNDER DEVELOPMENT AND CONSTRUCTION




*Links and References:*

https://owasp.org/www-community/HttpOnly

https://medium.com/@ryanchenkie_40935/react-authentication-how-to-store-jwt-in-a-cookie-346519310e81

https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Cookies

https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API

https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API

https://developer.mozilla.org/pt-BR/docs/Web/API/Window/sessionStorage

https://www.taniarascia.com/full-stack-cookies-localstorage-react-express/



