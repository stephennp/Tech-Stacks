# Intro
- https://docs.microsoft.com/en-us/aspnet/signalr/overview/getting-started/introduction-to-signalr
## Users in SignalR
- A single user in SignalR can have multiple connections to an app. For example, a user could be connected on their desktop as well as their phone. Each device has a separate SignalR connection, but they're all associated with the same user.
- If a message is sent to the user, all of the connections associated with that user receive the message. The `user identifier` for a connection can be accessed by the `Context.UserIdentifier` property in the hub.
- `System.Security.Claims.ClaimTypes.NameIdentifier` can get from `sub claim` of a JWT access token and also on [Authorize] attribute in a given route 

## Authenticate users connecting to a SignalR hub
### Bearer token authentication

- The client can provide an access token instead of using a cookie. The server validates the token and uses it to identify the user.
- This validation is done only when the connection is established. During the life of the connection, the server doesn't automatically revalidate to check for token revocation.
- In the JavaScript client, the token can be provided using the accessTokenFactory option.
```typescript
// Connect, using the token we got.
this.connection = new signalR.HubConnectionBuilder()
    .withUrl("/hubs/chat", { accessTokenFactory: () => this.loginToken })
    .build();
```
- Note
 - The access token function you provide is called before every HTTP request made by SignalR
 - . If you need to renew the token in order to keep the connection active (because it may expire during the connection), do so from within this function and return the updated token.
## Performance
### 1. Reducing message size

### 2. Throttling message frequency
- Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second. To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent). For a sample application that throttles messages to a certain rate (from both client and server)

### 3. SignalR configuration settings

- `DefaultMessageBufferSize`: By default, SignalR retains 1000 messages in memory per hub per connection. If large messages are being used, this may create memory issues which can be alleviated by reducing this value.
- `Max concurrent requests per application`: Increasing the number of concurrent IIS requests will increase server resources available for serving requests. The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:
- `ApplicationPool QueueLength`: This is the maximum number of requests that Http.sys queues for the application pool. When the queue is full, new requests receive a 503 "Service Unavailable" response. The default value is 1000.

## Security considerations
- https://docs.microsoft.com/en-us/aspnet/core/signalr/security?view=aspnetcore-3.1
## References:
- https://docs.microsoft.com/en-us/aspnet/core/signalr/authn-and-authz?view=aspnetcore-3.1#use-claims-to-customize-identity-handling
- https://docs.microsoft.com/en-us/aspnet/core/signalr/groups?view=aspnetcore-3.1