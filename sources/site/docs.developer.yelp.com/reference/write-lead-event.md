# Source: https://docs.developer.yelp.com/reference/write-lead-event

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
> This endpoint is part of the Leads API, visit [Leads API](https://docs.developer.yelp.com/docs/leads-api) to learn more.

ID

string

required

The Yelp Lead ID

Request body for creating an event.

The request object of the POST /v3/leads/{lead\_id}/events endpoint

request\_content

string

required

The actual content of the event. This must be a non empty string.

request\_type

string

enum

required

The content type of the event. Only "TEXT" is supported right now.

TEXT

Allowed:

`TEXT`

# 

201

The event was successfully writen.

# 

400

This error is returned in any of the following scenarios:

- The provided ID in the URL is not recognized as a valid Yelp Lead ID.
- The same successive message was sent to the same lead within the last hour. Sending the same message multiple times without a consumer response is not allowed.
- One of the mandatory parameters is missing from the request body.
- One of the parameters in the request body has an invalid value.
- The message body is invalid.

| code | description |
| --- | --- |
| INVALID\_ID | "The ID provided is not valid". |
| SAME\_SUCCESSIVE\_MESSAGE | "Same successive message sent to the same lead within the last hour. Wait for a consumer response or send a different message." |
| BAD\_REQUEST | "The message body is invalid". |
| VALIDATION\_ERROR | "'request\_content' is a required property". |
| VALIDATION\_ERROR | "'request\_type' is a required property". |
| VALIDATION\_ERROR | "' does not match '\[\\\\S\\\\s\]+\[\\\\S\]+'". |
| VALIDATION\_ERROR | "'' is not one of \['TEXT'\]". |

# 

401

The API key has either expired or doesn't have the required scopes to query this endpoint.

| code | description |
| --- | --- |
| UNAUTHORIZED\_API\_KEY | The API key provided is not currently able to query this endpoint. |
| TOKEN\_INVALID | Invalid API key or authorization header. |

# 

403

This error is returned in any of the following scenarios:

- The business user has been blocked from creating an event in the lead.
- The business isn't currently advertising.
- The business user doesn't have access to the business.
- The customer has archived this project.

| code | description |
| --- | --- |
| NOT\_AUTHORIZED | "The user has been blocked" |
| NOT\_AUTHORIZED | "This customer has archived this project." |
| UNAUTHORIZED\_BUSINESS\_MINIMUM\_ADVERTISING | "You're not authorized to access this business as it does not meet minimum advertising requirements." |
| NO\_BUSINESS\_ACCESS | "You don't have access to this Business." |

# 

404

The Lead with the given ID was not found.

# 

429

You have either exceeded your daily quota, or have exceeded the queries-per-second limit for this endpoint. Try reducing the rate at which you make queries.

# 

500

Internal Server Error

Updated about 1 year ago

---

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

Bearer

xxxxxxxxxx

1

curl \--request POST \\

2

 \--url https://api.yelp.com/v3/leads/ID/events \\

3

 \--header 'accept: application/json' \\

4

 \--header 'content-type: application/json' \\

5

 \--data '

6

{

7

 "request\_type": "TEXT"

8

}

9

'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

201 - Success400 - Invalid Lead ID400 - Invalid Request Body401 - Unauthorized401 - Invalid Token403 - Business User Blocked403 - Business must be Advertising404 - Not Found429 - Rate limited500 - Internal Server Error

Updated about 1 year ago

---

Did this page help you?

Yes

No