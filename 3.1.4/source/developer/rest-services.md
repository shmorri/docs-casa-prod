# REST Services

Plugin developers can add RESTful web services to Casa easily. Simply create your resource classes and use JAX-RS annotations such as `@Path`, `@GET`, `@POST`, etc. so when a plugin is started all endpoints are dynamically added.

In summary, the following is required to add a RESTful service:

1. Create a class in your plugin (any package and file name is fine)
1. Annotate the class with `javax.ws.rs.Path` and supply a value for the annotation
1. Annotate the class with `org.gluu.casa.rest.RSResourceScope` if you want to specify whether the resource should be treated as a singleton or a new instance should be created upon every request. If not used, default behavior will be "singleton"
1. Add methods with annotations such as `@Path`, `@GET`, `@POST`, etc. (i.e. implement your service)

Services created this way will be available at the URL

```
https://<host>/casa/rest/pl/<plugin-id>/<path>
```

where `path` is the value supplied in step 2.

## Protection

By default, all services are anonymously accessible. In case you want to protect your endpoints, Casa allows you to do so by means of an OAuth token, that is, clients of the service must pass in the Authorization header of HTTP requests a valid bearer token. Such token must be obtained via an OpenID client registered in the underlying Gluu Server.

!!! Note:
    Registering OpenID clients and getting access tokens is out of the scope of this document, but you can check [this](https://tools.ietf.org/html/rfc6750) for a quick start.

To make a method protected, simply add the annotation `org.gluu.casa.rest.ProtectedApi` to it.

The following HTTP status codes can be arise when using protected methods:

- FORBIDDEN (403): This will arise when access was attempted to a protected endpoint but no token was passed.

- UNAUTHORIZED (401): The token passed was invalid (it has expired for instance). To handle this, clients of the service should re-request an access token (e.g. with a refresh token), and retry accessing the endpoint.
