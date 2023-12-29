# What is a REST API?

A REST API is an application programming interface architecture style that conforms to specific architectural constraints, like stateless communication and cacheable data. It is not a protocol or standard. While REST APIs can be accessed through a number of communication protocols, most commonly, they are called over HTTPS, so the guidelines below apply to REST API endpoints that will be called over the internet.

# Use nouns instead of verbs in endpoint paths
We shouldn't use verbs in our endpoint paths. Instead, we should use the nouns which represent the entity that the endpoint that we're retrieving or manipulating as the pathname.

This is because our HTTP request method already has the verb. Having verbs in our API endpoint paths isn’t useful and it makes it unnecessarily long since it doesn’t convey any new information. The chosen verbs could vary by the developer’s whim. For instance, some like ‘get’ and some like ‘retrieve’, so it’s just better to let the HTTP GET verb tell us what and endpoint does.

The action should be indicated by the HTTP request method that we're making. The most common methods include GET, POST, PUT, and DELETE.

GET retrieves resources.
POST submits new data to the server.
PUT updates existing data.
DELETE removes data.
The verbs map to CRUD operations.

With the two principles we discussed above in mind, we should create routes like GET /articles/ for getting news articles. Likewise, POST /articles/ is for adding a new article , PUT /articles/:id is for updating the article with the given id. DELETE /articles/:id is for deleting an existing article with the given ID.

/articles represents a REST API resource. For instance, we can use Express to add the following endpoints for manipulate articles as follows: