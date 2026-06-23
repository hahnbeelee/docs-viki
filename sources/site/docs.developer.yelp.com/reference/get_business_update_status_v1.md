# Source: https://docs.developer.yelp.com/reference/get_business_update_status_v1

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> Job Status Tip
> 
> For attributes where Yelp has granted you Publish-Then-Review fast-tracking, you can set the 'detail\_level' parameter to 2 which will reflect the job status state for when updated attributes are live on Yelp's site.

Request

`GET https://partner-api.yelp.com/v1/ingest/status/c6HT44PKCaXqzN_BdgUYv7?detail_level=2`

Response

`{   "status": "APPLIED",   "completed_at": null,   "created_at": "2018-09-18T23:15:04+00:00",   "business_results": [     {       "status": "APPLIED",       "yelp_business_id": "4ojWppqh0YFoU9NQ7532PQ",       "update_results": {         "accepts_credit_cards": {           "status": "APPLIED",           "requested_value": "true"         },         "name": {           "status": "COMPLETED",           "requested_value": "Musikal"         },         "city": {           "status": "COMPLETED",           "requested_value": "Gunnison"         },         "address1": {           "status": "COMPLETED",           "requested_value": "600 E Tomichi Ave"         }       "partner_business_id": null     }   ] }`

> ## 📘
> 
> This endpoint is part of the Data Ingestion API, visit [Data Ingestion API](https://docs.developer.yelp.com/docs/data-ingestion-api) to learn more.

job\_id

string

required

Identifier of the job as returned from the Ingestion `POST`

detail\_level

integer

Parameter to check if business attributes have been applied

# 

200

200

# 

400

400

Updated over 2 years ago

---

ShellNodeRubyPHPPython

:

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400 - Result

Updated over 2 years ago

---