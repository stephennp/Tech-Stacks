
# JWT
- Json web-token security
# Refresh Tokens
- The Need for Refresh Tokens?
  - So, why do we need both access tokens and refresh tokens? Why don’t we just set a long expiration date, like a month or a year for the access tokens? Because, if we do that and someone manages to get hold of our access token they can use it for a long period, even if we change our password!
  - The idea of refresh tokens is that we can make the access token short-lived so that, even if it is compromised, the attacker gets access only for a shorter period. With refresh token-based flow, the authentication server issues a one time use refresh token along with the access token. The app stores the refresh token safely.
  - Every time the app sends a request to the server it sends the access token in the Authorization header and the server can identify the app using it. Once the access token expires, the server will send a token expired response. Once the app receives the token expired response, it sends the expired access token and the refresh token to obtain a new access token and refresh token. 
  - If something goes wrong, **the refresh token can be revoked** which means that when the app tries to use it to get a new access token, that request will be rejected and the user will have to enter credentials once again and authenticate.
  - Thus, refresh tokens help in a smooth authentication workflow without the need for users to submit their credentials frequently, and at the same time, without compromising the security of the app.
## References
https://code-maze.com/using-refresh-tokens-in-asp-net-core-authentication/
# JWT VS Session VS Cookie for ASP.NET Core Web Api

## JWT vs Session certification
- **Session**: When a user logs in to the application system, the server creates a Session (also known as a session), and the SessionId is saved in the user's cookie. As long as the user is logged in, the SessionId in the cookie is sent to the server for each request, and the server saves it in theSessionId in memory is compared with SessionId in Cookie to authenticate the user and respond.

- **JWT**: When a user logs in to the application system, the server creates a JWT and sends it to the client, which stores the JWT (typically in Local Storage) and also contains the JWT in each request header, Authorization For each request, the server verifies that the JWT is legal and directly in the service.End-to-end local authentication, such as issuers, acceptors, and so on, eliminates the need to make network requests or interact with the database, which may be faster than using Session, thereby increasing response performance and reducing server and database server load.
- From the brief description of JWT authentication and Session authentication above, we know that the biggest difference between them is that Session is stored on the `server side` and JWT is stored on the `client side`.
- There are two kinds of server-side storage sessions, one is to store `session` identifiers in the `database`, the other is to store session in `memory`. I think most of the time it is based on memory to maintain session, but this will bring some problems. If there is a large amount of traffic on the system, that is, if there are a large number of users accessing the systemUse of memory-based maintenance sessions limits horizontal expansion at this time, but there is no such problem with Token-based authentication, and cookies generally only apply to single or subdomains. For cross-domain, if it is a third-party Cookie, the browser may disable cookies, so it is also restricted by the browser, but for TokenAuthentication is not a problem because it is saved in the request header.
## Reference
- https://programming.vip/docs/jwt-vs-session-vs-cookie-for-asp.net-core-web-api.html
