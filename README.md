# API-Notes

## Good resource

1. [The battle for your api proxy](http://blog.apievangelist.com/2011/06/11/the-battle-for-your-api-proxy/)

## API Proxy

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
