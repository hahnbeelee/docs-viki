# Source: https://docs.developer.yelp.com/docs/claiming

# 

Overview

This document provides an API reference to claim businesses on Yelp and revoke business claims. The Data Ingestion API also supports the ability to look up the status of a business claim request.

# 

Authentication

Authentication uses basic HTTP authentication over SSL. Data Ingestion API credentials are used to claim, un-claim (revoke) and check the status of a business claim.

# 

Versioning

To maintain backwards-compatibility with partner-developed applications, the Yelp Data Ingestion API is versioned with the version encoded in the URI. The current and latest version is v1 and all endpoints are located at [https://partner-api.yelp.com/v1/](https://partner-api.yelp.com/v1/).

# 

Format

Response bodies use the application/json content type and should be encoded in UTF-8.

# 

Identifiers

Yelp identifiers are unique within a type of object only; they are not globally unique. For example, a photo and business may share the same identifier, WavvLdfdP6g8aZTtbBQHTw, but no other photo or business will have that same identifier.

# 

Data Ingestion API

The Yelp Data Ingestion API (“DI API”) provides a means for partners to programmatically perform updates on a large number of businesses asynchronously. Partners can perform updates on various attributes. The businesses and fields that can be updated are contract-dependent.

The DI API has two endpoints:

1. **Creating an ingestion job** Given a set of businesses and desired attribute updates, an ingestion job will be created. The job represents a set of updates that will be performed on Yelp businesses.
2. **Querying the status of an ingestion job** 
 Given an ingestion job ID, return the status of the job. The status will describe whether the job as a whole has been completed as well as the status of individual updates.

Please refer to the DI API document for details regarding the use of DI API. The DI API is required to claim businesses on Yelp.

# 

Business Claiming

The Data Ingestion API provides a means to submit a business claim and to revoke a business claim on Yelp. The API can also be used to check the status of a business claim.

| Method | HTTP Request | Description |
| --- | --- | --- |
| submit | POST /v1/ingest/create | Submit a business claim request using Business Claims object. |
| revoke | POST /v1/ingest/create | Revoke a business claim request using Business Claims Revoke object. |
| status | GET /v2/partner\_biz\_claim/request/status | Obtain the status of an existing business claim request. |

## 

Submit Business Claim

### 

Request

#### 

HTTP Request

Request

`POST https://partner-api.yelp.com/v1/ingest/create`

#### 

Parameters

Do not supply parameters with this method.

#### 

Request Body 

In the request body, supply the following resource:

| Property Name | Value | Description |
| --- | --- | --- |
| businesses\[\] | list | List of the businesses to submit business clams identified by **yelp\_business\_id** field. |

### 

Example

#### 

Request

JavaScript

`{   "businesses": [     {       "matching_criteria": {         "city": "Golden",         "name": "Mark's Sports Arena",         "country": "US",         "state": "CO",         "postal_code": "90456",         "address1": "90876 W Sandy Lane Ave"       },       "options": {         "use_matching_criteria_for_update": false       },       "update": {         "partner_biz_claim": {           "owner_account": {             "first_name": "John",             "last_name": "Smith",             "email": "john@johns-restaurant.com"           }         }       }     }   ] }`

## 

Revoke Business Claim

### 

Request

#### 

HTTP Request

Request

`POST https://partner-api.yelp.com/v1/ingest/create`

#### 

Parameters

Do not supply parameters with this method.

#### 

Request Body

In the request body, supply the following resource:

| Property Name | Value | Description |
| --- | --- | --- |
| businesses\[\] | list | List of the businesses to submit business clams identified by **yelp\_business\_id** field. |

### 

Example

#### 

Request

JavaScript

`{   "businesses": [     {       "matching_criteria": {         "city": "Golden",         "name": "Mark's Sports Arena",         "country": "US",         "state": "CO",         "postal_code": "90456",         "address1": "90876 W Sandy Lane Ave"       },       "options": {         "use_matching_criteria_for_update": false       },       "update": {         "partner_biz_claim_revoke": {           "email": "john@johns-restaurant.com"         }       }     }   ] }`

## 

Check Business Claim Status - v2

**First**, you must check if the claim request job succeeded using the Data Ingestion status endpoint:

#### 

HTTP Request

Request

`GET https://partner-api.yelp.com/v1/ingest/status/{job_id}`

**Second**, if the above status of the job=COMPLETED, then the business claim email(s) have been sent and you can use the Business Claim Status (v2) endpoint below to check if the business owner has APPROVED or DENIED the request:

#### 

HTTP Request

Request

`GET https://partner-api.yelp.com/v2/partner_biz_claim/request/status?job_id=<XX>&yelp_business_ids=<YY,ZZ>`

## 

Claim Status Success Response

| Name | Type | Description |
| --- | --- | --- |
| partner\_biz\_claim\_results | **PartnerBusinessClaimsStatusObject** | A list of PartnerBusinessClaims StatusObject. |
| errors | **RequestErrorObject** | Object that encapsulates errors with parameters on the request |

## 

Partner Business Claims Status Object

Description of the PartnerBusinessClaimsStatusObject 
 
The following fields can be returned under “partner\_biz\_claim\_results” on the response:

| Name | Type | Description |
| --- | --- | --- |
| job\_id | String | Encrypted ID |
| yelp\_business\_id | String | Encrypted ID |
| owner\_claim\_request | ClaimRequestStatusObject | Object that encapsulates basic claim info: 
\* biz\_user\_email 
\* request\_status 
\* error 
\* time\_created |

### 

Error fields

Description of the RequestErrorObject 
 
The following fields can be returned under “errors” on the response:

| Request Status Code | Description |
| --- | --- |
| invalid\_job\_id | The submitted job ID was not a valid job ID. |
| invalid\_biz\_ids | A list of input business IDs that were not valid Yelp business IDs. |
| job\_id\_with\_no\_claim\_results | The submitted job ID had no associated claim requests. |
| biz\_ids\_with\_no\_claim\_results | A list of submitted Yelp business IDs with no associated claim requests. |

### 

Example

#### 

Request

Request

`GET https://partner-api.yelp.com/v2/partner_biz_claim/request/status?job_id=5nhctdbrhydWeimreZ4R-Q&yelp_business_ids=Ak9iH80pR01lOgQ0wNTyPA`

#### 

Response

JavaScript

`{   "partner_biz_claim_results": [     {       "owner_claim_request": {         "request_status": "PENDING",         "biz_user_email": "john@johns-restaurant.com",         "time_created": "2017-12-12 13:55:25",         "signup_url": "https://biz.yelp.com/signup/partner_direct_claim/BC1F954082671EAF8538CCE2B5CFED767D695147873F76/Cy5rCoobuUhJsH071zMMvg/biz_owner?utm_campaign=claim_business&utm_content=biz_owner_approve&utm_medium=partner_link&utm_source=claim_partner_link"       }       "yelp_business_id": "Ak9iH80pR01lOgQ0wNTyPA",       "job_id": "5nhctdbrhydWeimreZ4R-Q"     }   ],     "errors": null }`

### 

Claim Request Status Codes

The following request status codes may be returned by the Claim Status endpoint:

| Request Status Code | Description |
| --- | --- |
| PENDING | The claim request for the account is on hold. A business owner needs to act on the claim email to change this state. |
| APPROVED | The claim request has been approved. The account should now have access to the business. |
| DENIED | The business owner has rejected the claim request by the partner. |
| REVOKED\_BY\_PARTNER | The claim request has been revoked by the partner. |
| CLAIM\_FAILED | The account was not claimed due to an internal error. |
| NEEDS\_REVERIFY | The user needs to redo the verification with Yelp to regain access to Yelp business owner account. This status includes a link to the Yelp verification page, field name “reverify\_url”. |
| DENIED\_NEW\_BUSINESS\_REJECTED | The new business addition has been rejected by our User Operations team. |

#### 

Note:

The v2 endpoint differs from v1 by adding job\_id and yelp\_business\_ids as request parameters. A request can be made either with a job ID or with a list of business IDs or both. **At least one must be present.** Any invalid job IDs or business IDs will be flagged on the response. Similarly, if the submitted job ID or any of the submitted business IDs do not yield any associated claim requests, they will be flagged on the response.

**A request will return with an HTTP 200 response if there are any claim request results**. Invalid IDs or IDs with no requests will be present under a separate errors field like so:

### 

Example

#### 

Request

Request

`GET https://partner-api.yelp.com/v2/partner_biz_claim/request/status?job_id=m9tQbx_sAOMpnuYb1zdClA&yelp_business_ids=Ak9iH80pR01lOgQ0wNTyPA,foobar,nDsND_MeUjo9j90eTkrVqQ`

#### 

Response

JavaScript

`{   "partner_biz_claim_results": [     {       "owner_claim_request": {         "request_status": "PENDING",         "biz_user_email": "john@johns-restaurant.com",         "time_created": "2017-12-12 13:55:25",         "signup_url": "https://biz.yelp.com/signup/partner_direct_claim/BC1F954082671EAF8538CCE2B5CFED767D695147873F76/Cy5rCoobuUhJsH071zMMvg/biz_owner?utm_campaign=claim_business&utm_content=biz_owner_approve&utm_medium=partner_link&utm_source=claim_partner_link"       },       "yelp_business_id": "Ak9iH80pR01lOgQ0wNTyPA",       "job_id": "5nhctdbrhydWeimreZ4R-Q"     }   ],   "errors": [     { 	"biz_ids_with_no_claim_results": ["nDsND_MeUjo9j90eTkrVqQ"],     	"invalid_biz_ids": ["foobar"],     	"job_id_with_no_claim_results": ["m9tQbx_sAOMpnuYb1zdClA"]     }   ] }`

### 

Claim Status HTTP Error Codes

The following error codes may be returned by the Claim Status endpoint:

| Error Code | ID | Description |
| --- | --- | --- |
| 400 | INVALID\_REQUEST | Missing a required parameter or includes an unsupported parameter. |
| 404 | PARTNER\_BIZ\_CLAIM\_IDS\_NOT\_FOUND | No requests associated with given ids found. |
| 400 | TOO\_MANY\_IDS | Number of supplied IDs exceeded limit. Must be no more than 500. |
| 404 | NOT\_FOUND | Resource not found |

### 

Example

#### 

Response

JavaScript

`{     "error": {         "http_code": 404,         "id": "PARTNER_BIZ_CLAIM_IDS_NOT_FOUND",         "description": "No requests associated with given ids found. Job ID: 1p68i0UEimI8c3aognhozQ. "     } }`

### 

Claim Request Status Error Codes

The following error codes may be returned in the ClaimsRequestStatusObject:

| Error Code | Description |
| --- | --- |
| BIZ\_CLAIM\_ERROR | A technical error on Yelp's side prevented the claim from succeeding. Please try again. |
| BIZ\_CLAIM\_NOT\_ALLOWED | Claiming is not allowed for this business. |
| BIZ\_CLOSED | Claiming is not allowed for this business because it is closed. |
| BIZ\_REMOVED\_FROM\_SEARCH | This business cannot be claimed because the business has been removed from search by Yelp due to duplicate, eligibility status, etc. Contact partner-support@yelp.com if the business is erroneously removed. |
| BIZ\_ID\_INVALID | This business cannot be claimed because the Yelp business ID provided is invalid. |
| BIZ\_PENDING | This business cannot be claimed because the business has not yet been approved by Yelp's User Ops team. |
| CLAIM\_CODE\_INVALID | A technical error on Yelp's side prevented the claim from succeeding. Please try again. |
| CLAIM\_CODE\_EXPIRED | A technical error on Yelp's side prevented the claim from succeeding. Please try again. |
| FAILED\_DUE\_TO\_FAILED\_OWNER\_REQUEST | This request failed because the corresponding owner request failed. |

### 

Example

#### 

Response

JavaScript

`{   "partner_biz_claim_results": [     {       "yelp_business_id": "rBtc3i5jYMm7Q_P4LMEHKw",       "owner_claim_request": {         "request_status": "FAILED",         "biz_user_email": "john@johns-restaurant.com",         "time_created": "2018-02-23 14:45:20",         "signup_url": "https://biz.yelp.com/signup/partner_direct_claim/BC1F954082671EAF8538CCE2B5CFED767D695147873F76/Cy5rCoobuUhJsH071zMMvg/biz_owner?utm_campaign=claim_business&utm_content=biz_owner_approve&utm_medium=partner_link&utm_source=claim_partner_link"         "error": {           "message": "Claiming is not allowed for this business because it is closed.",           "code": "BIZ_CLOSED"         }       },       "job_id": "5dP4T0nbtNXDwceLhGvKMg"     }   ],   "errors": {     "invalid_biz_ids": [       "foobar"     ]   } }`

## 

Create and Claim Business

#### 

HTTP Request

Request

`POST https://partner-api.yelp.com/v1/ingest/create`

### 

Example

This example below shows how you can create a new business called "BoJack's Restaurant" and send the business owner information for John Doe in 1 API call.

After the Yelp User Operations team approves the new business listing in 1-2 days, the business owner, John Doe, will receive an email to claim the business at [john.doe@bojackrestaurant.com](mailto:john.doe@bojackrestaurant.com)

#### 

Request

Request

`https://partner-api.yelp.com/v1/ingest/create`

#### 

Request Body

JavaScript

`{ 	"businesses": [{ 		"matching_criteria": { 			"name": "BoJack's Restaurant", 			"address1": "15 Hollywoo St", 			"city": "Los Angeles", 			"state": "CA", 			"country": "US", 			"phone": "+13640222312", 			"latitude": 1.924122456, 			"longitude": 49.12122299 		}, 		"options": { 			"use_matching_criteria_for_update": "true", 			"create_if_missing": "true" 		}, 		"update": { 			"categories": ["pizza"], 			"partner_biz_claim": { 				"owner_account": { 					"first_name": "John", 					"last_name": "Doe", 					"email": "john.doe@bojackrestaurant.com" 				} 			} 		} 	}] }`

#### 

Response

JavaScript

`{     "status": "PROCESSING",     "yelp_business_id": "9RKJAGex9lXjUReMcDETpg",     "update_results": {         "categories": [             {                 "status": "APPLIED",                 "requested_value": "pizza"             }         ]     },     "partner_business_id": null }`

| Property Name | Value | Required | Description |
| --- | --- | --- | --- |
| matching\_criteria | object | | This information will be used to create a business |
| matching\_criteria.name | string | Yes | The name of the business. Maximum length is 64; only digits, letters, spaces, and !#$%&+,-./:?@' are allowed. |
| matching\_criteria.address1 | string | No | The first line of the business’s address. Maximum length is 64; only digits, letters, spaces, and -’/#&,.: are allowed. |
| matching\_criteria.address2 | string | No | The second line of the business’s address. Maximum length is 64; only digits, letters, spaces, and -’/#&,.: are allowed. |
| matching\_criteria.city | string | Yes | The city of the business. Maximum length is 64; only digits, letters, spaces, and -’.() are allowed. |
| matching\_criteria.state | string | Yes | The ISO 3166-2 code for the region/province of the business. Maximum length is 3. |
| matching\_criteria.postal\_code | string | Yes | The postal code of the business. Maximum length is 12. |
| matching\_criteria.phone | string | No | The phone number of the business, either (a) locally-formatted with digits only (e.g., 016703080) or (b) internationally-formatted with a leading + sign and digits only after (+35316703080). Maximum length is 32. |
| matching\_criteria.country | string | Yes | The ISO 3166-1 alpha-2 country code of the business. Maximum length is 2. |
| matching\_criteria.latitude | double | No | The WGS84 latitude of the business in decimal degrees. Must be between -90 and 90. |
| matching\_criteria.longitude | double | No | The WGS84 longitude of the business in decimal degrees. Must be between -180 and 180. |
| update | object | | Provides rich content for the business. |
| update.categories\[\] | list | Yes | The categories, as [Yelp aliases](https://www.yelp.com/developers/documentation/v2/all_category_list), for the business. Case-sensitive. Maximum of 3 leaf categories. 
 
Yelp aliases can be found at the [Category List Page](https://www.yelp.com/developers/documentation/v2/all_category_list) or using the [Categories API endpoint.](https://www.yelp.com/developers/documentation/v3/all_categories) |
| update.url | string | | The business’s website URL. Maximum length is 255; only digits, ASCII letters, and !"#$%&'()\*+,-./:;<=>?@\[\\\]^\_\`{|}~ are allowed. Must start with http:// or https://. Links to Facebook, Twitter, Google Plus, or other directories are not allowed in most cases. |
| update.about\_this\_business\_specialties | string | No | The specialties of the business. Minimum length is 15, maximum is 1,000; URLs, all caps, and HTML tags are not allowed. |
| update.about\_this\_business\_history | string | No | The history of the business. Minimum length is 15, maximum is 1,000; URLs, all caps, and HTML tags are not allowed. |
| update.hours\[\] | list | No | The operating hours of the business. Multiple entries can exist for the same day (e.g., a business is open for lunch and dinner but closes in between). To set a business open 24 hours, set both the "open" and "close" fields to 00:00. To set a business to be closed for a specific day of the week, don't include that day in the list. |
| update.hours\[\].day | string | No | The full day of the week, in English, for the hours. Possible values are:
"monday"  
"tuesday"  
"wednesday"  
"thursday"  
"friday"  
"saturday"  
"sunday"

 |
| update.hours\[\].open | time | No | The time the business opens on the specified day. |
| update.hours\[\].close | time | No | The time the business closes on the specified day. The close time can be earlier than the open time if the business closes the following day (e.g., opens at 7 PM and closes at 2 AM). |
| update.photo\[\] | list |  | Photos for the business. |
| update.photo\[\].caption | string |  | The caption of the photo. Maximum length is 128, only digits, letters, spaces, and !"#$%&\\'()\*+,-./:;=?@\[\\\\\]^\_\`{|}~ are allowed. |
| update.photo\[\].url | string | | The photo’s full-size image URL. Photos must be larger than 100x100 and smaller than 10000x10000 to be considered valid. |

## 

Resource Types

### 

Business Claims Object

JavaScript

`"partner_biz_claim": { 	"owner_account": Owner Account Object }`

At least one of the Account Objects must be submitted.

| Property Name | Value | Required | Description |
| --- | --- | --- | --- |
| owner\_account | nested object | No | An Owner Account Object for the business owner. |

### 

Owner Account Object

JavaScript

`{ 	"first_name": {string}, 	"last_name": {string}, 	"email": {string}, 	"partner_name": {string} }`

| Property Name | Value | Required | Description |
| --- | --- | --- | --- |
| first\_name | string | Yes | First name for the account |
| last\_name | string | Yes | Last name for the acccount |
| email | string | Yes | Email address for the account |
| partner\_name | string | No | Name of the partner to appear in business claim emails sent to the business owner. If not specified, the default partner name will be used. |

### 

Business Claims Revoke Object

JavaScript

`"partner_biz_claim_revoke": { 	"email": {string} }`

| Property Name | Value | Required | Description |
| --- | --- | --- | --- |
| email | string | Yes | Email address for the business owner to un-claim. A business owner claim can only be un-claimed if it is still in PENDING state. |

> ## 📘
> 
> Check out our Claim Request Reference Page
> 
> ![:owlbert:](https://docs.developer.yelp.com/public/img/emojis/owlbert.png) [Claim Request Endpoint](https://docs.developer.yelp.com/reference#claim-request)

Updated almost 3 years ago

---

Did this page help you?

Yes

No

Copy Page