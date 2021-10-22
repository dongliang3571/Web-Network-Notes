# Web-Network-Notes

### Websocket, Comet, long-polling, persistent connection

#### Comet

Comet is a web application model in which a long-held HTTP request allows a web server to push data to a browser, without the browser explicitly requesting it. Comet is an umbrella term, encompassing multiple techniques for achieving this interaction. All these methods rely on features included by default in browsers, such as JavaScript, rather than on non-default plugins. The Comet approach differs from the original model of the web, in which a browser requests a complete web page at a time.

The use of Comet techniques in web development predates the use of the word Comet as a neologism for the collective techniques. Comet is known by several other names, including **Ajax Push**, **Reverse Ajax**, **Two-way-web**, **HTTP Streaming**, and **HTTP server push** among others. The term Comet is not an acronym, but was coined by Alex Russell in his 2006 blog post Comet: Low Latency Data for the Browser.

#### Websocket

The WebSocket API is an advanced technology that makes it possible to open a two-way interactive communication session between the user's browser and a server. With this API, you can send messages to a server and receive event-driven responses without having to poll the server for a reply.

#### Server-sent events

This is long-polling mechanism

https://html.spec.whatwg.org/multipage/server-sent-events.html#server-sent-events

#### Difference between server-sent events and websocket

https://stackoverflow.com/questions/5195452/websockets-vs-server-sent-events-eventsource

#### HTTP Persistent connection VS WebSocket

At the TCP/IP level it looks the same: a socket is open.

But from the browser point of view they are completely different. The keep-alive is for the browser to re-use to request more content (e.g. images, css files, next page on the site). WebSockets is for two-way communication from within your Javascript application code. The server can choose to send content at any time. Your JS application can send data to the server at any time.

Also worth comparing to SSE (aka EventSource), which also allows the server to choose to send content at any time, but is one-way (your JS application has to resort to using XHR when it needs to send more data). (A full comparison of WebSockets and SSE can get very complex, so I'll say no more here, except to say that SSE can often be the correct choice.)

Also compare to Server Push in HTTP/2 (aka SPDY). This is for the server to proactively push files (images, css files, next page on the site), but it is at the browser-level again, not controlled from Javascript


#### Difference between Rest API and Stream API (eg. Twitter API)

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


#### Chunked transfer encoding

https://en.wikipedia.org/wiki/Chunked_transfer_encoding

### API Proxy

#### Good resource

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

### OAUTH(Open Authentication)

#### Good resource

1. [How is OAuth 2 different from OAuth 1?](http://stackoverflow.com/questions/4113934/how-is-oauth-2-different-from-oauth-1)

2. [A conceptual look at OAuth](https://courses.codepath.com/course_videos/ios_university/youtu/tFYrq3d54Dc?title=A+Conceptual+Look+at+OAuth)

OAuth allows notifying a resource provider (e.g. Facebook) that the resource owner (e.g. you) grants permission to a third-party (e.g. a Facebook Application) access to their information (e.g. the list of your friends).

### SOAP, WSDL, REST

#### WSDL

A **WSDL** is an XML document that describes a web service. It actually stands for Web Services Description Language.

**SOAP** is an XML-based protocol that lets you exchange info over a particular protocol (can be HTTP or SMTP, for example) between applications. It stands for Simple Object Access Protocol and uses XML for its messaging format to relay the information. [good resource](http://www.doublehops.com/2009/07/07/quick-tutorial-on-getting-started-with-soap-in-php/comment-page-1/)

  "You use SOAP just the same way that you would any PHP class. However, in this case the class does not exist in the local applications file system, but at a remote site accessed over http." ... "If we think of using a SOAP service as just another PHP class then the WSDL document is a list of all the available class methods and properties. "

[understand WSDL](https://msdn.microsoft.com/en-us/library/ms996486.aspx)

#### SOAP

[understand SOAP](https://msdn.microsoft.com/en-us/library/ms995800.aspx)

**Make SOAP request with curl**

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

#### REST

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

#### Difference between SOAP and REST

https://stackoverflow.com/questions/19884295/soap-vs-rest-differences

A **SOAP** client works like a custom desktop application, tightly coupled to the server. There's a rigid contract between client and server, and everything is expected to break if either side changes anything. You need constant updates following any change, but it's easier to ascertain if the contract is being followed.

A **REST** client is more like a browser. It's a generic client that knows how to use a protocol and standardized methods, and an application has to fit inside that. You don't violate the protocol standards by creating extra methods, you leverage on the standard methods and create the actions with them on your media type. If done right, there's less coupling, and changes can be dealt with more gracefully

In short, REST use `GET`, `PUT`, `POST`, `DELETE` as verbs(operations), but SOAP has to use it's own defined operations, could be `addUser`, `deleteUser`, `something else`.

### What is hypermedia , hypermedia controls, hypermedia formats

There's a lot of confusion about this, because most applications that call themselves REST don't use hypermedia and aren't REST at all.

**Hypermedia** is a generalization of hypertext for content other than HTML. You can say hypertext is a subset of hypermedia. Hypermedia can be HTML in a browser, with all links, buttons and everything that's rendered so you can browse a website, or it can be a XML or JSON document intended to be parsed by an automated client who will also follow links and actions like a human would do with a browser, clicking rendered links and buttons.

**HATEOAS** means the interaction of a client with a REST application must be driven by hypermedia, or to put it simply, the client should obtain all URIs for every resource it needs by following links in the representation of resources themselves, not by relying on out-of-band information, like URI patterns given in documentation, as many APIs do.

This is simpler than it sounds. It just means that the interaction between a client and a REST application should be exactly like a human browsing a website. Take Stack Overflow itself for example. There are Users, Questions and Answers. When you want to see a list of your questions, you don't go to a documentation website, get an URI template for listing your questions, fill a placeholder with your user id and paste it on your brownser. You simply click on a link to another document described as the list of questions, and you don't even care about what the exact URI is. That's what HATEOAS means in practice.

An **hypermedia format** defines the contract between client and server. It's the hyperlink-enabled data format you are using for a particular representation of a resource in an hypermedia application. For instance, if you have an User resource, you have to document what exactly clients should expect from a representation of that resource and how to parse the representation to extract the information. Before interacting with your API, your clients need to implement a parser to extract the information, they need to know what properties the resource has and what they mean, what link relations they should expect and what state transitions are available, etc.

**Hypermedia controls** are the combinations of protocol methods and link relations in an hypermedia format that tells the client what state transitions are available and how to perform them. For instance, a Question might have a rel=post_answer link that expects an Answer representation as the payload of a POST method and will create a new Answer resource related to it.

Once you have a set of hypermedia formats defined, you need a **domain specific media-type** to determine exactly what hypermedia format is being used for a particular interaction. A generic media-type like application/xml only tells the client how to parse the data format, it doesn't say anything about the information extracted by the parser. For instance, let's say a document has the media-type application/vnd.mycompany.user.v1+xml, the client knows it's a version 1.0 representation of the User resource in XML format. If you change the resource by adding or removing properties, links, etc, you can change the version number and clients won't break, since they can request the version they were implemented for by using the Accept header. You can also provide multiple formats for the same resource, like XML or JSON, and even a pretty human-readable representation in HTML.

When you wrap everything together -- the underlying protocol, HTTP; the contracts defined by hypermedia formats and media types -- you have your Domain Application Protocol, which is the whole set of resources and available state transitions advertised by your application.

Needless to say, 99% of the so-called REST APIs you'll find around the internet don't follow all of this. Most of them are simply HTTP APIs that follow some of the REST constraints, sometimes because they don't really need all of them, sometimes because that's what the developers thought REST really is.

### GET, POST, PUT and DELETE

There seems to be quite a bit of misunderstanding here. PUT versus POST is not really about replace versus create, but rather about idempotency and resource naming.

**PUT** is an **idempotent** operation. With it, you give the name of a resource and an entity to place as that resource's content (possibly with server-generated additions). Crucially, doing the operation twice in a row should result in the same thing as if it was done just once or done 20 times, for some fairly loose definition of “the same thing” (it doesn't have to be byte-for-byte identical, but the information that the user supplied should be intact). You wouldn't ever want a PUT to cause a financial transaction to be triggered.

**POST** is a **non-idempotent** operation. You don't need to give the name of the resource which you're looking to have created (nor does a POST have to create; it could de-duplicate resources if it wished). POST is often used to implement “create a resource with a newly-minted name and tell me what the name is” — the lack of idempotency implied by “newly-minted name” fits with that. Where a new resource is created, sending back the locator for the resource in a Location header is entirely the right thing to do.

Now, if you are taking the policy position that clients should never create resource names, you then get POST being the perfect fit for creation (though theoretically it could do anything based on the supplied entity) and PUT being how to do update. For many RESTful applications that makes a lot of sense, but not all; if the model being presented to the user was of a file system, having the user supply the resource name makes a huge amount of sense and PUT becomes the main creation operation (and POST becomes delegated to less common things like making an empty directory and so on; WebDAV reduces the need for POST even further).

The summary: Don't think in terms of create/update, but rather in terms of who makes the resource names and which operations are idempotent. PUT is really create-or-update, and POST is really do-anything-which-shouldnt-be-repeated-willy-nilly.

Better is to choose between PUT and POST based on idempotence of the action.

**PUT** implies putting a resource - completely replacing whatever is available at the given URL with a different thing. By definition, a PUT is idempotent. Do it as many times as you like, and the result is the same. x=5 is idempotent. You can PUT a resource whether it previously exists, or not (eg, to Create, or to Update)!

**POST** updates a resource, adds a subsidiary resource, or causes a change. A POST is not idempotent, in the way that x++ is not idempotent.

By this argument, PUT is for creating when you know the URL of the thing you will create. POST can be used to create when you know the URL of the "factory" or manager for the category of things you want to create.

so:

`POST /expense-report`

or:

`PUT  /expense-report/10929`

### Jumpboxes vs. Bastion Hosts

Both bastion hosts and jumpboxes function similarly: they segregate between one private network or server group and external traffic. Usually you connect to them through SSH or RDP. They each create a single point of entry to a cluster, but their intended purpose and architecture are subtly different in practice.

A **jump server** is a virtual machine that is used to manage other systems. It is sometimes called a “pivot server” for this reason: once you are logged in, you can “pivot” to the other servers. It is usually security hardened and treated as the single entryway to a server group from within your security zone, or inside the overall network. A jump server is a “bridge” between two trusted networks. The two security zones are dissimilar but both are controlled.

A **bastion host** is also treated with special security considerations and connects to a secure zone, but it sits outside of your network security zone. The bastion host is intended to provide access to a private network from external networks such as the public internet. Email servers, web servers, security honeypots, DNS servers, FTP servers, VPNs, firewalls, and security appliances are sometimes considered bastion hosts.

In both cases, the connecting server can be treated as a single audit point for logging access to the subnetworks. Both jump servers and bastion hosts are considered weak points and careful attention must be given to keep them up to date and monitored.


### AWS

[AWS](https://www.youtube.com/watch?v=X0wU-HTjv0g)

[AWS S3 Rest API]http://czak.pl/2015/09/15/s3-rest-api-with-curl.html

### Authentication and authorization

#### Hash Algorithm Aka Hash Function

**Definitions:**

Hash algorithms are used widely in computer science field. But with difference purposes, different hash algorithm is applied. For example,
hash function that computes hash key for data structure hashtable in programming languages is different from hash function that computes (checksum)[https://en.wikipedia.org/wiki/Checksum] to verify data integrity. The type of hash algorithm like checksum algorithm is also called (crytographic hash alogorithm)[https://en.wikipedia.org/wiki/Cryptographic_hash_function]. It widely used for check message integrity in network. Crytographic hash alogorithm includes MD5, (SHA0, SHA1, SHA2, SHA3)[https://en.wikipedia.org/wiki/Secure_Hash_Algorithms] and so on.

The ideal cryptographic hash function has five main properties:

- it is deterministic so the same message always results in the same hash
- it is quick to compute the hash value for any given message
- it is infeasible to generate a message from its hash value except by trying all possible messages
- a small change to a message should change the hash value so extensively that the new hash value appears uncorrelated with the old hash value
- it is infeasible to find two different messages with the same hash value

### Encryption

#### Symmertric encrytion

Both party shares a key and encryt and decrypt all messages using the same key

#### Asymmetric encryption

- **public key encryption** - there is a public key and a private key, they are different
  - **Encrypting** - When encrypting, you use their public key to write a message and they use their private key to read it.
  - **Signing** - When signing, you use your private key to write message's signature, and they use your public key to check if it's really yours. It's very similar to encryption
  https://en.wikipedia.org/wiki/Digital_signature#How_they_work
  In RSA crypto, when you generate a key pair, it's completely arbitrary which one you choose to be the public key, and which is the private key. If you encrypt with one, you can decrypt with the other - it works in both directions.
  It's fairly simple to see how you can encrypt a message with the receiver's public key, so that the receiver can decrypt it with their private key.
  A signature is proof that the signer has the private key that matches some public key. To do this, it would be enough to encrypt the message with that sender's private key, and include the encrypted version alongside the plaintext version. To verify the sender, decrypt the encrypted version, and check that it is the same as the plaintext.
  Of course, this means that your message is not secret. Anyone can decrypt it, because the public key is well known. But when they do so, they have proved that the creator of the ciphertext has the corresponding private key.
  However, this means doubling the size of your transmission - plaintext and ciphertext together (assuming you want people who aren't interested in verifying the signature, to read the message). So instead, typically a signature is created by creating a hash of the plaintext. It's important that fake hashes can't be created, so cryptographic hash algorithms such as SHA-2 are used.
  So:
    1. To generate a signature, make a hash from the plaintext, encrypt it with your private key, include it alongside the plaintext.
    2. To verify a signature, make a hash from the plaintext, decrypt the signature with the sender's public key, check that both hashes are the same.

#### MAC, HMAC

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

### SAML, SSO

#### SAML

https://www.varonis.com/blog/what-is-saml/#:~:text=Security%20Assertion%20Markup%20Language%20(SAML,log%20into%20many%20different%20websites.

#### Single sign-on(SSO)

Utilize SAML to pass authentication information between service provider and identity provider


### Role-based authorization, Claim-based authorization

#### Role-based authorization

A user gets assigned to one or more roles through which the user gets access rights. Also, by assigning a user to a role, the user immediately gets all the access rights defined for that role.

#### Claim-based authorization

https://docs.microsoft.com/en-us/aspnet/core/security/authorization/claims?view=aspnetcore-3.1

When an identity is created it may be assigned one or more claims issued by a trusted party. A claim is a name value pair that represents what the subject is, not what the subject can do. For example, you may have a driver's license, issued by a local driving license authority. Your driver's license has your date of birth on it. In this case the claim name would be DateOfBirth, the claim value would be your date of birth, for example 8th June 1970 and the issuer would be the driving license authority. Claims based authorization, at its simplest, checks the value of a claim and allows access to a resource based upon that value. For example if you want access to a night club the authorization process might be:

The door security officer would evaluate the value of your date of birth claim and whether they trust the issuer (the driving license authority) before granting you access.

An identity can contain multiple claims with multiple values and can contain multiple claims of the same type.

### X.509, certificate, CA, keystore, truststore, private key, HTTPS, TLS/SSL, Crytography

#### keystore vs truststore

https://www.educative.io/edpresso/keystore-vs-truststore

**Keystore** is used to store private key and identity certificates that a specific program should present to both parties (server or client) for verification.

**Truststore** is used to store certificates from Certified Authorities (CA) that verify the certificate presented by the server in SSL connection.

| Keystore	| Truststore |
|-----------|------------|
|Keystore stores your credential. (server or client) |	Truststore stores others credentials (CA)|
|Keystore is needed when you are setting up the server side on SSL	| Truststore setup is required for the successful connection at the client side|
|Client will store its private key and identify certificate on Keystore	| Server will authenticate the client against the certificate stored on the server’s Truststore |
|`javax.net.ssl.keyStore` is used to specify Keystore	| `javax.net.ssl.trustStore` is used to specify Truststore.|
|Keystore passwords are stored in plaintext that is only readable by the specific group.	| Truststore passwords are stored in plaintext that can be read by everyone.|
|Keystore contains private and sensitive information	| Truststore doesn’t contain private and sensitive information|


#### HTTPS, TSL/SSL, CSR, CRT

https://www.youtube.com/watch?v=T4Df5_cojAs

https://github.com/k8sp/tls

#### How HTTPS/TLS works between browser and http server

1. Http server creates a CRS using tools like openssl and ask a CA to sign it with CA private key.
2. CA agrees and sign the CRS and return it back as a TSL certificate(CA signed certificate), which is a combination of a CRS and a digital signature CRS
3. The http server installs the certificate
4. When a browser requests a https resource, TSL certifcate is send to browser first
5. The browser checks the CA from the TSL certificate and all built-in CAs in the browser, make sure the CA from the http server is trusted.
6. The browser goes to the CA and use the CA public key to verify the signature in the TLS certificate and if verified CRS is same as CRS sent from http server, it's legit.
7. Once verification is done, the browser creates a new secret and encrypted with the public key in the http server CRS
8. The http server gets the encrypted secret and decrypt it with its private key.
9. Now only the browser and the http server has the secret
10. They can start communicate using the secret thru symmetrical encryption.

#### How HTTPS/TLS works between http server and http server

1. Each of the server creates a CRS using tools like openssl and ask a CA t sign it with CA private key.
2. CA agrees and sign both CRS and return it back as TSL certificates(CA signed certificate), which is a combination of a CRS and signed CRS.
3. Both http servers install the certificates
4. Http server A sends its TSL certificate to http server B, http server B checks the CA from the TSL certificate and all installed CAs in the server, make sure the CA from http server A is trusted.
5. Http server B will do the same thing
6. Both http servers verifies each other and both generate a new secret and encryt them with each other's public keys and send to each other.
7. Both http servers got the secrets and combine two secrets.
8. Now only these two http servers has the newly combined secret.
9. They can start comminicate using the secret thru symmetrical encryption

#### HTTPS/TLS in Java server and client

1. On server side, we can use `keytool` to generate a self-signed certificate.

    ```bash
    java-home/bin/keytool -genkey -alias server-alias -keyalg RSA -keypass password1 -storepass password2 -keystore keystore.jks
    ```
    the outout file `keystore.jks` actually contains the self-signed certificate(include CA info) and a private key and a public key

    In an example of Java Spring Boot server config:

    ```bash
    # The format used for the keystore. It could be set to PKCS12 in case it is a PKCS12 file
    server.ssl.key-store-type=JKS
    # The path to the keystore containing the certificate
    server.ssl.key-store=classpath:keystore/keystore.jks
    # The password used to generate the certificate
    server.ssl.key-store-password=password2
    # The alias mapped to the certificate
    server.ssl.key-alias=server-alias
    # enable ssl
    server.ssl.enabled=true
    ```

2. Export the generated self-signed certificate(CA) in `keystore.jks` into the file `server.cer`

    ```bash
    java-home/bin/keytool -export -alias server-alias -storepass password2 -file server.cer -keystore keystore.jks
    ```

3. Import the generated self-signed certificate(CA) into a truststore file `cacerts.jks` for client

    ```bash
    java-home/bin/keytool -import -v -trustcacerts -alias server-alias -file server.cer -keystore cacerts.jks -keypass password4 -storepass password3
    ```

3. On client side, we need to trust the CA for the self-signed certificate by specify the trust store location

    In an example of Java Spring client config:

    ```bash
    #trust store location
    trust.store=classpath:keystore/cacerts.jks
    #trust store password
    trust.store.password=password3
    ```

#### CA signing

![SSL signing](https://d1smxttentwwqu.cloudfront.net/wp-content/uploads/2019/07/ca-diagram-b.png)

An example of a CA signed certificate

```bash
$ cat /tmp/stackoverflow-certs.crt
-----BEGIN CERTIFICATE-----
MIIIPDCCBySgAwIBAgIQB2XGTnTlkdaAOcoqhHVj8DANBgkqhkiG9w0BAQsFADBw
MQswCQYDVQQGEwJVUzEVMBMGA1UEChMMRGlnaUNlcnQgSW5jMRkwFwYDVQQLExB3
...
aVnw9vahqf7nKHHcC2VRTUgkQfn9yDmmBOo0nQ8Xgfpd65/PaxVfBnuKfEkXBfpM
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
MIIEsTCCA5mgAwIBAgIQBOHnpNxc8vNtwCtCuF0VnzANBgkqhkiG9w0BAQsFADBs
...
/D6q1UEL2tU2ob8cbkdJf17ZSHwD2f2LSaCYJkJA69aSEaRkCldUxPUd1gJea6zu
xICaEnL6VpPX/78whQYwvwt/Tv9XBZ0k7YXDK/umdaisLRbvfXknsuvCnQsH6qqF
0wGjIChBWUMo0oHjqvbsezt3tkBigAVBRQHvFwY+3sAzm2fTYS5yh+Rp/BIAV0Ae
cPUeybQ=
-----END CERTIFICATE-----
```

##### Why CA signing is needed?

CA signing was invented because of potential `man in the middle` attack.

Assume that we don't have CA signing. We only have a pair of keys(public and private). A server sends the public key to a client, the client generate a new secret key and encrypted with the server's public key and send it back to server. The server gets the encrypted secret and decrypted with its private key. Now they are the only two parties know the secret and they can communicate safely with the secret using symmetrical encryption.

Everything is good until a hacker comes in. He hijack the server's public key and send to client his own public key. Now he can decrypt client's messages with his own private key. And encrpt it again with server public key to tell server that he is the client. Later the hacker can hijack the secret generated from browser. This is so called `man in the middle` attack.

The attack is able to be launched succesfully is because the client doesn't know weather the public key that was sent from server is indeed the right one. To overcome this issue, we need to find a way to verify that the key is the actual key from server.

In order to verify the key. The key needs to be somehow signed by a trustworthy vendor, in this case, CA is the vendor. A CA uses its private key to sign the server's public key and also release its own public key to public, so that everyone has its public key can verify CA's signature. With this approach, the attacker will not be able to use his own public key because it was not signed by the CA.

#### TSL/SSl certificate verification

https://kulkarniamit.github.io/whatwhyhow/howto/verify-ssl-tls-certificate-signature.html

**CA** - Certificate Authority

**CSR** - A CSR or Certificate Signing request is a block of encoded text that is given to a Certificate Authority when applying for an SSL Certificate. A certificate authority(CA) will use a CSR to create your SSL certificate. The actual format is PKCS10 which is defined in RFC 2986. It includes some/all of the key details of the requested certificate such as subject, organization, state, whatnot, as well as the public key of the certificate to get signed. These get signed by the CA and a certificate is returned. The returned certificate is the public certificate (which includes the public key but not the private key), which itself can be in a couple of formats. https://www.sslshopper.com/what-is-a-csr-certificate-signing-request.html

  ```bash
  # generate CSR and private key using openssl
  openssl req -new -newkey rsa:2048 -nodes -out servername.csr -keyout servername.key

  # decode CSR
  openssl req -in server.csr -noout -text
  ```

**CRT** - is a public key certificate consisting of CRS and signed CRS(signature), it's signed by a CA. Also known as a digital certificate or identity certificate, is an electronic document used to prove the ownership of a public key.

**SSL CRT** - a CRT used in SSL

**X.509 CRT** - is a standard defining the format of public key certificate. All X.509 objects are transferrable and are presented by using Abstract Syntax Notation One (ASN.1)

**Abstract Syntax Notation One (ASN.1)** - is a standard interface description language for defining data structures that can be serialized and deserialized in a cross-platform way

**PEM** - is an encoding, X.509 is usually encoded in PEM. Literally any data can be represented in PEM format. It's governed by RFCs, its used preferentially by open-source software. It can have a variety of extensions (.pem, .key, .cer, .cert, more)

  - **.key** - This is a PEM formatted file containing just the private-key of a specific certificate and is merely a conventional name and not a standardized one. In Apache installs, this frequently resides in /etc/ssl/private. The rights on these files are very important, and some programs will refuse to load these certificates if they are set wrong.

  - **.pem** - Defined in RFCs 1421 through 1424, this is a container format that may include just the public certificate (such as with Apache installs, and CA certificate files /etc/ssl/certs), or may include an entire certificate chain including public key, private key, and root certificates. It can sometimes be used to encode a CSR

  - **.cert .cer .crt** - A .pem (or rarely .der) formatted file with a different extension, one that is recognized by Windows Explorer as a certificate, which .pem is not.


**DER** - The parent format of PEM. It's useful to think of it as a binary version of the base64-encoded PEM file. Not routinely used very much outside of Windows.

**PKCS7** - is a type of encoding just like PEM. It's an open standard used by Java and supported by Windows. Does not contain private key material.

  - **.p7b .keystore** - Defined in RFC 2315 as PKCS number 7, this is a format used by Windows for certificate interchange. Java understands these natively, and often uses .keystore as an extension instead. Unlike .pem style certificates, this format has a defined way to include certification-path certificates.

**PKCS#12** - is also a type of encoding just like PEM, but with added secure feature

 - **.pkcs12 .pfx .p12** - Originally defined by RSA in the Public-Key Cryptography Standards (abbreviated PKCS), the "12" variant was originally enhanced by Microsoft, and later submitted as RFC 7292. This is a passworded container format that contains both public and private certificate pairs. Unlike .pem files, this container is fully encrypted. Openssl can turn this into a .pem file with both public and private keys: openssl pkcs12 -in file-to-convert.p12 -out converted-file.pem -nodes

An analogy to understand these terms:

- A X.509 CRT is deserialized in ASN.1 and encoded in PEM and stored in a file
- a http request is descriablized in Json and encoded in UTF-8 and stored in a file


#### Keytool vs Openssl

In short, they're both crypto key generation tools, but keytool has the additional feature of manipulating Java's preferred key storage file format, the KeyStore.

**Keytool** is a tool that comes with Java that works with KeyStores - it can create KeyStores and manipulate keys and certificates inside them. It can also create keys and sign certificates. So it is both a key generation and a KeyStore-file-administration tool.

  - storepass is used to access the key store
  - keypass is used to access the particular key pair's private key.

**OpenSSL** works with standard formats (PEM/CER/CRT/PKCS/etc) but does not manipulate KeyStore files. It is possible to generate a key and/or certificate with OpenSSL, and then import that key/cert into a KeyStore using keytool, but you can't put the key/cert into the KeyStore directly using OpenSSL.

Java strongly prefers to work with keys and certificates that are stored in a KeyStore (also called a TrustStore when it's only got certificates in it). It is possible, but not trivial, to get Java to work with straightforward PEM/CER/CRT/PKCS/etc files, so for all intents and purposes if you're coding crypto in Java you're going to use a KeyStore.

**Openssl examples**

https://github.com/k8sp/tls/blob/master/openssl.md#x509

**Java HTTPS**

The Java runtime ships with a default set of CA certificates in a truststore, and the only prerequisite for SSL connections to be successfully established is that the SSL certificate of the server be issued by one of the CAs in the truststore.

```java
// a java 8 program talks to a https endpoint
import java.io.IOException;
import java.io.InputStream;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import javax.net.ssl.HttpsURLConnection;
import java.net.URL;
import java.util.stream.Collectors;
import java.util.Base64;
import java.nio.charset.StandardCharsets;

public class Main {

    public static void main(String[] args) throws IOException, InterruptedException {

        // Create a neat value object to hold the URL
        URL url = new URL("https://dongliang3571.github.io");

        // Open a connection(?) on the URL(?) and cast the response(??)
        HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();

        String auth = "username:password";
        String encodedString = Base64.getEncoder().encodeToString(auth.getBytes());
        String authHeaderValue = "Basic " + new String(encodedString);

        // Now it's "open", we can set the request method, headers etc.
        connection.setRequestProperty("accept", "application/json");
        connection.setRequestProperty("Authorization", authHeaderValue);

        // This line makes the request
        InputStream responseStream = connection.getInputStream();

        String result = new BufferedReader(new InputStreamReader(responseStream)).lines().collect(Collectors.joining("\n"));
        System.out.println(result);
    }
}
```

for CA certificates that are not part of original set of CA certificates shipped with java, you can do

```java
System.setProperty("javax.net.ssl.trustStore","<path_to_truststore>");
System.setProperty("javax.net.ssl.trustStorePassword","<truststore_password>");
```

## AWS

https://medium.com/awesome-cloud/aws-vpc-difference-between-internet-gateway-and-nat-gateway-c9177e710af6

- Internet Gateway (IGW) allows instances with public IPs to access the internet.
- NAT Gateway (NGW) allows instances with no public IPs to access the internet.

#### Internet Gateway

An Internet Gateway (IGW) is a logical connection between an Amazon VPC and the Internet. It is not a physical device. Only one can be associated with each VPC. It does not limit the bandwidth of Internet connectivity. (The only limitation on bandwidth is the size of the Amazon EC2 instance, and it applies to all traffic — internal to the VPC and out to the Internet.)

If a VPC does not have an Internet Gateway, then the resources in the VPC cannot be accessed from the Internet (unless the traffic flows via a corporate network and VPN/Direct Connect).

An Internet Gateway allows resources within your VPC to access the internet, and vice versa. In order for this to happen, there needs to be a routing table entry allowing a subnet to access the IGW.

That is to say — an IGW allows resources within your public subnet to access the internet, and the internet to access said resources.
A subnet is deemed to be a Public Subnet if it has a Route Table that directs traffic to the Internet Gateway.

#### NAT Gateway

A NAT Gateway does something similar, but with two main differences:
It allows resources in a private subnet to access the internet (think yum updates, external database connections, wget calls, OS patch, etc).
It only works one way. The internet at large cannot get through your NAT to your private resources unless you explicitly allow it.
AWS introduced a NAT Gateway Service that can take the place of a NAT Instance. The benefits of using a NAT Gateway service are:
It is a fully-managed service — just create it and it works automatically, including fail-over.
A NAT gateway supports 5 Gbps of bandwidth and automatically scales up to 45 Gbps. (a NAT Instance is limited to the bandwidth associated with the EC2 instance type).
However:
Security Groups cannot be associated with a NAT Gateway.
You’ll need one in each AZ since they only operate in a single AZ.
