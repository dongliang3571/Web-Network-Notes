# API-Notes

### Difference between Rest API and Stream API (eg. Twitter API)

https://developer.twitter.com/en/docs/tutorials/consuming-streaming-data

https://en.wikipedia.org/wiki/HTTP_persistent_connection

https://www.quora.com/What-is-meant-by-streaming-API

REST / SOAP API work as request and response way. Client send Request to server and server reply back to client as Response [whether in JSON, XML or HTML].

But Streaming API is different in respect of Response. Server continue send Response to client when ever a update is available.

So this is type of socket program where continue stream of response will come to client from server.

eg. twitter streaming API will give you continue stream of responses

REST API won’t maintain a persistent HTTP connection between the client and the server where as a streaming API will maintain a persistent HTTP connection as long as possible. By persistent HTTP connection, I mean, there is a continuous request-response happening between the client and server.

So, in such scenario, the REST API’s will fail to fetch the new instantaneous updates in the server (new tweets as in your query) where as streaming API’s will successfully do it!

A streaming API differs from the normal REST API in the way that it leaves the HTTP connection open for as long as possible(i.e. "persistent connection"). It pushes data to the client as and when it's available and there is no need for the client to poll the requests to the server for newer data. This approach of maintaining a persistent connection reduces the network latency significantly when a server produces continous stream of data like say, today's social media channels. These APIs are mostly used to read/subscribe to data.

### HTTP Persistent connection VS WebSocket

At the TCP/IP level it looks the same: a socket is open.

But from the browser point of view they are completely different. The keep-alive is for the browser to re-use to request more content (e.g. images, css files, next page on the site). WebSockets is for two-way communication from within your Javascript application code. The server can choose to send content at any time. Your JS application can send data to the server at any time.

Also worth comparing to SSE (aka EventSource), which also allows the server to choose to send content at any time, but is one-way (your JS application has to resort to using XHR when it needs to send more data). (A full comparison of WebSockets and SSE can get very complex, so I'll say no more here, except to say that SSE can often be the correct choice.)

Also compare to Server Push in HTTP/2 (aka SPDY). This is for the server to proactively push files (images, css files, next page on the site), but it is at the browser-level again, not controlled from Javascript

### Chunked transfer encoding

https://en.wikipedia.org/wiki/Chunked_transfer_encoding

## API Proxy

### Good resource

1. [The battle for your api proxy](http://blog.apievangelist.com/2011/06/11/the-battle-for-your-api-proxy/)

Every day an API can receive thousands or potentially millions of calls. Before the API can process these requests and returns a response, it has to potentially tackle a huge laundry list of functionalities:

- Identity / Authentication
- Traffic Controls
- Rate Limiting
- Performance
- Security
- Scalability
- Filtering
- Encryption
- Logging

Once all these items are handled, then the API can do what it is designed to do -- process its payload and return a response.

Many API owners tackle all these layers of the API themselves. But there are also several service providers out there looking to do this for them.

Two kind of API proxy

1. The first group of API service providers in this area use what I call the Proxy Flow Through, and this includes Mashery and Apigee. Mashery and Apigee deliver these service by routing all calls to an API through their proxy. Each call actually is made to Mashery and Apigee, then they route the request to the actual API for a response.

![proxy_flow_through](https://github.com/dongliang3571/API-Proxy-Notes/blob/master/screenshots/proxy_flow_through.png?raw=true "proxy_flow_through")

2. The second group of API service providers in this area, use what I call the Proxy Connector, and this includes 3Scale and Mashape. 3Scale and Mashape deliver these services by providing a connector your API can use to communicate with the proxy during each call.

![proxy_connector](https://github.com/dongliang3571/API-Proxy-Notes/blob/master/screenshots/proxy_connector.png?raw=true "proxy_connector")

## OAUTH(Open Authentication)

### Good resource

1. [How is OAuth 2 different from OAuth 1?](http://stackoverflow.com/questions/4113934/how-is-oauth-2-different-from-oauth-1)

2. [A conceptual look at OAuth](https://courses.codepath.com/course_videos/ios_university/youtu/tFYrq3d54Dc?title=A+Conceptual+Look+at+OAuth)

OAuth allows notifying a resource provider (e.g. Facebook) that the resource owner (e.g. you) grants permission to a third-party (e.g. a Facebook Application) access to their information (e.g. the list of your friends).

## SOAP, WSDL, REST

A **WSDL** is an XML document that describes a web service. It actually stands for Web Services Description Language.

**SOAP** is an XML-based protocol that lets you exchange info over a particular protocol (can be HTTP or SMTP, for example) between applications. It stands for Simple Object Access Protocol and uses XML for its messaging format to relay the information. [good resource](http://www.doublehops.com/2009/07/07/quick-tutorial-on-getting-started-with-soap-in-php/comment-page-1/)

  "You use SOAP just the same way that you would any PHP class. However, in this case the class does not exist in the local applications file system, but at a remote site accessed over http." ... "If we think of using a SOAP service as just another PHP class then the WSDL document is a list of all the available class methods and properties. "
  
[understand WSDL](https://msdn.microsoft.com/en-us/library/ms996486.aspx)

[understand SOAP](https://msdn.microsoft.com/en-us/library/ms995800.aspx)

### Make SOAP request with curl

Let’s create a SOAP envelope as below which is the SOAP request to be sent via curl. Create a file with the below content named “request.xml”. The SOAP envelope and the SOAP request parameters depend on your web service.

```
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:v1="http://schemas.conversesolutions.com/xsd/dmticta/v1">
<soapenv:Header/>
<soapenv:Body>
<v1:GetVehicleLimitedInfo>
<v1:vehicleNo>?</v1:vehicleNo>
<v1:phoneNo>?</v1:phoneNo>
</v1:GetVehicleLimitedInfo>
</soapenv:Body>
</soapenv:Envelope>
```

Let’s make a request using the curl command.

```
curl --header "Content-Type: text/xml;charset=UTF-8" --header "SOAPAction: ACTION_YOU_WANT_TO_CALL" --data @FILE_NAME URL_OF_THE_SOAP_WEB_SERVICE_ENDPOINT
```

Below mentioned should be replaced according to your web service.

1. ACTION_YOU_WANT_TO_CALL
2. FILE_NAME
3. URL_OF_THE_SOAP_WEB_SERVICE_ENDPOINT

See the example below to get an idea.

**REST** is an architectural style of networked systems and stands for Representational State Transfer. It's not a standard itself, but does use standards such as HTTP, URL, XML, etc.

An architectural style called REST (Representational State Transfer) advocates that web applications should use HTTP as it was originally envisioned. Lookups should use GET requests. PUT, POST, and DELETE requests should be used for *mutation, creation, and deletion respectively *.

REST proponents tend to favor URLs, such as

http://myserver.com/catalog/item/1729
but the REST architecture does not require these “pretty URLs”. A GET request with a parameter

http://myserver.com/catalog?item=1729
is every bit as RESTful.

Keep in mind that GET requests should never be used for updating information. For example, a GET request for adding an item to a cart

http://myserver.com/addToCart?cart=314159&item=1729
would not be appropriate. GET requests should be idempotent. That is, issuing a request twice should be no different from issuing it once. That’s what makes the requests cacheable. An “add to cart” request is not idempotent—issuing it twice adds two copies of the item to the cart. A POST request is clearly appropriate in this context. Thus, even a RESTful web application needs its share of POST requests.

(good resource)[https://stackoverflow.com/questions/671118/what-exactly-is-restful-programming#answer-671132]

(How I Explained REST to My Wife)[http://web.archive.org/web/20130116005443/http://tomayko.com/writings/rest-to-my-wife]

REST provides a definition of a resource, which is what those things point to. A web page is a representation of a resource. 

### Difference between SOAP and REST

https://stackoverflow.com/questions/19884295/soap-vs-rest-differences

A **SOAP** client works like a custom desktop application, tightly coupled to the server. There's a rigid contract between client and server, and everything is expected to break if either side changes anything. You need constant updates following any change, but it's easier to ascertain if the contract is being followed.

A **REST** client is more like a browser. It's a generic client that knows how to use a protocol and standardized methods, and an application has to fit inside that. You don't violate the protocol standards by creating extra methods, you leverage on the standard methods and create the actions with them on your media type. If done right, there's less coupling, and changes can be dealt with more gracefully

In short, REST use `GET`, `PUT`, `POST`, `DELETE` as verbs(operations), but SOAP has to use it's own defined operations, could be `addUser`, `deleteUser`, `something else`.

### what is hypermedia , hypermedia controls, hypermedia formats

There's a lot of confusion about this, because most applications that call themselves REST don't use hypermedia and aren't REST at all.

**Hypermedia** is a generalization of hypertext for content other than HTML. You can say hypertext is a subset of hypermedia. Hypermedia can be HTML in a browser, with all links, buttons and everything that's rendered so you can browse a website, or it can be a XML or JSON document intended to be parsed by an automated client who will also follow links and actions like a human would do with a browser, clicking rendered links and buttons.

**HATEOAS** means the interaction of a client with a REST application must be driven by hypermedia, or to put it simply, the client should obtain all URIs for every resource it needs by following links in the representation of resources themselves, not by relying on out-of-band information, like URI patterns given in documentation, as many APIs do.

This is simpler than it sounds. It just means that the interaction between a client and a REST application should be exactly like a human browsing a website. Take Stack Overflow itself for example. There are Users, Questions and Answers. When you want to see a list of your questions, you don't go to a documentation website, get an URI template for listing your questions, fill a placeholder with your user id and paste it on your brownser. You simply click on a link to another document described as the list of questions, and you don't even care about what the exact URI is. That's what HATEOAS means in practice.

An **hypermedia format** defines the contract between client and server. It's the hyperlink-enabled data format you are using for a particular representation of a resource in an hypermedia application. For instance, if you have an User resource, you have to document what exactly clients should expect from a representation of that resource and how to parse the representation to extract the information. Before interacting with your API, your clients need to implement a parser to extract the information, they need to know what properties the resource has and what they mean, what link relations they should expect and what state transitions are available, etc.

**Hypermedia controls** are the combinations of protocol methods and link relations in an hypermedia format that tells the client what state transitions are available and how to perform them. For instance, a Question might have a rel=post_answer link that expects an Answer representation as the payload of a POST method and will create a new Answer resource related to it.

Once you have a set of hypermedia formats defined, you need a **domain specific media-type** to determine exactly what hypermedia format is being used for a particular interaction. A generic media-type like application/xml only tells the client how to parse the data format, it doesn't say anything about the information extracted by the parser. For instance, let's say a document has the media-type application/vnd.mycompany.user.v1+xml, the client knows it's a version 1.0 representation of the User resource in XML format. If you change the resource by adding or removing properties, links, etc, you can change the version number and clients won't break, since they can request the version they were implemented for by using the Accept header. You can also provide multiple formats for the same resource, like XML or JSON, and even a pretty human-readable representation in HTML.

When you wrap everything together -- the underlying protocol, HTTP; the contracts defined by hypermedia formats and media types -- you have your Domain Application Protocol, which is the whole set of resources and available state transitions advertised by your application.

Needless to say, 99% of the so-called REST APIs you'll find around the internet don't follow all of this. Most of them are simply HTTP APIs that follow some of the REST constraints, sometimes because they don't really need all of them, sometimes because that's what the developers thought REST really is.

## GET, POST, PUT and DELETE

There seems to be quite a bit of misunderstanding here. PUT versus POST is not really about replace versus create, but rather about idempotency and resource naming.

PUT is an idempotent operation. With it, you give the name of a resource and an entity to place as that resource's content (possibly with server-generated additions). Crucially, doing the operation twice in a row should result in the same thing as if it was done just once or done 20 times, for some fairly loose definition of “the same thing” (it doesn't have to be byte-for-byte identical, but the information that the user supplied should be intact). You wouldn't ever want a PUT to cause a financial transaction to be triggered.

POST is a non-idempotent operation. You don't need to give the name of the resource which you're looking to have created (nor does a POST have to create; it could de-duplicate resources if it wished). POST is often used to implement “create a resource with a newly-minted name and tell me what the name is” — the lack of idempotency implied by “newly-minted name” fits with that. Where a new resource is created, sending back the locator for the resource in a Location header is entirely the right thing to do.

Now, if you are taking the policy position that clients should never create resource names, you then get POST being the perfect fit for creation (though theoretically it could do anything based on the supplied entity) and PUT being how to do update. For many RESTful applications that makes a lot of sense, but not all; if the model being presented to the user was of a file system, having the user supply the resource name makes a huge amount of sense and PUT becomes the main creation operation (and POST becomes delegated to less common things like making an empty directory and so on; WebDAV reduces the need for POST even further).

The summary: Don't think in terms of create/update, but rather in terms of who makes the resource names and which operations are idempotent. PUT is really create-or-update, and POST is really do-anything-which-shouldnt-be-repeated-willy-nilly.

Better is to choose between PUT and POST based on idempotence of the action.

PUT implies putting a resource - completely replacing whatever is available at the given URL with a different thing. By definition, a PUT is idempotent. Do it as many times as you like, and the result is the same. x=5 is idempotent. You can PUT a resource whether it previously exists, or not (eg, to Create, or to Update)!

POST updates a resource, adds a subsidiary resource, or causes a change. A POST is not idempotent, in the way that x++ is not idempotent.

By this argument, PUT is for creating when you know the URL of the thing you will create. POST can be used to create when you know the URL of the "factory" or manager for the category of things you want to create.

so:

`POST /expense-report`

or:

`PUT  /expense-report/10929`

## AWS

[AWS](https://www.youtube.com/watch?v=X0wU-HTjv0g)

[AWS S3 Rest API]http://czak.pl/2015/09/15/s3-rest-api-with-curl.html

## Hash Algorithm Aka Hash Function

### definitions

Hash algorithms are used widely in computer science field. But with difference purposes, different hash algorithm is applied. For example, 
hash function that computes hash key for data structure hashtable in programming languages is different from hash function that computes (checksum)[https://en.wikipedia.org/wiki/Checksum] to verify data integrity. The type of hash algorithm like checksum algorithm is also called (crytographic hash alogorithm)[https://en.wikipedia.org/wiki/Cryptographic_hash_function]. It widely used for check message integrity in network. Crytographic hash alogorithm includes MD5, (SHA0, SHA1, SHA2, SHA3)[https://en.wikipedia.org/wiki/Secure_Hash_Algorithms] and so on. 

The ideal cryptographic hash function has five main properties:

- it is deterministic so the same message always results in the same hash
- it is quick to compute the hash value for any given message
- it is infeasible to generate a message from its hash value except by trying all possible messages
- a small change to a message should change the hash value so extensively that the new hash value appears uncorrelated with the old hash value
- it is infeasible to find two different messages with the same hash value

## MAC, HMAC

In cryptography, a **message authentication code (MAC)**, sometimes known as a tag, is a short piece of information used to authenticate a message. One of the famous one is **(keyed-hash message authentication code (HMAC))[https://www.youtube.com/watch?v=NU923LkfuvE]**.

Basically, MAC is to prove the integrity of a message. That is,

- Send message over an untrusted network
- Message: engrypted or not
- Prove it has not been altered

HMAC uses crytographic hash alogorithm to generate a MAC, that is,

`HMAC(K, m) = H((K' xor opad) || H((K' xor ipad) || m))`

where

- `H` is a cryptographic hash function,
- `K` is the secret key,
- `m` is the message to be authenticated,
- `K'` is another secret key, derived from the original key K (by padding K to the right with extra zeroes to the input block size of the hash function, or by hashing K if it is longer than that block size),
- `||` denotes concatenation,
- `xor` denotes exclusive or,
- `opad` is the outer padding (0x5c5c5c…5c5c, one-block-long hexadecimal constant),
- `ipad` is the inner padding (0x363636…3636, one-block-long hexadecimal constant).

Another video demostrates HMAC, https://www.youtube.com/watch?v=0628oUIssFA
