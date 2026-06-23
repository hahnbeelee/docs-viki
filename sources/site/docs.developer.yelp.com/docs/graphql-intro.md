# Source: https://docs.developer.yelp.com/docs/graphql-intro

Looking for schema instead? [Click here](https://docs.developer.yelp.com/graphql)

[GraphQL](https://graphql.org/) is a query language for APIs. What does this mean for you? Unlike regular SOAP or REST APIs, GraphQL gives you the ultimate flexibility in being able to specify in your API requests specifically what data you need, and get back exactly that.

As a query language, it provides you with a lot of flexibility that most normal APIs will not. Without needing to recreate endpoints, you can provide developers with the same functionality as a bulk endpoint. Your queries will be cleaner and easier to understand by combining multiple queries into one request.

### 

What’s the difference between Yelp's GraphQL API and the regular API?

The regular API is very well structured and specifically defined. The endpoints have their set requests and responses and that’s what you get whether or not that matches your usage pattern. GraphQL let’s you control all of this so that the way you consume the data matches exactly what you need.

This is both a pro and a con. If your use case does not require all of the data, GraphQL can speed up your requests as we do less work on the server-side to fulfill those requests. Conversely, if you need all of the data in one request, your requests could slow down as we do more work to fulfill these requests.

The data itself returned from the regular API and GraphQL should be identical, with one caveat: we’re only returning 1 photo from GraphQL at the moment compared to 3 from the regular API.

### 

Should I use GraphQL over the regular API?

That’s up to you! If you’re someone who favors the ability to customize their requests to fit your specific use-case, GraphQL will be a good fit. GraphQL is still in beta period, which means that we can’t promise that it’s fully stable or that some of the existing implementation won’t change. If you’re not comfortable with finding a bug or two and making changes to your app to keep up with us, the regular API will be a better fit.

The regular API (Places) is not going away so you do not have to migrate your apps over if you do not want. GraphQL will remain in beta for a little while as we iron out the bugs and smooth things over. We don’t currently have a timeline for when GraphQL will be considered production-stable. For now, we’re going to limit GraphQL to 10,000 queries per day as we slowly ramp it up. If you use multiple queries in a single request, we will count each individual query called, so 3 uses of the business queries in a single request will count 3 off your total.

### 

How do I use Yelp’s GraphQL API?

First, you’ll need to create a client and join the beta program. Once you’ve done this, follow our instructions to authenticate against the API. Both GraphQL and the regular API use the same authentication both will be interchangeable inside your app.

After you’ve got your access token, you can start querying the API. Let’s get some info for a restaurant, Garaje:

Shell

`$ curl -X POST -H "Authorization: Bearer ACCESS_TOKEN" -H "Content-Type: application/graphql" https://api.yelp.com/v3/graphql --data ' {     business(id: "garaje-san-francisco") {         name         id         alias         rating         url     } }'`

You get the response:

JSON

`{     "data": {         "business": {             "name": "Garaje",             "id": "tnhfDv5Il8EaGSXZGiuQGg",             "alias": "garaje-san-francisco",             "rating": 4.5,             "url": "https://yelp.com/biz/garaje-san-francisco"         }     } }`

Your response should look exactly like what you passed in! To make it easier for you to experiment with different queries, we’ve setup [interactive graphql editor](https://docs.developer.yelp.com/graphql). 
To make the actual calls from this editor, you will need to pass the auth token in the following format in the headers section.

![864](https://files.readme.io/77beda4-Screen_Shot_2022-11-28_at_10.34.35_AM.png)

We’ve also provided many interactive examples all around our documentation.

Updated 10 months ago

---

### What’s Next

- [Basic Usage](https://docs.developer.yelp.com/docs/graphql-basic-usage)

Did this page help you?

Yes

No

Copy Page