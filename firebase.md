# Intro

# FCM (Firebase cloud message)

## Foreground & Background
- **Foreground** refers to the active apps which consume data and are currently running on the mobile.
- **Background** refers to the data used when the app is doing some activity in the background, which is not active right now.

This is due to the fact that whether they are active or not, apps consume data. They may be

checking for updates or refreshing the user content
running ads in the background
sending notifications
## Message Types
- **Notification** messages, sometimes thought of as "display messages." These are handled by the FCM SDK automatically.
- **Data** messages, which are handled by the client app.
- Maximum payload for both message types is `4KB`, except when sending messages from the Firebase console, which enforces a 1024 character limit.

## Topic vs Tokens
- When you use **topics**, you separate the sending of messages about a topic, from the fact that an install of your app subscribes to that topic. This means you can add subscribers to the topic later, without having to write additional code or even data (as the list of tokens that are subscribed to a topic is handled by FCM itself).
- On the other hand: topics are `public`. Once somebody knows the topic ID, they can subscribe to that topic, and receive any messages you send to that topic.
- The alternative to using topics is sending messages directly to FCM Instance ID tokens. In that case you'll keep a list of tokens somewhere yourself, and determine what token(s) to deliver the message to. In this case, you fully control who receives the message, but will have to maintain your own list of tokens, and the mapping of what token receives what message(s).

- **Note** that sending messages (no matter whether to topics or to tokens) can be done from any trusted environment, like your development machine, a server you control, or Cloud Functions. And sending messages (no matter whether to topics or to tokens) can't be (securely) done from the client-side code.
## Reference:
- https://firebase.google.com/docs/cloud-messaging/android/receive
- https://medium.com/@anum.amin/react-native-integrating-push-notifications-using-fcm-349fff071591
- https://hiranya911.medium.com/firebase-introducing-the-cloud-messaging-batch-apis-in-the-admin-sdk-2a3443c412d3
# Cloud Firestore

# Realtime Database

# Hosting

# Cloud Storage

# Authentication
