# Dead Letter Queues
Amazon SQS supports dead-letter queues (DLQ), which other queues (source queues) can target for messages that can't be processed (consumed) successfully. Dead-letter queues are useful for debugging your application or messaging system because they let you isolate unconsumed messages to determine why their processing doesn't succeed.

## Redrive Capability
You can configure a dead-letter queue redrive to move standard unconsumed messages out of an existing dead-letter queue back to their source queues.

After you have investigated the attributes and related metadata available for standard unconsumed messages in a dead-letter queue, you can redrive the messages back to their source queues. Dead-letter queue redrive reduces API call billing by batching the messages while moving them.

By default, dead-letter queue redrive moves messages from a dead-letter queue to a source queue. However, you can also configure any other standard queue as the redrive destination. Additionally, you can configure the redrive velocity to set the rate at which Amazon SQS moves messages.

## When should I use a DLQ
- Do use dead-letter queues with standard queues. You should always take advantage of dead-letter queues when your applications don't depend on ordering. Dead-letter queues can help you troubleshoot incorrect message transmission operations.

`````
Note
Even when you use dead-letter queues, you should continue to monitor your queues and retry sending messages that fail for transient reasons.
`````

- Do use dead-letter queues to decrease the number of messages and to reduce the possibility of exposing your system to poison-pill messages (messages that can be received but can't be processed).
---------------
[Go Home](../README.md)