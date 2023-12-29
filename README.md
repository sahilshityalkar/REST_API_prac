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

# Use logical nesting on endpoints
When designing endpoints, it makes sense to group those that contain associated information. That is, if one object can contain another object, you should design the endpoint to reflect that. This is good practice regardless of whether your data is structured like this in your database. In fact, it may be advisable to avoid mirroring your database structure in your endpoints to avoid giving attackers unnecessary information.

For example, if we want an endpoint to get the comments for a news article, we should append the /comments path to the end of the /articles path. We can do that with the following code in Express:

```express
const express = require('express');
const bodyParser = require('body-parser');

const app = express();

app.use(bodyParser.json());

app.get('/articles/:articleId/comments', (req, res) => {
  const { articleId } = req.params;
  const comments = [];
  // code to get comments by articleId
  res.json(comments);
});


app.listen(3000, () => console.log('server started'));


In the code above, we can use the GET method on the path '/articles/:articleId/comments'. We get comments on the article identified by articleId and then return it in the response. We add 'comments' after the '/articles/:articleId' path segment to indicate that it's a child resource of /articles.

This makes sense since comments are the children objects of the articles, assuming each article has its own comments. Otherwise, it’s confusing to the user since this structure is generally accepted to be for accessing child objects. The same principle also applies to the POST, PUT, and DELETE endpoints. They can all use the same kind of nesting structure for the path names.

However, nesting can go too far. After about the second or third level, nested endpoints can get unwieldy. Consider, instead, returning the URL to those resources instead, especially if that data is not necessarily contained within the top level object.

For example, suppose you wanted to return the author of particular comments. You could use /articles/:articleId/comments/:commentId/author. But that's getting out of hand. Instead, return the URI for that particular user within the JSON response instead:

`"author": "/users/:userId"`
