# Source: https://docs.developer.yelp.com/reference/get_partner_biz_claim_status_v1

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
> This endpoint is part of the SMB Claiming API, visit [SMB Claiming API](https://docs.developer.yelp.com/docs/claiming) to learn more.

job\_id

string

required

Identifier of the job as returned from the Ingestion `POST`

yelp\_business\_id

string

required

Yelp Business ID

# 

200

200

# 

400

400

Updated over 2 years ago

---

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

:

xxxxxxxxxx

1

curl \--request GET \\

2

 \--url https://partner-api.yelp.com/v2/partner\_biz\_claim/request/status \\

3

 \--header 'accept: application/json'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400 - Result

Updated over 2 years ago

---

Did this page help you?

Yes

No