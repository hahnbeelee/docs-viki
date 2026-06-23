# Source: https://docs.developer.yelp.com/docs/places-intro

The Yelp Places API allows you to get the best local content and user reviews from millions of businesses around the world. This tutorial provides an overview of the capabilities our suite of APIs offer, provides instructions for how to authenticate API calls, and walks through a simple scenario using the API.

Learn more about the full suite of Data Licensing products, features and use-cases [here](https://business.yelp.com/data)

### 

Plan and Pricing

Choose a plan that fits your development needs and start your free trial [here](https://business.yelp.com/data/products/fusion/)

### 

Authentication

The Yelp Places API uses private key authentication to authenticate all endpoints. Your private API Key will be automatically generated after you create your app. For detailed instructions, refer to our [authentication guide](https://docs.developer.yelp.com/docs/fusion-authentication).

### 

Endpoints

All Yelp Places API endpoints are under `https://api.yelp.com/v3`. Below are current Yelp Fusion API endpoints. Click the links for detailed documentation.

You can also find small code samples for Node.js, Python, Ruby, and other languages at [Yelp Places Code Samples on Github](https://github.com/Yelp/yelp-fusion#code-samples).

#### 

Businesses

| Name | Path | Description |
| --- | --- | --- |
| Business Search | [/businesses/search](https://docs.developer.yelp.com/reference/v3_business_search) | Search for businesses by keyword, category, location, price level, etc. |
| Phone Search | [/businesses/search/phone](https://docs.developer.yelp.com/reference/v3_business_phone_search) | Search for businesses by phone number. |
| Business Match | [/businesses/matches](https://docs.developer.yelp.com/reference/v3_business_match) | Find the Yelp business that matches an exact input location. Use this to match business data from other sources with Yelp businesses. |
| Business Details | [/businesses/{id}](https://docs.developer.yelp.com/reference/v3_business_info) | Get rich business data, such as name, address, phone number, photos, Yelp rating, price levels and hours of operation. |
| Transaction Search | [/transactions/{transaction\_type}/search](https://docs.developer.yelp.com/reference/v3_transaction_search) | Search for businesses which support food delivery transactions. |
| Business Engagement Metrics | [businesses/engagement](https://docs.developer.yelp.com/reference/v3_get_businesses_engagement) | Get engagement metrics information for the provided businesses. |
| Business Service Offerings | [/businesses/{business\_id\_or\_alias}/service\_offerings](https://docs.developer.yelp.com/reference/v3_business_service_offerings) | Get active and eligible service offerings for a business. |

#### 

Reviews

| Name | Path | Description |
| --- | --- | --- |
| Reviews (up to 3 excerpts) | [/businesses/{business\_id\_or\_alias}/reviews](https://docs.developer.yelp.com/reference/v3_business_reviews) | Get up to three review excerpts for a business. |
| Review Highlights | [/businesses/{business\_id\_or\_alias}/review\_highlights](https://docs.developer.yelp.com/reference/v3_business_review_highlights) | Get a business's review highlights. |

#### 

Events

| Name | Path | Description |
| --- | --- | --- |
| Events Search | [/events](https://docs.developer.yelp.com/reference/v3_events_search) | Get events that match search criteria. |
| Event Lookup | [/events/{event\_id}](https://docs.developer.yelp.com/reference/v3_event) | Get the detailed information of a Yelp event. 
Get the event ID from `/events` or `/events/featured`. |
| Featured Event | [/events/featured](https://docs.developer.yelp.com/reference/v3_featured_event) | Get the featured event for a given location. Featured events are chosen by Yelp's community managers. |

#### 

Categories

| Name | Path | Description |
| --- | --- | --- |
| Category Search | [/categories](https://docs.developer.yelp.com/reference/v3_all_categories) | Get all Yelp business categories across all locales. |
| Category Search by Alias | [/categories/{alias}](https://docs.developer.yelp.com/reference/v3_categories) | Get detailed information about the Yelp category specified by a Yelp category alias. 
The alias for each category can be found either by using the `/v3/categories` endpoint, or the [category list](https://docs.developer.yelp.com/docs/resources-categories). |

#### 

Miscellaneous

| Name | Path | Description |
| --- | --- | --- |
| Autocomplete | [/autocomplete](https://docs.developer.yelp.com/reference/v3_autocomplete) | Provide autocomplete suggestions for businesses, search keywords and categories. |

### 

Using the API

Let's use a simple scenario to demonstrate how to use the Yelp Places API. Imagine you are building an app to help people find great food nearby and you want to provide a search experience.

1. A user enters "del" in the search box.
2. They are provided a few autocomplete suggestions, like "delivery" and "delis".
3. They choose "delis" to see what options they have nearby.
4. They choose "delivery" since they do not want to go out to get the food.
5. They are offered a list of all the restaurants which deliver to their location.
6. They choose one, view the restaurant details and reviews, then make the decision to order delivery.

The following is how you can use the Yelp Places API to implement this experience.

#### 

Get autocomplete suggestions based on user's input

As the user is typing, you can monitor the user's input and call our autocomplete endpoint in real time. It's always good to also provide the latitude and longitude parameters so that you receive suggestions on businesses based on location.

Shell

`GET https://api.yelp.com/v3/autocomplete?text=del&latitude=37.786882&longitude=-122.399972`

In the response body below, you can see that it's returning suggestions for terms, businesses and categories.

JSON

`{   "terms": [     {       "text": "Delivery"     }   ],   "businesses": [     {       "id": "YqvoyaNvtoC8N5dA8pD2JA",       "name": "Delfina"     },     {       "id": "vu6PlPyKptsT6oEq50qOzA",       "name": "Delarosa"     },     {       "id": "bai6umLcCNy9cXql0Js2RQ",       "name": "Pizzeria Delfina"     }   ],   "categories": [     {       "alias": "delis",       "title": "Delis"     },     {       "alias": "fooddeliveryservices",       "title": "Food Delivery Services"     },     {       "alias": "couriers",       "title": "Couriers & Delivery Services"     }   ] }`

#### 

Search for businesses with a keyword

Once the user selects "delis" from the autocomplete suggestions as the search keyword, you can call the Search endpoint to find restaurants matching the keyword. Again, by providing the latitude and longitude parameters, you'll get the best results which take location into consideration.

Shell

`GET https://api.yelp.com/v3/businesses/search?term=delis&latitude=37.786882&longitude=-122.399972`

In the response body below, you'll get a list of businesses with valuable information such as name, address, phone number, Yelp rating, price levels, and review counts. The URL of the restaurant points the corresponding Yelp business page. Deeplinks ensure that the Yelp mobile app opens to the desired page, if installed. If not installed, users are taken to Yelp's mobile website.

JSON

`{   "total": 1316,   "businesses": [     {       "rating": 4.5,       "price": "$$",       "phone": "+14154212337",       "id": "molinari-delicatessen-san-francisco",       "categories": [         {           "alias": "delis",           "title": "Delis"         }       ],       "review_count": 910,       "name": "Molinari Delicatessen",       "url": "https://www.yelp.com/biz/molinari-delicatessen-san-francisco",       "coordinates": {         "latitude": 37.7983818054199,         "longitude": -122.407821655273       },       "image_url": "http://s3-media4.fl.yelpcdn.com/bphoto/6He-NlZrAv2mDV-yg6jW3g/o.jpg",       "location": {         "city": "San Francisco",         "country": "US",         "address2": "",         "address3": "",         "state": "CA",         "address1": "373 Columbus Ave",         "zip_code": "94133"       }     },     // ...   ] }`

#### 

Search for businesses supporting delivery

Once the user selects "Delivery" from the autocomplete suggestions as the search keyword, you can call the Transaction Search endpoint to find businesses which deliver to the user's location. Here the latitude and longitude parameters are required since delivery availability depends on the location of the delivery. You can also pass in a different location to implement the case where the user will request delivery from a different location.

Shell

`GET https://api.yelp.com/v3/transactions/delivery/search?latitude=37.786882&longitude=-122.399972`

The response body right now is pretty much the same as search endpoint response body.

JSON

`{   "total": 25,   "businesses": [     {       "rating": 4,       "image_url": "",       "name": "North India Restaurant",       "url": "https://www.yelp.com/biz/north-india-restaurant-san-francisco",       "review_count": 551,       "coordinates": {         "latitude": null,         "longitude": null       },       "id": "north-india-restaurant-san-francisco",       "categories": [         {           "alias": "indpak",           "title": "Indian"         }       ]     },     // ...   ] }`

#### 

Get business details and reviews

Finally, you can call the Business Details endpoint and Reviews endpoint to retrieve business details and up to 3 review excerpts.

To get business detail information, you can make the following call.

Shell

`GET https://api.yelp.com/v3/businesses/north-india-restaurant-san-francisco`

In the response body right now, you'll get up to 3 additional photos and hours of the business.

JSON

`{   "rating": 4,   "price": "$$",   "hours": [     {       "hours_type": "REGULAR",       "open": [         {           "is_overnight": false,           "end": "2300",           "day": 0,           "start": "1000"         },         {           "is_overnight": false,           "end": "2300",           "day": 1,           "start": "1000"         },         {           "is_overnight": false,           "end": "2300",           "day": 2,           "start": "1000"         },         {           "is_overnight": false,           "end": "2300",           "day": 3,           "start": "1000"         },         {           "is_overnight": false,           "end": "0000",           "day": 4,           "start": "1000"         },         {           "is_overnight": false,           "end": "0000",           "day": 5,           "start": "1000"         },         {           "is_overnight": false,           "end": "2300",           "day": 6,           "start": "1000"         }       ],       "is_open_now": true     }   ],   "photos": [     "http://s3-media4.fl.yelpcdn.com/bphoto/howYvOKNPXU9A5KUahEXLA/o.jpg",     "http://s3-media3.fl.yelpcdn.com/bphoto/I-CX8nioj3_ybAAYmhZcYg/o.jpg",     "http://s3-media2.fl.yelpcdn.com/bphoto/uaSNfzJUiFDzMeSCwTcs-A/o.jpg"   ],   "id": "north-india-restaurant-san-francisco",   "categories": [     {       "alias": "indpak",       "title": "Indian"     }   ],   "review_count": 551,   "name": "North India Restaurant",   "url": "https://www.yelp.com/biz/north-india-restaurant-san-francisco",   "coordinates": {     "latitude": 37.787789124691,     "longitude": -122.399305736113   },   "image_url": "https://s3-media1.fl.yelpcdn.com/bphoto/howYvOKNPXU9A5KUahEXLA/o.jpg",   "location": {     "city": "San Francisco",     "country": "US",     "address2": "",     "address3": "",     "state": "CA",     "address1": "123 Second St",     "zip_code": ""   } }`

To get reviews of the business, you can make the following call.

Shell

`GET https://api.yelp.com/v3/businesses/north-india-restaurant-san-francisco/reviews`

In the response body, you can retrieve up to three review excerpts, the URL to the full review, the Yelp rating with each review excerpt as well as the name and profile photo of the reviewer.

JSON

`{   "reviews": [     {       "url": "https://www.yelp.com/biz/north-india-restaurant-san-francisco?hrid=AeVAkQgueu6JtYtU4r3Jrg",       "text": "This place is really pretty and I really love this place. My friends and me came here yesterday. The food is superb, the service is impeccable (mostly) and...",       "user": {         "image_url": "",         "name": "Hoang V."       },       "rating": 5     },     {       "url": "https://www.yelp.com/biz/north-india-restaurant-san-francisco?hrid=6tsz9tl7HAiOcYj_fGrsCg",       "text": "Went there for the first time Saturday Evening,everything is great, the ambiance is outstanding for this location, tried the mulliatawny soup for starters...",       "user": {         "image_url": "http://s3-media2.fl.yelpcdn.com/photo/O1ZuPKBhwxHAT60XZksWHQ/o.jpg",         "name": "Winston P."       },       "rating": 5     },     {       "url": "https://www.yelp.com/biz/north-india-restaurant-san-francisco?hrid=3b3-zDKfomV-1qR3Z0jmQw",       "text": "I came in here for the $9.95 lunch buffet the day after it opened.  It is the old Tara space and I like how it has been opened up to accommodate many more...",       "user": {         "image_url": "http://s3-media1.fl.yelpcdn.com/photo/bQRonQWaxInb7eKAtMjf3A/o.jpg",         "name": "Ronita J."       },       "rating": 4     }   ],   "total": 3 }`

### 

What's next

Now you've learned how to use our API endpoints to get the best local business content, user reviews, and more. We can't wait to learn about your product as you start building.

- To inquire about a commercial use case in your consumer product, please complete a [Yelp Places Enterprise](https://fusion.yelp.com/enterprise/) application.
- To provide feedback or report an issue, please go to [https://github.com/Yelp/yelp-fusion/issues](https://github.com/Yelp/yelp-fusion/issues).
- To tell us about your apps and ideas, please email [api@yelp.com](mailto:api@yelp.com).
- Also, be sure to check out our [FAQ](https://docs.developer.yelp.com/docs/fusion-faq).

Copy Page