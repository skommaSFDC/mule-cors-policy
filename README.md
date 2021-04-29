# mule-cors-policy
## CORS interceptor on Mule API http listener

__CORS (Cross-origin resource sharing) is a standard mechanism that allows JavaScript XMLHttpRequest (XHR) calls executed in a web page to interact with resources from non-origin domains.CORS is a commonly implemented solution to the "same-origin policy" that is enforced by all browsers.__

*MuleSoft documentation: https://docs.mulesoft.com/api-manager/2.x/cors-policy*

The CORS algorithm works on the web server and on the client-side for the web page that requested the information.
- A preflight is a preliminary request (using OPTIONS as the HTTP method) from the web browser to the backend server to test the identity (origin and a few other headers) of the web page that is trying to perform the request.
- If the backend does not accept the origin, the backend server responds to the request without a specific header (Access-Control-Allow-Origin). The client then understands that the page’s origin is not allowed in that server and does not execute the actual request.

*So in some cases, for instance, GET with custom headers and/or POST, when you invoke GET or POST endpoint, browser issues a preflight request first and only then the actual service call once preflight passes CORS test*

*CORS support for Mule Apps can be added either as CORS Interceptor at http listener config level at the application level OR can be enforced thru API Manager via CORS policy. Even when you apply using API Manager, you can apply directly on the implementation API (via auto-discovery) or at the Proxy layer on top of implementation layer.*

Browser automatically passes __Origin__ header with the value of its domain. When preflight request is invoked, it is issued with the following request headers:
- Origin: The origin making the cross origin request.
- Access-Control-Request-Method: The method that is invoked in the actual request.  is sent in the preflight request.
- Access-Control-Request-Headers: Custom headers that are sent in the actual request.

*If that domain is configured to be one of the accepted origins CORS interceptor/policy, requested method is supported, and request headers are supported - then response header access-control-allow-origin populated with the value of the domain sent in the request.*

__In http listener config, configuration of CORS interceptor looks like this with one or more domains from which requests to the API are accepted:__

![image](https://user-images.githubusercontent.com/16226297/116600861-ca56b280-a8f7-11eb-8156-0a358b52f139.png)

### In the API Manager, CORS Policy is as shown below

![image](https://user-images.githubusercontent.com/16226297/116602749-215d8700-a8fa-11eb-9af2-c70e12551c7a.png)


*Used POSTMAN to test it and invoked OPTIONS method with the above three headers*

### Successful Test. Expected domain is found by Mule CORS interceptor. Returns *access-control-allow-origin* header

![image](https://user-images.githubusercontent.com/16226297/116602579-eb200780-a8f9-11eb-98ac-eb0b037e1d02.png)


### Failed test. Domain sent not accepted. Does not return *access-control-allow-origin* header

![image](https://user-images.githubusercontent.com/16226297/116602650-00953180-a8fa-11eb-8e73-e72de581c1c4.png)
