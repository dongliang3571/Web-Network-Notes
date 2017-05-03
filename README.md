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
