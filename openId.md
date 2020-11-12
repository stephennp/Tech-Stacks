# Intro

## How to get the user identifier in an ASP.NET Core API?
- When you do the above and include the [Authorize] attribute in a given route the information contained in the received access token will be mapped to a claims principal that you can access at your route method through the use of this.User.

- By default the `JWT authentication handler` in .NET will map the `sub claim` of a JWT access token to the `System.Security.Claims.ClaimTypes.NameIdentifier` claim type

## Openidict
- https://kevinchalet.com/2017/01/30/implementing-simple-token-authentication-in-aspnet-core-with-openiddict/