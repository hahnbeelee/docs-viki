# Source: https://docs.developer.yelp.com/reference/claim_business_v1

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

#### URL Expired

The URL for this request expired after 30 days.

Claim Request

`{   "businesses": [     {       "matching_criteria": {         "address1": "800 N Point St",         "address2": null,         "address3": null,         "city": "San Francisco",         "country": "US",         "latitude": 37.8058024,         "longitude": -122.420582,         "name": "Gary Danko",         "phone": "+14157492060",         "postal_code": "94109",         "state": "CA",         "yelp_business_id": "WavvLdjbuy6g8aZTtbBQHTw"       },       "options": {         "use_matching_criteria_for_update": "true"       },       "update": {         "partner_biz_claim": {           "owner_account": {             "first_name": "John",             "last_name": "Doe",             "email": "johndoe@gmail.com"           }         }       }     }   ] }`

> ## 📘
> 
> This endpoint is part of the SMB Claiming API, visit [SMB Claiming API](https://docs.developer.yelp.com/docs/claiming) to learn more.

Request body

matching\_criteria

object

required

matching\_criteria object

options

object

options object

update

object

Provides rich content for the business. Please use the table below for reference to all 'update' attributes.

update object

partner\_business\_id

string

Optional unique partner identifier for the business. Must not contain leading or trailing spaces. When provided, partner identifiers cannot change and must remain unique. Maximum length is 100.

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

curl \--request POST \\

2

 \--url https://partner-api.yelp.com/v1/ingest/create \\

3

 \--header 'accept: application/json' \\

4

 \--header 'content-type: application/json'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400 - Result

Updated over 2 years ago

---

Did this page help you?

Yes

No