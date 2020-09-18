# Azure service Bus

## Info

### What is Service Bus

- Service Bus is the second message queuing platform build by Azure that provides **Relay and Brokered** messaging capabilities

### Service Bus vs. Queue Storage

- Service Bus Queue would be the best chose If you:
  - You would like to be able to publish and consume **batches of messages**
  - Can be used when the application must **receive messages without polling the queue**.
  - Implicitly enabling a **pre-fetch** property or explicitly through the use of transactions
  - You want to use the **AMQP 1.0** standards-based messaging protocol
  - The maximum message size of Service Bus messages is 256 KB in Standard Tier and 1 MB in Premium Tier. The maximum size of the message header is 64 KB
  - Your queue size will not grow larger than **80 GB**
  - Provide a guaranteed **first-in-first-out (FIFO)** ordered delivery
  - Support automatic **duplicate detection**
  - Requires **transactional behavior** and atomicity when sending or receiving multiple messages from a queue
  - Atomic operation support
  - A maximum of **10,000 queues**
  - **Session** Handling
  - **Dead lettering** which is only supported by Service Bus queues:
    - Messages sent to session enabled queue without session id will be dead-lettered
    - Messages that are received **beyond the provided max delivery count** of the queue will be dead-lettered
    - Messages with header size more than 64KB will be dead-lettered.

- Queue Storage would be the best chose If you:
  - **Failure Handling** > If the application requires load balancing, failure tolerance, and increased scalability then Azure Storage Queues are the best choice.
  - Provide logging of all the occurred transactions
  - Delivery guarantee **At-Least-Once**
  - Needs to retain more than **80 GB of data** in queue
  - Message time to live **less** than 7 days
  - The ability to **track** message processing within a **queue**
  - Batched receive: yes, Explicitly specifying message count when retrieving messages, up to a maximum of 32 messages
  - Batched send: no
  - Scalability better than Service Bus that can store up 200 TB of messages, unlimited number of queues
  - The maximum message size in Storage Queues is 64 KB. If the messages are base64 encoded, then the maximum message size is 48 KB. Large message sizes are supported by combining queues with blobs, through which messages up to 200 GB can be enqueued as single data
- More info here : <https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted>

### Message Info

- A message at its heart is made up of a body and properties
- The total max size of a message is **256kb**
- The max size of all properties is **64kb**

## Sending Messages

- There are only 2 options:
  - QueueClient
  - MessageSender (is also an abstraction for the QueueClient )
- We will get the benefits of utilizing the MessageSender over a QueueClient when we use **Topics** Sender mode.

## Receiving Messages

- **Default mode** of the Queue where messages received are received in a **PeekLock** mode
- We have ***Received Delay** property to wait up a specific time to pulled from the azure message queue.
- Upon successfully pulling a message, the message is processed and then we explicitly notifying Azure Service Bus with the state of the message by calling **CompleteAsync or AbandonAsync**
- There are 2 modes of message retrieval:

  - PeekLock Mode
    - Specifies that a message is only temporarily checked out for **some duration of time** to be processed.  Unless the message is checked in as **complete** will it be removed from the queue.
    - There are other consequences that would directly affect a message being removed from the queue such as time to live setting of the queue or message.
    - But as far as message handling by our receiver, we will need to **complete, abandon or dead-letter** the message.
  - ReceiveAndDelete Mode

### Prefetching

- Fetching messages from a Queue or Subscription have been per call and incur the cost of a round trip to Azure for each request
- Imagine preloading messages to a local cache to your client when you make request for a single message and all subsequent message requests for another message pulls from the local cache until you run out of messages in the local cache.  This is roughly what you are setting up when enabling Prefetching.
- The PrefetchCount count is not an arbitrary number but should be calculated based on Microsoft recommended formula (as a starting point).  The formula is 20x the total number of messages that a single receiver can process per second.  So if a receiver can process 5 messages/sec = 20×5 = 100 PrefetchCount
- The number should be multiplied by the number of clients being created by the factory
- Something to be very aware of, there is a default of 60 second lock duration per message at the server which can be extended up to 5 minutes. If a message is not processed before it hits the expiration it will be made available on the server for another client to process.  However, the client who has cached that message will not know this and will receive the message (from local cache) and will receive an exception if attempting to process after the message’s Time-To-Live has expired.
- Example:
  - Receiving time in milliseconds for 3 messages without Prefetching:
- ReceiveAndDelete Mode:
  - With the ReceiveAndDelete receive mode, all messages that are acquired into the prefetch buffer are no longer available in the queue, and **only reside in the in-memory prefetch buffer** until they are received into the application through the **Receive/ReceiveAsync or OnMessage/OnMessageAsync** APIs. If the application terminates before the messages are received into the application, those messages are irrecoverably lost.
- PeekLock Mode:
  - In the PeekLock receive mode, messages fetched into the Prefetch buffer are acquired into the buffer in a locked state, and have the timeout clock for the lock ticking. If the prefetch buffer is large, and processing takes so long that message locks expire while residing in the prefetch buffer or even while the application is processing the message, there might be some confusing events for the application to handle.

  ```csharp
  Time taken to get message: 1126 in ms.
  Time taken to get message: 79 in ms.
  Time taken to get message: 157 in ms.
  ```

  - But after setting the PrefetchCount

  ```csharp
  Time taken to get message: 1126 in ms.
  Time taken to get message: 79 in ms.
  Time taken to get message: 157 in ms.
  ```

## References

- Part 1: <https://lockmedown.com/be-sure-with-azure-net-azure-service-bus-part-1/>
- Part 2: <https://lockmedown.com/everything-you-need-to-know-about-azure-service-bus-brokered-messaging-part-2/>
- Part 3: <https://lockmedown.com/everything-need-know-azure-service-bus-brokered-messaging-part-3/>
