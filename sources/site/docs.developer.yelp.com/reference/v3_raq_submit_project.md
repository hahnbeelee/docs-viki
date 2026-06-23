# Source: https://docs.developer.yelp.com/reference/v3_raq_submit_project

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

#### URL Expired

The URL for this request expired after 30 days.

Request body for submitting a quote request.

business\_id

string

The Yelp business ID to submit the quote request to.

job\_alias

string

required

The job alias for the quote request.

survey\_responses

array of objects

required

List of survey question responses.

survey\_responses\*

ADD object

submit\_to\_nearby\_businesses

boolean

required

Whether to submit quote request to nearby businesses. If business\_id is not provided, this will be set to true.

truefalse

customer\_info

object

required

Customer information for the quote request.

customer\_info object

# 

200

The quote request has been submitted successfully.

# 

400

Bad Request. Message varies depending on failure scenario

# 

401

The API key has either expired or doesn't have the required scopes to query this endpoint.

| code | description |
| --- | --- |
| UNAUTHORIZED\_API\_KEY | The API key provided is not currently able to query this endpoint. |
| TOKEN\_INVALID | Invalid API key or authorization header. |

# 

403

Authorization Error

# 

404

Resource Not Found

# 

429

You have either exceeded your daily quota, or have exceeded the queries-per-second limit for this endpoint. Try reducing the rate at which you make queries.

# 

500

Internal Server Error

Updated 5 months ago

---

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

xxxxxxxxxx

1

curl \--request POST \\

2

 \--url https://api.yelp.com/v3/projects \\

3

 \--header 'accept: application/json' \\

4

 \--header 'content-type: application/json' \\

5

 \--data '

6

{

7

 "submit\_to\_nearby\_businesses": true

8

}

9

'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200400 - Invalid Request401 - Unauthorized401 - Invalid Token403 - Authorization Error404 - Resource Not Found429 - Rate limited500 - Internal Server Error

Updated 5 months ago

---

Did this page help you?

Yes

No