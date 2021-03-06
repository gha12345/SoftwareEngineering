# Identifier Design with URIs

## URI Format

* Rule: Forward slash separator (/) must be used to indicate a hierarchical relationshi
```xml
http://api.canvas.restapi.org/shapes/polygons/quadrilaterals/squares
```
* Rule: A trailing forward slash (/) should not be included in URIs
```xml
Many web components and frameworks will treat the following two URIs equally:
http://api.canvas.restapi.org/shapes/
http://api.canvas.restapi.org/shapes
```

* Rule: Hyphens (-) should be used to improve the readability of URIs
```xml
http://api.example.restapi.org/blogs/mark-masse/entries/this-is-my-first-post
```

* Rule: Underscores (_) should not be used in URIs 
* Rule: Lowercase letters should be preferred in URI paths 
* Rule: File extensions should not be included in URIs 
```xml
http://api.college.restapi.org/students/3248234/transcripts/2005/fall.json (not prefered)
http://api.college.restapi.org/students/3248234/transcripts/2005/fall 
```

## URI Authority Design
* Rule: Consistent subdomain names should be used for your APIs
```
For example:
http://api.soccer.restapi.org
```
* Rule: Consistent subdomain names should be used for your client developer portal


## Resource Archetypes
A REST API is composed of four distinct resource archetypes
* Document
* Collection
* Store
* Controller

## Document
* A document resource is a singular concept that is akin to an object instance or database record. 
* A document’s state representation typically includes both fields with values and links to other related resources.
* With its fundamental field and link-based structure, the document type is the conceptual base archetype of the other resource archetypes.
* In other words, the three other resource archetypes can be viewed as specializations of the document archetype.

```xml
Each URI below identifies a document resource:
http://api.soccer.restapi.org/leagues/seattle
http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet
http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players/mike
```

## Collection
* A collection resource is a server-managed directory of resources. 
* Clients may propose new resources to be added to a collection. 
* However, it is up to the collection to choose to create a new resource, or not. 
* A collection resource chooses what it wants to contain and also decides the URIs of each contained resource.

```xml
Each URI below identifies a collection resource:
http://api.soccer.restapi.org/leagues
http://api.soccer.restapi.org/leagues/seattle/teams
http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players
```

## Store
* A store is a client-managed resource repository. 
* A store resource lets an API client put resources in, get them back out, and decide when to delete them. 
* On their own, stores do not create new resources; therefore a store never generates new URIs. 
* Instead, each stored resource has a URI that was chosen by a client when it was initially put into the store.

```xml
PUT /users/1234/favorites/alonso
```
## Controller
* A controller resource models a procedural concept. 
* Controller resources are like executable functions, with parameters and return values; inputs and outputs.
* Like a traditional web application’s use of HTML forms, a REST API relies on controller resources to perform application-specific actions that cannot be logically mapped to one of the standard methods (create, retrieve, update, and delete, also known as CRUD).
* Controller names typically appear as the last segment in a URI path, with no child resources to follow them in the hierarchy. 
* The example below shows a controller resource that allows a client to resend an alert to a user:

```xml
POST /alerts/245743/resend
```

# Resource Modeling
The URI path conveys a REST API’s resource model, with each forward slash separated
path segment corresponding to a unique resource within the model’s hierarchy. For
example, this URI design:
http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet
indicates that each of these URIs should also identify an addressable resource:
http://api.soccer.restapi.org/leagues/seattle/teams
http://api.soccer.restapi.org/leagues/seattle
http://api.soccer.restapi.org/leagues
http://api.soccer.restapi.org


## URI Path Design 
* Rule: A singular noun should be used for document names 
```xml
For example, the URI for a single player document would have the singular form:
http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players/claudio
```

* Rule: A plural noun should be used for collection names 
```xml
For example, the URI for a collection of player documents uses the plural noun form of its contained resources:
http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players
```

* Rule: A plural noun should be used for store names 
```xml
The URI for a store of music playlists may use the plural noun form as follows:
http://api.music.restapi.org/artists/mikemassedotcom/playlists
```

* Rule: A verb or verb phrase should be used for controller names 
```xml
 For example:
http://api.college.restapi.org/students/morgan/register
http://api.example.restapi.org/lists/4324/dedupe
http://api.ognom.restapi.org/dbs/reindex
http://api.build.restapi.org/qa/nightly/runTestSuite
```

* Rule: Variable path segments may be substituted with identity-based values 
```xml
 The URI template example below has three variables (leagueId, TeamId, and playerId):
http://api.soccer.restapi.org/leagues/{leagueId}/teams/{teamId}/players/{playerId}

http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players/21 - Conceptually, the value 21 occupies a variable path segment slot named playerId.
http://api.soccer.restapi.org/games/3fd65a60-cb8b-11e0-9572-0800200c9a66 - The UUID value fills in the gameId variable.
```

* Rule: CRUD function names should not be used in URIs 
```xml
For example, this API interaction design is preferred:
DELETE /users/1234

The following anti-patterns exemplify what not to do:
GET /deleteUser?id=1234
GET /deleteUser/1234
DELETE /deleteUser/1234
POST /users/1234/delete
```

## URI Query Design 
As a component of a URI, the query contributes to the unique identification of a resource.
Consider the following example:
http://api.college.restapi.org/students/morgan/send-sms - The URI of a controller resource that sends an sms message.
http://api.college.restapi.org/students/morgan/send-sms?text=hello - The URI of a controller resource that sends an sms message with a text value of hello

* Rule: The query component of a URI may be used to filter collections or stores 
```xml
 Let’s take a look at an example:
GET /users - The response message’s state representation contains a listing of all the users in the  collection.
GET /users?role=admin - The response message’s state representation contains a filtered list of all the users in the collection with a “role” value of admin.
```
* Rule: The query component of a URI should be used to paginate collection or store results 
```xml
GET /users?pageSize=25&pageStartIndex=50

```

# Interaction Design with HTTP 
## Request Methods 
* Rule: GET and POST must not be used to tunnel other request methods 
* Rule: GET must be used to retrieve a representation of a resource 
* Rule: HEAD should be used to retrieve response headers 
* Rule: PUT must be used to both insert and update a stored resource 
* Rule: PUT must be used to update mutable resources 
* Rule: POST must be used to create a new resource in a collection 
* Rule: POST must be used to execute controllers 
* Rule: DELETE must be used to remove a resource from its parent 
* Rule: OPTIONS should be used to retrieve metadata that describes a  resource’s available interactions 
```xml
```

## Response Status Codes
* Rule: 200 (“OK”) should be used to indicate nonspecific success 
* Rule: 200 (“OK”) must not be used to communicate errors in the response body 
* Rule: 201 (“Created”) must be used to indicate successful resource creation 
* Rule: 202 (“Accepted”) must be used to indicate successful start of an asynchronous action 
* Rule: 204 (“No Content”) should be used when the response body is intentionally empty 
* Rule: 301 (“Moved Permanently”) should be used to relocate resources 
* Rule: 302 (“Found”) should not be used 
* Rule: 303 (“See Other”) should be used to refer the client to a different URI 
* Rule: 304 (“Not Modified”) should be used to preserve bandwidth 
* Rule: 307 (“Temporary Redirect”) should be used to tell clients to resubmit the request to another URI 
* Rule: 400 (“Bad Request”) may be used to indicate nonspecific failure 
* Rule: 401 (“Unauthorized”) must be used when there is a problem with the client’s credentials 
* Rule: 403 (“Forbidden”) should be used to forbid access regardless of authorization state 
* Rule: 404 (“Not Found”) must be used when a client’s URI cannot be mapped to a resource 
* Rule: 405 (“Method Not Allowed”) must be used when the HTTP method is not supported 
* Rule: 406 (“Not Acceptable”) must be used when the requested media type cannot be served 
* Rule: 409 (“Conflict”) should be used to indicate a violation of resource state 
* Rule: 412 (“Precondition Failed”) should be used to support conditional operations 
* Rule: 415 (“Unsupported Media Type”) must be used when the media type of a request’s payload cannot be processed 
* Rule: 500 (“Internal Server Error”) should be used to indicate API malfunction

# Metadata Design
## HTTP Headers 
* Rule: Content-Type must be used 
* Rule: Content-Length should be used 
* Rule: Last-Modified should be used in responses 
* Rule: ETag should be used in responses 
* Rule: Stores must support conditional PUT requests 
* Rule: Location must be used to specify the URI of a newly created resource
* Rule: Cache-Control, Expires, and Date response headers should be used to encourage caching
* Rule: Cache-Control, Expires, and Pragma response headers may be used to discourage caching 
* Rule: Caching should be encouraged 
* Rule: Expiration caching headers should be used with 200 (“OK”) responses
* Rule: Expiration caching headers may optionally be used with 3xx and 4xx responses 38
* Rule: Custom HTTP headers must not be used to change the behavior of HTTP methods

## Media Type Design 
* Rule: Application-specific media types should be used 
* Rule: Media type negotiation should be supported when multiple representations are available 
* Rule: Media type selection using a query parameter may be supported 


# Representation Design
## Message Body Format 
* Rule: JSON should be supported for resource representation 
* Rule: JSON must be well-formed 
* Rule: XML and other formats may optionally be used for resource representation
* Rule: Additional envelopes must not be created 

## Hypermedia Representation 
* Rule: A consistent form should be used to represent links 
* Rule: A consistent form should be used to represent link relations 
* Rule: A consistent form should be used to advertise links 
* Rule: A self link should be included in response message body representations
* Rule: Minimize the number of advertised “entry point” API URIs 54
* Rule: Links should be used to advertise a resource’s available actions in a state-sensitive manner 

## Media Type Representation 
* Rule: A consistent form should be used to represent media type formats 
* Rule: A consistent form should be used to represent media type schemas 

## Error Representation 
* Rule: A consistent form should be used to represent errors
* Rule: A consistent form should be used to represent error responses
* Rule: Consistent error types should be used for common error conditions


# Client Concerns 
## Versioning
* Rule: New URIs should be used to introduce new concepts 
* Rule: Schemas should be used to manage representational form versions 
* Rule: Entity tags should be used to manage representational state versions 
## Security 
* Rule: OAuth may be used to protect resources 
* Rule: API management solutions may be used to protect resources 
## Response Representation Composition 
* Rule: The query component of a URI should be used to support partial responses 
* Rule: The query component of a URI should be used to embed linked resources 
## JavaScript Clients 
* Rule: JSONP should be supported to provide multi-origin read access from JavaScript 
* Rule: CORS should be supported to provide multi-origin read/write access from JavaScript


Notes from the my favorite book REST API by Mark Masse
