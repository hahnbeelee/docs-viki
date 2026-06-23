# Source: https://docs.developer.yelp.com/docs/graphql-basic-usage

In GraphQL, a [query document](https://graphql.org/learn/queries/) is the string you send to the server to process and request data. It’s a read-only operation so you cannot create or manipulate data with it.

The query tells the server what it needs to do, but the fields are what the server uses to identify what data to return. These are usually represented as [Objects](https://graphql.org/learn/schema/#object-types-and-fields) or [Scalars](https://graphql.org/learn/schema/#scalar-types).

A basic request to GraphQL will look like this:

JSON

`{     business(id: "yelp-san-francisco") {   # the query with an argument         name                               # a field that returns a scalar         id                                 # a field that returns a scalar         coordinates {                      # a field that returns an object             latitude                       # a field that returns a scalar             longitude                      # a field that returns a scalar         }     } }`

Each query will have a specific object that it returns and, based on the object the query returns, you can add or remove fields to match the specific data you care about to fit your specific use case.

GraphQL provides a powerful query language to very specifically tailor your request outside of just the simplest use case, like passing multiple queries in a single request. In some cases, you might already have a cached list of Yelp Business IDs and you’d want to make 1 request to fetch the data instead of multiple. Make sure to alias the calls so you can match the data returned with the query:

JSON

`{     b1: business(id: "yelp-san-francisco") {         name     }     b2: business(id: "garaje-san-francisco") {         name     } }`

Now, let’s say you’re making a lot of queries and repeating the same fields. [Fragments](https://graphql.org/learn/queries/#fragments) provide you with the ability to refactor your query a little bit to not repeat the same fields over and over again or to extract out commonly repeated fields. Without fragments:

JSON

`{     b1: business(id: "yelp-san-francisco") {         name         id         rating         review_count         photos     }     b2: business(id: "garaje-san-francisco") {         name         id         rating         review_count         photos     } }`

And with fragments:

JSON

`{     b1: business(id: "yelp-san-francisco") {         ...basicBizInfo     }     b2: business(id: "garaje-san-francisco") {         ...basicBizInfo     } }  fragment basicBizInfo on Business {     name     id     rating     review_count     photos }`

Updated over 3 years ago

---

### What’s Next

- [Making Requests](https://docs.developer.yelp.com/docs/graphql-making-requests)

Did this page help you?

Yes

No

Copy Page