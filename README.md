# API-Notes

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

**REST** is an architectural style of networked systems and stands for Representational State Transfer. It's not a standard itself, but does use standards such as HTTP, URL, XML, etc.

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
