# RestAPI

# Web Architecture
The six constraints are: (click the constraint to read more)
* Uniform Interface
* Stateless
* Cacheable
* Client-Server
* Layered System
* Code on Demand (optional)



# Resources 
• Everything is a resource 
• Resources are addressable via URIs (Uniform Resource Identifier) Example: GET http://<pref>/principals/133519972001296 
• Resources are self descriptive – Typically through content types (“application/xml” “application/json”) – Resources are stateless 
• Resources are manipulated via verbs and the uniform interface

# Command API
Take a resources, add a command (verb) to the end, send data for that command in POST HTTP verb
POST /street/11/repave
POST /house/122/condemn
POST /people/993/hospitalize

Three patterns of payload format encoding most frequently found in the wild are:
* HTTP headers (e.g. Content-Type: and Accept:)
* GET parameters (e.g. &format=json)
* resource label (e.g. /foo.json)

Good RESTful URL examples
/api/v1/magazines.json 
/api/v1/magazines.json?year=2011&sort=desc 
/api/v1/magazines/1234.json 
/api/v1/magazines/1234/articles.json 
/api/v1/magazines/1234/articles.xml 
/api/v1/magazines/1234.json?fields=title,subtitle,date
/api/v1/magazines/1234/articles.json 


Bad RESTful URL examples
/magazine --Non-plural noun:
/magazine/1234 
/magazine/1234/create	--Verb in URL:
/magazines/2011/desc 	--Filter outside of query string:


//no effect if the resource already exists.
HTTP/1.1 405 Method Not Allowed
Vary: Accept
Content-Type: text/javascript

{
  "developerMessage" : "Unable to create a magazine with ID of 1234 because a magazine with that ID already exists",
  "userMessage" : "Unable to create duplicate magazine 1234",
  "errorCode" : "444444",
  "moreInfo" : "http://api.example.gov/v1/documentation/errors/444444.html"
}




# Resource Vs Command
https://image.slidesharecdn.com/cqrsapi-141104212120-conversion-gate01/95/cqrs-api-20-638.jpg?cb=1415137502
https://image.slidesharecdn.com/cqrsapi-141104212120-conversion-gate01/95/cqrs-api-21-638.jpg?cb=1415137502
https://image.slidesharecdn.com/cqrsapi-141104212120-conversion-gate01/95/cqrs-api-37-638.jpg?cb=1415137502

# Error Handling
https://blogs.mulesoft.com/dev/api-dev/api-best-practices-response-handling/	
https://www.polidea.com/blog/Error_Handling_why_it_is_crucial_in_API_design_process/



# Idempotent/Safe Methods

Idempotent/Safe Methods 
Idempotent methods can be applied over and over again and always have the same effect on the resource 
Safe methods do not have any modifying effect on the resource


# POST v PUT v PATCH 
● POST is used to create an entity 
● PUT is used to update an entity where you must send the entire representation of the entity as you wish for it to be stored 
● PATCH is used to update an entity where you send only the fields that need updated





![1](http://networkop.co.uk/images/rest-crud.png)
![1](http://blog.ciaranoconnor.me/content/images/2016/02/RESTful-API-design-1014x457.jpg)


* GET tasks/5/messages – Retrieves list of messages for task #5
* GET tasks/5/messages/10 – Retrieves the 10th messages for task #5
* POST tasks/5/messages – Create a new message for task #5
* DELETE tasks/5/messages/10 – Delete the 10th messages of task #5
* PUT tasks/5/messages/12 – Update the 12th messages of task #5


* [Understanding of rest](https://scotch.io/bar-talk/a-quick-understanding-of-rest)
* [Best Practices for Designing a Pragmatic RESTful API](http://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api)
* [REST 101: An Introduction to Restful APIs -Infographic](https://dzone.com/articles/rest-101-an-introduction-to-restful-apis-infograph)
* [Microsoft REST API Guidelines Are Not RESTful](https://www.infoq.com/news/2016/07/microsoft-rest-api)
* [Soap Vs REST](http://nordicapis.com/rest-vs-soap-nordic-apis-infographic-comparison/)
* [Securing your APIs with OAuth, OpenID, and OpenID Connect](http://www.slideshare.net/lobster1234/securing-your-apis-with-oauth-openid-and-openid-connect)

The never-ending REST API design debate
https://www.slideshare.net/restlet/the-neverending-rest-api-design-debate

REST API Best Practices
http://javabeat.net/rest-api-best-practices/

REST API ARCHITECTURE – BEST PRACTICES
http://dasunhegoda.com/rest-api-architecture-best-practices/1049/

# https://dzone.com/articles/restful-web-services

https://github.com/RestCheatSheet/platform-cheat-sheet
https://github.com/RestCheatSheet/api-cheat-sheet

REST
* [Microsoft REST API Guidelines](https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md)
* [REST Design - Choosing the Right HTTP Method](http://codeahoy.com/2016/07/04/rest-design-choosing-the-right-http-method)
* [3 FREE API Security Test Tools](https://www.joecolantonio.com/2016/07/19/3-free-api-security-tools/)

## API Ebook
* [The API Economy](http://nordicapis.com/wp-content/uploads/theapieconomy.pdf)
* [Programming APIs with the Spark Web Framework](http://nordicapis.com/wp-content/uploads/using-spark-java-to-program-apis.pdf)
* [Securing The API Stronghold](http://nordicapis.com/wp-content/uploads/securing-the-api-stronghold.pdf)
* [The API Lifecycle](http://nordicapis.com/wp-content/uploads/theapilifecycle.pdf)
* [Developing the API Mindset](http://nordicapis.com/wp-content/uploads/developingtheapimindset.pdf)
* [Design Beautiful REST + JSON APIs](http://www.slideshare.net/stormpath/rest-jsonapis)
* [REST+JSON API Design - Best Practices for Developers](https://www.youtube.com/watch?v=hdSrT4yjS1g)
* 
http://www.restapitutorial.com
RESTful API Authentication Basics
https://dzone.com/articles/restful-api-authentication-basics-1


https://dzone.com/articles/a-need-for-rest-apis-and-api-development-managemen-1
A Need for REST APIs and API Development Management


## API Infographic
![1](http://www.platform28.com/wp-content/uploads/2015/02/Infographic-3.png))
![1](http://d27n205l7rookf.cloudfront.net/wp-content/uploads/2015/01/API-Infographic-Final.jpg)
![1](http://blog.smartbear.com/wp-content/uploads/2016/08/REST-101-Infographic-Final.png)
![1](https://www.api2cart.com/wp-content/uploads/2015/07/JSON-REST-vs-XML-SOAP.png)
![1](http://media02.hongkiat.com/rest-restful-api-dev/01-restful-rest-diagram-api.jpg)
![1](https://s-media-cache-ak0.pinimg.com/564x/8d/9e/33/8d9e33a75699e3dc95eaf1f00e547ab5.jpg)
![1](https://657cea1304d5d92ee105-33ee89321dddef28209b83f19f06774f.ssl.cf1.rackcdn.com/Cloud_DNS_Infographic-1-71149d726aad5000c246d7303d0fd9055e00ee46fef088768a311c073f61dfc5.png)

https://www.smashingmagazine.com/2016/09/understanding-rest-and-rpc-for-http-apis/
* [API Security: Ways to Authenticate and Authorize](https://dzone.com/articles/api-security-ways-to-authenticate-and-authorize)
