# mule-cors-policy
## CORS interceptor on Mule API http listener

__CORS (Cross-origin resource sharing) is a standard mechanism that allows JavaScript XMLHttpRequest (XHR) calls executed in a web page to interact with resources from non-origin domains.CORS is a commonly implemented solution to the "same-origin policy" that is enforced by all browsers.__

*CORS support for Mule Apps can be added either as CORS Interceptor at http listener config level at the application level OR can be enforced thru API Manager via CORS policy. Even when you apply using API Manager, you can apply directly on the implementation API (via auto-discovery) or at the Proxy layer on top of implementation layer.*

*Browser automatically passes __Origin__ header with the value of its domain. If that domain is configured to be one of the accepted domains in CORS interceptor/policy, then response header __access-control-allow-origin__ populated with the value of the domain sent in the request.*

__In http listener config, configuration of CORS interceptor looks like this with one or more domains from which requests to the API are accepted:__

![image](https://user-images.githubusercontent.com/16226297/114775726-a2841e00-9d3f-11eb-8dcd-cb97edcb4a99.png)


### In the API Manager, CORS Policy is as shown below


![image](https://user-images.githubusercontent.com/16226297/114775191-065a1700-9d3f-11eb-8a36-9f84b5de63b3.png)


*Used https://www.test-cors.org/ website to test it. You can populate Mule API endpoint for Remote URL, select HTTP Method and send the request. In Browser developer tools, you can view request headers, response headers, and result*


### Successful Test. Expected domain is found by Mule CORS interceptor. Returns *access-control-allow-origin* header

![image](https://user-images.githubusercontent.com/16226297/114776101-17efee80-9d40-11eb-97b8-150b1bbe5265.png)

### Failed test. Domain sent not accepted. Does not return *access-control-allow-origin* header

![image](https://user-images.githubusercontent.com/16226297/114776681-bda35d80-9d40-11eb-9f65-c19dc6399ca3.png)





