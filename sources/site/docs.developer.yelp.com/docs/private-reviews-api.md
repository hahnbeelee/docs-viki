# Source: https://docs.developer.yelp.com/docs/private-reviews-api

> ## 📘
> 
> This is a Yelp Partner API
> 
> Access is disabled by default. See [Yelp Partner APIs](https://docs.developer.yelp.com/docs/yelp-partner-apis) on how to get access.

# 

Overview

The Yelp Private Reviews API provides a means for partners to retrieve reviews posted by consumers that are publicly viewable on Yelp. The exact number and sort of reviews available via this endpoint will be dictated by your partnership agreement. Access to this API is reserved for contracted Yelp partners. This API does not permit the viewing of private messages that are sent directly from consumers to businesses, the [Leads API](https://docs.developer.yelp.com/docs/leads-api) contains those private messages.

# 

Access and Credentials

Before the application client system can initiate a request for an access token, the system must register with Yelp as a client of our Private Reviews system. Upon registration, the client will be permitted access to this endpoint. Credentials can be generated [here](https://www.yelp.com/developers/v3/manage_app).

# 

Authentication

Refer [here](https://docs.developer.yelp.com/docs/fusion-authentication) for more about authentication for this API

# 

Request

Private Reviews API

`GET https://api.yelp.com/v3/private/businesses/{business_id}/reviews`

**Request parameter:**

- business\_ids
- locale

**Response parameters:**

| Name | Type | Description |
| --- | --- | --- |
| reviews | object\[\] | A list of reviews for this business. |
| time\_created | string | The time that the review was created in PDT. |
| id | string | A unique identifier for this review. |
| rating | int | Rating of this review. |
| text | string | Full-text content of this review. |
| url | string | URL of this review. |
| user | object\[\] | The user who wrote the review. |
| user.name | string | User screen name (first name and first initial of last name). |
| user.image\_url | string | URL of the user's profile photo. |
| public\_response | object\[\] | The response from the business owner. |
| public\_response.text | string | Full-text content of the review response. |
| public\_response.time\_created | string | The time that the review response was created. |
| public\_response.business\_user | object\[\] | The business user who responded to the review. |
| business\_user.name | string | The name of the business user (aliases like “Customer Support” are common) |
| business\_user.role | string | The role of the business user. Possible values are: 
OWNER, MANAGER, CUSTOMER SERVICE, or EMPLOYEE |
| business\_user.photo\_url | string | URL of the business user's profile photo. |

**Example Request**

Text

`GET https://api.yelp.com/v3/private/businesses/PerbRA5npIlclM0CmLLrbw/reviews?locale=en_US`

**Example Response**

Text

`{   "reviews": {     "review": [       {         "time_created": "2020-06-08 20:00:23",         "rating": 1,         "text": "The moment you walk inside the store you can tell about the \"dollar store\" quality of every single item.  The designs are so depressing and tasteless.",         "url": "https://www.yelp.com/biz/the-brick-vancouver-2?adjust_creative=Ey_LbvkpsGAECYM_cP_3Jw&hrid=QaXIVEd8brM89ctSg4inEw&utm_campaign=yelp_api_v3&utm_medium=api_v3_graphql&utm_source=Ey_LbvkpsGAECYM_cP_3Jw",         "user": {           "name": "Shannon W.",           "image_url": "https://s3-media1.fl.yelpcdn.com/photo/Y8eHsgY2emwWmUOk9TWnZg/o.jpg"         },         "public_response": {           "text": "Hello Shannon W.. From British Columbia, to the Northwest Territories and to Nova Scotia, there is a Brick team focused on saving you more. If you did not find the product that suits your needs in store, don't forget we have a wide variety of options to browse online. Thank you for taking the time to submit a review!",           "time_created": "2020-06-10T21:16:43+00:00",           "business_user": {             "name": "The Brick",             "role": "CUSTOMER_SERVICE",             "photo_url": "https://s3-media1.fl.yelpcdn.com/buphoto/GKx20wV9-mEucKDhsNXw4Q/o.jpg"           }         }       },       {         "time_created": "2009-10-11 10:43:28",         "rating": 2,         "text": "I wonder if someone in their marketing department told the Brick that by putting the word \"Urban\" in front of the store name, that it will make the furniture more appealing?\n\nHmmm, I think not!\n\nInstead of regular poor quality and unstylish furniture, this urban location now stocks poor quality and unstylish furniture that attempts to be more contemporary by having cleaner lines.  It doesn't work and it's still a terrible place to buy furniture.\n\nEverything here is mass produced and materials are terrible in quality - their leather is so cheap that it might as well be PVC.  I don't know if you can get quality below bonded leather, but this would be it.  Lamps are already wobbly in the store.  Sofas are stiff and have all the poor finishing features.\n\nThe Urban Brick is not any better than a regular Brick... you're honestly better off saving your pennies for a sale at a better quality store since I can't imagine having this style in any respectable urban Vancouver home.",         "url": "https://www.yelp.com/biz/the-brick-vancouver-2?adjust_creative=Ey_LbvkpsGAECYM_cP_3Jw&hrid=l7-yn4JLx7jSY8y8cmxgNg&utm_campaign=yelp_api_v3&utm_medium=api_v3_graphql&utm_source=Ey_LbvkpsGAECYM_cP_3Jw",         "user": {           "name": "Chris F.",           "image_url": "https://s3-media3.fl.yelpcdn.com/photo/nslinOHxl7qU3tLUZhLTsQ/o.jpg"         },         "public_response": null       }]}}`

Non-english reviews can be retrieved using either 'Accept-Language' header or locale request parameter. In case of a conflict between the two, locale is given preference. This value needs to be one of the Yelp supported locales => [https://www.yelp.com/developers/documentation/v3/supported\_locales](https://www.yelp.com/developers/documentation/v3/supported_locales)

API response will contain a header 'Content-Language' specifying the locale of the text in reviews.

Updated over 1 year ago

---

Did this page help you?

Yes

No

Copy Page