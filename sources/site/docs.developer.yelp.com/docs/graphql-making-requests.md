# Source: https://docs.developer.yelp.com/docs/graphql-making-requests

There are a few different ways to make requests into the GraphQL API:

- Using client libraries
- Sending JSON
- Sending raw GraphQL queries

## 

Using client libraries

Client libraries will provide you with the fastest and most comprehensive way to access the API and can assist in handling auth, formatting your requests and your responses.

The [Apollo](https://www.apollographql.com/docs) client libraries are available for:

- [React and React Native](https://www.apollographql.com/docs/react)
- [iOS](https://www.apollographql.com/docs/ios)
- [Kotlin](https://www.apollographql.com/docs/kotlin)
- [Angular](https://the-guild.dev/graphql/apollo-angular/docs)

Additional clients are available for:

- [Ruby](https://github.com/github/graphql-client)
- [Python](https://github.com/graphql-python/gql)

## 

Sending JSON

You can send your GraphQL requests as JSON to our API and have it correctly interpolate variables passed into it. To do so, set the "Content-Type" header to "application/json" and format the query as such:

GraphQL

`{     "query": "business(id: $business_name) {         name         id         rating         url     }",     "variables": {         "business_name": "garaje-san-francisco"     } }`

## 

Sending raw GraphQL queries

If you want to send raw GraphQL queries to the API, you can still do so but you must set the "Content-Type" header to "application/graphql". If you do not, the request will be interpreted as JSON and will fail.

GraphQL

`{     business(id: "garaje-san-francisco") {         name         id         rating         url     } }`

Updated over 3 years ago

---

### What’s Next

- [Rate Limiting](https://docs.developer.yelp.com/docs/graphql-rate-limiting)

Did this page help you?

Yes

No

Copy Page