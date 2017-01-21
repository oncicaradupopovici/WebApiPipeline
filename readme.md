# WebAPI Request Processing Pipeline

This is a study project meant to shead light on the WebApi request processing pipelie and illustrate the framework extensibility points.

## 1. The hosting environment:

This environment is responsible for providing a instance of **HttpServer** witch exposes the HttpConfiguration and forwards the *HttpRequestMessage* to the *HttpMessageHandlers* (the next stage of the pipeline). Actualy the HttpServer is itself a *DelegatingHandler* (a specialized *HttpMessageHandler*) that only *massages* the *HttpRequestMessage* before invoking the next *HttpMessageHandler*.
This phase is important because you have two out-of-the-box choises for hosting a web api:
* ASP.Net: the good old traditional environment. So in ASP.Net you have the **HttpControllerHandler** witch is a bad name for a *HttpHandler* responsible for handling Web Api requests by providing the hosting environment for the Web Api pipeline a.k.a an instance of *HttpServer*.
* Katana (also known as the Microsoft OWIN implementation) witch provides the **HttpSelfHostServer** witch is a specialized *HttpServer*. With OWIN you can host your web api in any .net process like a console app or windows service or whatever.

The important thing to note here is that **WebAPI is not part of System.Web nor has dependencies on it** so **the ASP.Net part of ASP.Net Web Api is just a marketing prefix**.