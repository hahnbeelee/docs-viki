# Source: https://docs.developer.yelp.com/docs/verified-license-status-webhooks

> ## 📘
> 
> This page described the details of the Verified License Status Webhooks. For the general webhook setup please see [Webhooks](https://docs.developer.yelp.com/docs/webhooks).

# 

Overview

Verified License Status webhooks are intended for notifying you about verification status changes to your submitted licenses. When one of your licenses gets e.g. verified or rejected, we'll send an HTTP POST payload to the webhook's configured URL. If you experience any issues with the system or if you have questions, feel free to contact us at [partner-support@yelp.com](mailto:partner-support@yelp.com)

# 

Format of Webhook Messages (POST Requests)

The webhook request payload is a JSON object that will include a timestamp, an object of "business" and data related to the message. The "id" inside of data refers to the business\_id related to the event.

Full Webhook Payload

`{   "time": "2021-02-09T14:54:54.239056",   "object": "business",   "data": {     "id": "i2kK8NtpmtuKf84NYm0d3A",     "updates": [       {         "event_type": "VERIFIED_LICENSE_UPDATE_EVENT",         "license_verification_status": "VERIFIED",         "license_number": "test_license_1",         "license_expiry_date": null,         "license_trade": "plumber",         "license_issuing_agency": null       }     ]   } }`

Request Attributes

| Field name | Description | Data Type |
| --- | --- | --- |
| `event_type` | The type of event this update represents. Will be always `VERIFIED_LICENSE_UPDATE_EVENT`. | String |
| `license_verification_status` | Verification status of the license. One of: 
\- `REJECTED` 
\- `VERIFIED` 
\- `PENDING` | String |
| `license_verification_failure_reason` | Reason for license rejection. Possible values are: 
\- `NOT_FOUND` 
\- `NAME_MATCH_FAILURE` 
\- `SECONDARY_MATCH_FAILURE` 
\- `INACTIVE` 
\- `REJECT` 
 
Only included if `license_verification_status` is `REJECTED` | String |
| `license_number` | Number of the license | String |
| `license_expiry_date` | Expiry date of the license in YYYY-MM-DD format | String (nullable) |
| `license_trade` | The trade the license was issued for. | String (nullable) |
| `license_issuing_agency` | The agency or authority that issued the license. | String (nullable) |

Updated about 4 years ago

---

Did this page help you?

Yes

No

Copy Page