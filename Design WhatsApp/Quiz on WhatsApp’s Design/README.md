# Quiz on WhatsApp’s Design


```
1
The WebSocket manager is responsible for which function?

A)
Routing data toward a user

B)
Maintaining the mapping between users and their WebSocket handlers

C)
Reconnecting users to blob storage

D)
None of the above
```

```
2
What happens to the message if it’s sent to an offline user?

A)
The message is discarded, and an error response is sent back to the sender.

B)
The message is forwarded to another user.

C)
The message is stored in a database for a temporary period unless the user becomes online.

D)
None of the above
```

```
3
Why can’t WhatsApp use the Mnesia database to store media files instead of using blob storage?

A)
Mnesia provides limited capacity.

B)
Blob store is optimized to store and retrieve large files.

C)
Mnesia is more costly than blob storage.

D)
None of the above
```

```
4
(Fill in the blank.) If a media file is shared and accessed multiple times, it’s stored in ________ from blob storage.

A)
Kafka

B)
the Mnesia database

C)
a CDN

D)
a MySQL database
```

```
5
(Fill in the blank.) WebSocket servers use cache to ________.

A)
store messages temporarily

B)
store messages permanently

C)
store mapping of users and their corresponding WebSocket handlers

D)
store metadata of each user
```

Answers

1. (B)
2. (C)
3. (B)
4. (C)
5. (C)
