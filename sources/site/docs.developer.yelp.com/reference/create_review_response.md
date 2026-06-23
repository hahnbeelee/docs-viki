# Source: https://docs.developer.yelp.com/reference/create_review_response

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

#### URL Expired

The URL for this request expired after 30 days.

> ## 📘
> 
> This endpoint is part of the Respond to Reviews API, visit [Respond to Reviews API](https://docs.developer.yelp.com/docs/respond-to-reviews-api-v2) to learn more.

review\_id

string

required

22-character unique ID of a review. Review IDs are usually obtained from the Yelp Places API Review endpoints, GraphQL API, or a Yelp Partner Feed.

response\_text

string

required

Response text (only UTF-8 characters, no emojis)

response\_type

string

enum

required

public\_comment

Allowed:

`public_comment`

# 

200

Successfully responded to the given review.

# 

400

There are multiple scenarios in which different errors can be returned.

## 

General Error Responses:

| id | description | http\_code |
| --- | --- | --- |
| INVALID\_REQUEST | Missing a required parameter or includes an unsupported parameter. | HTTPBadRequest (400) |
| INSUFFICIENT\_SCOPE | The request requires higher privileges than provided by the access token. | HTTPBadRequest (400) |
| R2R\_COMMENTS\_NOT\_ALLOWED | This location does not include the respond-to-reviews feature. Contact your Yelp sales exec to enable. | HTTPBadRequest (400) |

## 

Public R2R Error Responses:

| id | description | http\_code |
| --- | --- | --- |
| R2R\_PROBLEM\_WITH\_USER\_PHOTO | Photo is missing, unacceptable, or pending. (A business owner needs to upload their own photo on biz.yelp.com - a valid photo is required in order to use R2R API.) | HTTPBadRequest (400) |
| R2R\_UNACCEPTABLE\_BIZ\_USER\_NAME | Unacceptable biz user name. | HTTPBadRequest (400) |
| R2R\_REVIEW\_DOES\_NOT\_EXIST | Review does not exist. | HTTPBadRequest (400) |
| R2R\_INVALID\_RESPONSE\_TYPE | Invalid response type. | HTTPBadRequest (400) |
| R2R\_INVALID\_RESPONSE\_TEXT | Invalid response text. (This error happens if the response is empty or exceeds 5K characters or has foul language or is too similar to a comment that's already been posted.) | HTTPBadRequest (400) |
| R2R\_PUBLIC\_COMMENTS\_DISABLED | Invalid response type. | HTTPBadRequest (400) |
| R2R\_BUSINESS\_NOT\_CLAIMED | Cannot determine the status of your business. | HTTPBadRequest (400) |
| R2R\_PERMISSION\_DENIED | You do not have permission to comment on that review. | HTTPBadRequest (400) |
| R2R\_COMMENT\_QUOTA\_EXCEEDED | You have made too many comments recently. (There is a maximum of 20 comments for each location per biz owner per day). | HTTPBadRequest (400) |

# 

401

This error is returned in any of the following scenarios:

| id | Description | http\_code |
| --- | --- | --- |
| INVALID\_TOKEN | The access token provided is expired, revoked, malformed, or invalid for other reasons | HTTPUnauthorized (401) |

Updated over 2 years ago

---

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

xxxxxxxxxx

1

curl \--request POST \\

2

 \--url https://partner-api.yelp.com/reviews/v1/review\_id \\

3

 \--header 'accept: application/json' \\

4

 \--header 'content-type: application/json' \\

5

 \--data '

6

{

7

 "response\_type": "public\_comment"

8

}

9

'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400 - Invalid Request400 - Invalid Response Type401 - Invalid Token

Updated over 2 years ago

---

Did this page help you?

Yes

No