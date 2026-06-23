# Source: https://docs.developer.yelp.com/docs/places-faq

**What is the Yelp Places API?**

The Yelp Places API gives developers access to Yelp’s wealth of high quality local content and search capabilities for millions of businesses.

 

**How can I get started using the Yelp Places API?**

Getting started with the Yelp Places API is easy! Simply visit our [sign-up page](https://business.yelp.com/data/products/places-api/). Here you can browse available plans, select the one that fits your needs, and get started quickly.

Please note that you need a Yelp user account. If you don’t already have an account, please visit our [registration page](https://www.yelp.com/signup). If you are a Yelp Business Owner Account user, please note this is different from a regular Yelp user account and you must be logged out of your [Yelp Business Owner account](https://biz.yelp.com/) in order to sign up for the API.

 

**How do I ask questions and provide feedback?**

Open and participate in issues at our [GitHub page](https://github.com/Yelp/yelp-fusion/issues). You can also reach out to [data-licensing@yelp.com](mailto:api@yelp.com).

 

**How many API requests do I receive?**

**Trial Plan:** You get up to 5,000 free API calls during your 30-day trial. These API calls are **STRICTLY FOR EVALUATION AND NOT FOR COMMERCIAL DEPLOYMENT**.

**Paid Plans:** Your plan includes 30,000 API calls per month by default, with a daily limit of up to 5,000 calls. Usage beyond 30,000 calls is billed in increments of 1,000 calls.

> ## 📘
> 
> If you need to raise the daily quota, book a meeting [here](https://business.yelp.com/data/#form) to discuss your needs with our sales team.

 

**What happens if I exceed my daily limit?**

Any additional requests on the same day will return a 429 (Too Many Requests) error. Limits reset at midnight UTC every day.

If you are already in the trial program, you can continue access by [upgrading to a paid plan](https://www.yelp.com/developers/v3/payment). If you require more than 150,000 API calls, [book a meeting](https://business.yelp.com/data/#form) to discuss your needs with our sales team.

 

**What can I do if I want to purchase a different plan than the one I’m currently trialing?**

At this time, there isn’t a direct way to switch plans during your trial. We’re sorry for the inconvenience! You can however do one of the following:

**Option 1:** Email us at [data-licensing@yelp.com](mailto:fusion@yelp.com), and we can assist with changing your plan. 
**Option 2:** Sign up for the new plan using a different Yelp consumer account.

We appreciate your patience as we work to improve this process!

 

**How can I check how many remaining API calls I have left?**

You can view your remaining calls by visiting the [Manage App page](https://www.yelp.com/developers/v3/manage_app) or checking the header of each response. Please see the [Places API Rate Limiting documentation](https://docs.developer.yelp.com/docs/fusion-rate-limiting) for more details.

 

**How much does it cost to use the Yelp API?**

Yelp offers different pricing plans for the Yelp Places API. You can find more information about pricing and included API calls on our [sign-up page](https://business.yelp.com/data/products/places-api/). You can also reach out to our sales team [here](https://business.yelp.com/data/#form) to set up a discussion.

 

**How do I transition from an evaluation license to a commercial license?**

If you are already in the trial program, you can continue access by upgrading to a paid plan [here](https://www.yelp.com/developers/v3/payment). This plan includes 30,000 API calls per month by default, with a daily limit of up to 5,000 calls. Usage beyond 30,000 calls is billed in increments of 1,000 calls.

If you need to raise the daily quota, book a meeting [here](https://business.yelp.com/data/#form) to discuss your needs with our sales team.

 

**Can I cache data from the API?**

You may cache Yelp Places API content for a maximum of 24 hours. Yelp Business IDs can be stored indefinitely.

 

**Can my organization commercially analyze the data I receive from its API credentials?**

Analysis is not permitted for Yelp Places integrations. Visit the [Yelp Insights API](https://business.yelp.com/data/products/insights-api/) website to learn more about supported use cases.

 

**What locales does the API support?**

The Yelp API supports numerous locales using the locale parameter. [Here](https://docs.developer.yelp.com/docs/resources-supported-locales) is the list of supported locales.

 

**Why does the API not return some businesses that I can find on Yelp?**

We only return businesses which have Yelp user-generated content added to them or have been updated by Yelp users. Specifically, any listing must have at least one review, photo, or other user-contributed enhancement.

 

**How can I get access to full review text?**

The Yelp Places API does not return full review text. Three review excerpts from individual business of approximately 160 characters each are returned by default from each [Reviews API](https://docs.developer.yelp.com/reference/v3_business_reviews) endpoint request.

 

**Can I change which reviews are returned for an API query?**

No, the Yelp Places API cannot be configured to return alternative or hand-picked review excerpts. In order to maintain a consistent Yelp experience across all platforms, a variety of factors are considered in order to determine and return a business’s top review excerpts. The sort order is based on recency, user voting, and other review quality factors to help consumers make informed decisions.

 

**Can I get coordinates of a business through the API?**

Yes, the large majority of businesses returned by Yelp Places API endpoints will have coordinates (latitude and longitude).

 

**How do I filter by country?**

The Yelp Places API returns results from all geographies where Yelp is available. To filter results to a specific city, make sure you use the location parameter when using [Search API](https://docs.developer.yelp.com/reference/v3_business_search).

 

**What’s the best way to match a specific business?**

We offer a few options for business matching based what data you have to match. If you know the business name and address information, you can use the [business match API](https://docs.developer.yelp.com/reference/v3_business_match). If you have a phone number, you can use the [phone search API](https://docs.developer.yelp.com/reference/v3_business_phone_search). You can also use the [autocomplete API](https://docs.developer.yelp.com/reference/v3_autocomplete) to provide suggestions for businesses, keywords and categories.

 

**Where can I get high resolution versions of the Yelp stars and logos?**

Please visit the [Yelp Display Requirements](https://www.yelp.com/developers/display_requirements) and [Yelp Brand](https://yelp.com/brand) websites.

 

**How do I get more than 50 results per request and more than 240 businesses per originating Search API query?**

The Search API endpoint returns up to 240 results from your originating query and up to 50 results per individual Search API request. Use the offset parameter to get the next page of results.

To use the offset parameter, give it any number. If you specify **limit=50** you'll get results 1 through 50. Further, specify **offset=51** and you'll get results 51 through 100.

 

**What image resolution options do you offer for business photos and user profile photos?**

By default, we return the original full-sized resolution; we use 'o' for business photos from the [Business Details](https://docs.developer.yelp.com/reference/v3_business_info) endpoint and 'o' for user profile photos (image\_url) in the Reviews endpoint. Here are the different resolutions we currently provide:

- 'o' (original): Up to 1,000x1,000
- 'l' (large): Up to 600x400
- 'm' (medium): Up to 100x100
- 'ms' (medium square): 100x100
- 's' (small): Up to 40x40
- 'ss' (small square): 40x40

That said, do keep in mind that sizing is not always consistent because users upload images at different resolutions.

 

**What's the difference between the Yelp business ID and business alias?**

Every Yelp business has both a unique ID, such as **4kMBvIEWPxWkWKFN\_\_8SxQ**, as well as a unique alias, such as **yelp-san-francisco**. Both are returned for every business in any endpoint that returns business information. Generally, business ID and business alias are interchangeable methods of identifying a Yelp Business.

The business alias is more human-readable, but often longer, than the business ID. The business alias may also contain unicode characters, so it is recommended to use the business ID whenever possible.

 

**There are many more business attributes on Yelp's website and mobile app than are listed in the API documentation here. How do I access them?**

Yelp’s success is built on our first class data for local businesses, so we are careful with which data fields we expose via our API. If you are building an app that could benefit from additional Yelp features or data, please apply for a [Yelp Places Enterprise](https://fusion.yelp.com/enterprise/) license and share your commercial project with us in more detail.

 

**What is Yelp's GraphQL API?**

Let's first explain GraphQL - it is a query language for APIs that places emphasis on being able to query for exactly the data you want. GraphQL gives you the ultimate flexibility in being able to specify in your API requests specifically what data you need, and get back exactly that. The Yelp GraphQL API will allow you to customize the request and responses when retrieving Yelp data.

For more information, check out our [blog post](https://engineeringblog.yelp.com/2017/05/introducing-yelps-local-graph.html) and [GraphQL Intro page](https://docs.developer.yelp.com/docs/graphql-intro).

 

**How do I sign up for access to Yelp's GraphQL API?**

GraphQL is part of the Yelp Developer Beta program which grants developers early access to new and experimental features. To sign up for the Developer Beta program, go to the [Manage App](https://www.yelp.com/developers/v3/manage_app) page and click the Join button. 
 

Copy Page