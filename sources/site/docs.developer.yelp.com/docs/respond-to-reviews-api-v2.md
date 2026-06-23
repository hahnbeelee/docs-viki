# Source: https://docs.developer.yelp.com/docs/respond-to-reviews-api-v2

> ## 📘
> 
> This is a Yelp Partner API
> 
> Access is disabled by default. See [Yelp Partner APIs](https://docs.developer.yelp.com/docs/yelp-partner-apis) on how to get access.

# 

Overview

The Yelp Respond to Reviews (R2R) API is an external-facing API for Yelp partners to respond to business reviews. On the Yelp for Business Owners site, business owners can view and respond to reviews that are publicly viewable on Yelp.

# 

Video Demo

[Here](https://docs.google.com/videos/d/1Jg25A6WrusSSEBqki3EaOs2fOkRQoEsBUJRuOSwA3i8/edit?usp=sharing) is a 3-minute end-to-end demo showcasing all the features you need to implement.

# 

OAuth Authorization Workflow

[![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Guide to OAuth Authorization Workflow](https://docs.developer.yelp.com/docs/oauth-authorization-workflow)

# 

Yelp Policy for Respond to Reviews (R2R) API Partners

See [FAQs](https://docs.developer.yelp.com/docs/faqs) & [Policies](https://docs.developer.yelp.com/docs/policies).

# 

API Endpoints

## 

Respond to Review

[API Reference Docs for this endpoint](https://docs.developer.yelp.com/reference/create-review-response)

The access token assigned to the business user must be included in this request. This request also includes the actual response to a review. The {review\_id} is obtained from the Yelp Full-text Review API or a Yelp Partner Feed.

The client constructs the request by including the following parameters using the “application/json” format in the HTTP request entity-body. The access token must be included in the HTTP request header Authorization.

### 

Review Response Parameters

Request: 
`POST https://partner-api.yelp.com/reviews/v1/{review_id}`

| Parameter Name | Requirement | Description |
| --- | --- | --- |
| response\_text | Required | Response text in UTF-8 characters. Emojis are not currently supported in. |
| response\_type | Required | Response type - only possible value is `public_comment` |

### 

Retrieve information about the business owner associated with access token

[API Reference Docs for this endpoint](https://docs.developer.yelp.com/reference/retrieve-business-owner-information)

Request: 
`GET https://partner-api.yelp.com/v1/business_owner/me/profile`

Response:

Text

`{   "first_name": "Chris",   "last_name": "Sample",   "email": "chris.sample@companyname.com",   "position": "MANAGER",   "id": "ziUn,iIXzXAuv-hUpCOadA",   "photo_url": "https://s3-media0.fl.yelpcdn.com/buphoto/tTs_H5N5QtY7umnkv44VXA/ms.jpg" }`

### 

Error Codes and Resolutions

Here are the common error codes you can encounter when posting a business owners response.

| Error Code | Description and how to resolve. |
| --- | --- |
| Photo is missing, unacceptable, or pending. | Direct the business owner to [this page](https://biz.yelp.com/settings/photo?return_url=%2Fsettings) to add a new photo. If this is for an enterprise business, you can also submit this request through our shared escalations document. |
| Unacceptable biz user name. | Direct the business owner to [this page](https://biz.yelp.com/settings/profile) to update their business username. If this is for an enterprise business, you can also submit this request through our shared escalations document. |
| You do not have permission to comment on that review. | This means the business owner hasn't claimed the location whose review they're trying to respond to. To resolve: 1) if an enterprise location please add this claim request to our shared escalations doc or 2) if SMB either submit a claim request via our [claim API](https://docs.developer.yelp.com/docs/claiming) or direct the business owner [here](https://biz.yelp.com/business_name_and_location) to claim their page. |
| Review does not exist. | Double check that you have the right review\_id. This error could also be the result of the consumer deleting their review. |
| Review already has a comment by a different business user. | Reviews can only have one response on them. No action needed to resolve this error as the review has already been responded too |
| Internal Error | Something unexpected happened please retry the request or reach out to [partner-support@yelp.com](mailto:partner-support@yelp.com) if retries are unsuccessful. If you submit a response with emojis in it, that will also result in this error message, remove the emojis and retry. |
| This location does not include the respond-to-reviews feature. Contact your official Yelp Partner for more information. | This location hasn't been authorized for review response. Authorization is typically handled by the [location subscription api](https://docs.developer.yelp.com/docs/location-subscription-api-v2). To resolve this error please subscribe to this location. |
| Cannot determine the status of your business. | Please retry the request or reach out to [partner-support@yelp.com](mailto:partner-support@yelp.com) with relevant api request details. |
| You are not allowed to comment at this time. | You might've exceeded the 20 review responses per location per day limit. Wait then retry. |
| Invalid response text. | Double check the text you're sending. Review response text must be UTF-8. |

Copy Page