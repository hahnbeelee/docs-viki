# Source: https://docs.developer.yelp.com/docs/graphql-localization

Unlike the regular Places API where you can localize your request through a request parameter, localization for GraphQL API happens by sending a header.

When you send your request to GraphQL, provide us with the [Accept-Language](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language) header. The GraphQL API supports the [same locales](https://docs.developer.yelp.com/docs/resources-supported-locales) our regular API does. You can only provide 1 locale per request, if you provide more we'll return a 400 Bad Request error with the code **INVALID\_LOCALE**.

### 

Example

Shell

`$ curl -X POST -H "Authorization: Bearer ACCESS_TOKEN" -H "Content-Type: application/graphql" -H "Accept-Language: en_US" --data ' {     business(id: "garaje-san-francisco") {         name         url     } }'`

Specifying the locale in the header is optional, if you do not provide one we will default to _en\_US_.

Updated 10 months ago

---

Copy Page