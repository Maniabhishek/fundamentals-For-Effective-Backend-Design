## Why are we using a message queue

>- Since most message queues provide best-effort ordering which ensures that
messages are generally delivered in the same order as they're sent and that a
message is delivered at least once which is an important part of our service
functionality.
>- While this seems like a classic publish-subscribe use case, it is actually not as mobile
devices and browsers each have their own way of handling push notifications.
Usually, notifications are handled externally via Firebase Cloud Messaging (FCM) or
Apple Push Notification Service (APNS) unlike message fan-out which we commonly
see in backend services. We can use something like Amazon SQS or RabbitMQ to
support this functionality.
