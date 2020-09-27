
# JWT
- Json web-token security
## Refresh Tokens
- The Need for Refresh Tokens?
  - So, why do we need both access tokens and refresh tokens? Why don’t we just set a long expiration date, like a month or a year for the access tokens? Because, if we do that and someone manages to get hold of our access token they can use it for a long period, even if we change our password!
  - The idea of refresh tokens is that we can make the access token short-lived so that, even if it is compromised, the attacker gets access only for a shorter period. With refresh token-based flow, the authentication server issues a one time use refresh token along with the access token. The app stores the refresh token safely.
  - Every time the app sends a request to the server it sends the access token in the Authorization header and the server can identify the app using it. Once the access token expires, the server will send a token expired response. Once the app receives the token expired response, it sends the expired access token and the refresh token to obtain a new access token and refresh token. 
  - If something goes wrong, **the refresh token can be revoked** which means that when the app tries to use it to get a new access token, that request will be rejected and the user will have to enter credentials once again and authenticate.
  - Thus, refresh tokens help in a smooth authentication workflow without the need for users to submit their credentials frequently, and at the same time, without compromising the security of the app.
## References
https://code-maze.com/using-refresh-tokens-in-asp-net-core-authentication/