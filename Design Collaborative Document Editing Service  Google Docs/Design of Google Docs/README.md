# Design of Google Docs
## Design
We’ll complete our design in two steps. In the first step, we’ll explain different components and building blocks and the reason for their choice in our design. The second step will describe how we fulfill various functional requirements by depicting a workflow.

### Components
We’ve utilized the following set of components to complete our design:

- API gateway: Different client requests will get intercepted through the API gateway. Depending on the request, it’s possible to forward a single request to multiple components, reject a request, or reply instantly using an already cached response, all through the API gateway. Edit requests, comments on a document, notifications, authentication, and data storing requests will all go through the API gateway.
- Application servers: The application servers will run business logic and tasks that generally require computational power. For instance, some documents may be converted from one file type to another (for example, from a PDF to a Word document) or support features like import and export. It’s also central to the attribute collection for the recommendation engine.
- Data stores: Various data stores will be used to fulfill our requirements. We’ll employ a relational database for saving users’ information and document-related information for imposing privilege restrictions. We can use NoSQL for storing user comments for quicker access. To save the edit history of documents, we can use a time series database. We’ll use blob storage to store videos and images within a document. Finally, we can use distributed cache like Redis and a CDN to provide end users good performance. We use Redis specifically to store different data structures, including user sessions, features for the typeahead service, and frequently accessed documents. The CDN stores frequently accessed documents and heavy objects, like images and videos.
- Processing queue: Since document editing requires frequently sending small-sized data (usually characters) to the server, it’s a good idea to queue this data for periodic batch processing. We’ll add characters, images, videos, and comments to the processing queue. Using an HTTP call for sending every minor character is inefficient. Therefore, we’ll use WebSockets to reduce overhead and observe live changes to the document by different users.
- Other components: Other components include the session servers that maintain the user’s session information. We’ll manage document access privileges through the session servers. Essentially, there will also be configuration, monitoring, pub-sub, and logging services that will handle tasks like monitoring and electing leaders in case of server failures, queueing tasks like user notifications, and logging debugging information.
The illustration below provides a depiction of how different components and building blocks coordinate to provide the service.

[A detailed design of the collaborative document editing service](./design.jpg)

```
Question 1
Why should we use WebSockets instead of HTTP methods? Why are WebSockets optimal for this kind of communication?

Answer
WebSockets offer us the following characteristics:

- They have a long-lasting connection between clients and servers.
- They enable full-duplex communication. That is, we can simultaneously communicate from client to server and vice versa.
- There’s no overhead of HTTP request or response headers.
The lightweight nature of WebSockets reduces the latency and allows the server to push changes to clients as soon as they are available.
```

```
Question 2
The design above depicts a microservices architecture instead of a monolithic one. Why is that suitable here?

Answer
Microservices are preferred for the following reasons:

- Development is simpler and faster.
- Each service within the architecture is isolated. That is, failure of one service doesn’t produce a cascading effect.
- Different components may have different programming language requirements for various reasons. Microservices give the freedom of using different programming languages for different components.
- Because of microservices’ modular nature, it’s easy to scale and update services individually.
```

```
Question 3
What queuing algorithm is best suited for the operations queue in the design above?

Answer
First in, first out (FIFO) with strict ordering is best suited for the operations queue so that operations are performed in the order requested by the users.
```

### Workflow
In the following steps, we’ll explain how different requests will get entertained after they reach the API gateway:

- Collaborative editing and conflict resolution: Each request gets forwarded to the operations queue. This is where conflicts get resolved between different collaborators of the same document. If there are no conflicts, the data is batched and stored in the time series database via session servers. Data like videos and images get compressed for storage optimization, while characters are processed right away.
- History: It’s possible to recover different versions of the document with the help of a time series database. Different versions can be compared using DIFF operations that compare the versions and identify the differences to recover older versions of the same document.
- Asynchronous operations: Notifications, emails, view counts, and comments are asynchronous operations that can be queued through a pub-sub component like Kafka. The API gateway generates these requests and forwards them to the pub-sub module. Users sharing documents can generate notifications through this process.
- Suggestions: Suggestions are in the form of the typeahead service that offers autocomplete suggestions for typically used words and phrases. The typeahead service can also extract attributes and keywords from within the document and provide suggestions to the user. Since the number of words can be high, we’ll use a NoSQL database for this purpose. In addition, most frequently used words and phrases will be stored in a caching system like Redis.
- Import and export documents: The application servers perform a number of important tasks, including importing and exporting documents. Application servers also convert documents from one format to another. For example, a .doc or .docx document can be converted in to .pdf or vice versa. Application servers are also responsible for feature extraction for the typeahead service.

```
Note: Our use of WebSockets speeds up the overall performance and enables us to facilitate chatting between users who are collaborating on the same document. If we combine WebSockets with a Redis-like cache, it’s possible to develop an effective chatting feature.
```

```
Question 1
We’re implementing view counters through an asynchronous method, which means that the number of views of a document may be outdated. Could we use sharded counters or Redis counters to get effective results?

Answer
Both solutions (sharded counters or Redis counters) will work, though they seem excessive for counting views on documents.

To provide near real-time view counting, we can use a streaming pub-sub system, such as Kafka, where a topic can be based on a document identifier.
```

```
Question 2
The detailed design above doesn’t depict where the view counter data is saved. What would be suitable storage for the view counter, and what design changes will have to be made?

Answer
For scalability purposes, it’s suitable to store the view counter data in NoSQL because the read/write latency of NoSQL is generally lower.

To complete the design, we’ll have to connect the view counter with the NoSQL database.
```
