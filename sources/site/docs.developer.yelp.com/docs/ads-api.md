# Source: https://docs.developer.yelp.com/docs/ads-api

> ## 📘
> 
> This is a Yelp Partner API
> 
> Access is disabled by default. See [Yelp Partner APIs](https://docs.developer.yelp.com/docs/yelp-partner-apis) on how to get access.

# 

Overview

This document provides a reference to all API endpoints and sample responses available to manage Yelp advertising campaigns. This api isn't available by default, to request access, please work with your Yelp account team.

## 

Authentication

Authentication uses basic HTTP authentication over SSL. The credentials used for the Yelp Data Ingestion API should be used for the Advertising API.

## 

Versioning

To maintain backwards-compatibility with partner-developed applications, the Yelp Advertising API is versioned with the version encoded in the URI. The current and latest version is v1 and all endpoints are located at `https://partner-api.yelp.com/v1/`.

## 

Format

Response bodies use the application/json content type and should be encoded in UTF-8.

## 

Identifiers

Yelp identifiers are unique within a type of object only; they are not globally unique. For example, a photo and business may share the same identifier, _WavvLdfdP6g8aZTtbBQHTw_, but no other photo or business will have that same identifier.

## 

Value Types

All date properties should use the YYYY-MM-DD format.

## 

Yelp Business IDs

The Advertising API requires encrypted business IDs to create new programs. Please reference our [Business Match API documentation](https://www.yelp.com/developers/documentation/v3/business_match) on how to pull these values for Yelp listings.

# 

Advertising API Endpoints

The Yelp Advertising API provides a means to add/modify/terminate advertising programs for businesses on Yelp by calling into one of the following four endpoints:

| Method | HTTP Request | Description |
| --- | --- | --- |
| **create** | POST /create | Create a new program for a Yelp business |
| **modify** | POST /{program\_id}/edit | Modify an existing program for a Yelp business |
| **terminate** | POST /{program\_id}/end | Terminate an existing program for a Yelp business |
| **status** | GET /status/{job\_id} | Obtain the status of an existing ingestion job |

## 

Create Program

### 

HTTP POST

[https://partner-api.yelp.com/v1/reseller/program/create](https://partner-api.yelp.com/v1/reseller/program/create)

**Request:**

JavaScript

`curl \   -X POST \   --user "{username}:{password}" \   https://partner-api.yelp.com/v1/reseller/program/create?start=<date>&end=<date>&business_id=<yelp_business_id>&program_name=<program_name>` 

**Description:**

This endpoint will create the program `<program_name>` to the Yelp business as specified by `<business_id>`. Start and end dates are left as optional parameters to specify the duration of the program. The dates are expected to be in YYYY-MM-DD format. `<business_id>` and `<program_name>` are the required parameters for all program types. For CPC programs, `<budget>` and `<is_autobid>` is required. The `<max_bid>` parameter is also required for CPC programs if `<is_autobid>` is set to false.

**NOTE:** For CPC programs, the business listing **must have** text for the specialties field since CPC ads uses text from specialties if there isn't a sufficient level of reviews to use reviews text for ads. Please use the Data Ingestion API to set the about\_this\_business\_specialties field for a given business. Also, the business listing **must have** at least 1 category in order to appear in Yelp search results.

**Common Program Parameters: (create)** 
 
The following table describes the request parameters for all programs.

| Property Name | Value | Optional | Description |
| --- | --- | --- | --- |
| business\_id | string | No | Yelp business id |
| program\_name | string | No | Indicates the type of program you want to enable. 
 
Possible values are:
- BP – Branded Profile
- EP – Enhanced Profile
- CPC – Cost per click ads
- RCA (Remove Competitor Ads)
- CTA (Call To Action)
- SLIDESHOW (Slideshow)
- BH (Business Highlights)
- VL (Verified License)
- LOGO
- PORTFOLIO

 |
| promotion\_code | string | Yes | Use a valid promotion code to purchase this program. |
| start | date | Yes | Start date for the specified program. The date format is YYYY-MM-DD format (e.g., 2016-01-01). Programs will start at 12:00am PST for a given start date. 
 
If no start date is set, then the program will start immediately. |
| end | date | Yes | End date for the specified program. The date format is YYYY-MM-DD format (e.g., 2016-01-31). Programs will end at 11:59pm PST for a given end date. 
 
If no end date is set, then the program will run indefinitely until it is terminated via the Advertising API. |

**CPC Program Parameters: (create)** 
 
The following table describes the request parameters for CPC programs.

| Property Name | Value | Optional | Description |
| --- | --- | --- | --- |
| budget | integer | No | Monthly budget in cents. For a monthly budget of $50.00, please input “5000”. 
Value must be greater than or equal to $25 dollars. |
| currency | string | Yes | [ISO 4217 Currency Code](http://www.xe.com/iso4217.php). Default is USD |
| is\_autobid | boolean | No | If field is set to true, then Yelp will autobid. Set to false if using max\_bid |
| max\_bid | integer | Yes\* | Maximum bid value in cents. 
\* Value must be greater than or equal to $0.50 or "50". 
\* This field is required if is\_autobid is false. 
\* You can set a max\_bid for paced campaigns but will run the risk of potentially underfulfilling if the max\_bid is set too low. 
\* If you want to bid a maximum of $25.50, please use a value of “2550” cents and not “25.50” which will result in error. \* max\_bid is not immediately applied and can take up to 24 hours to go live on Yelp's end. 
 |
| pacing method | string | Yes | Possible values are: 
\* "paced" (default if is\_autobid=true) 
\* "unpaced" (default if max\_bid is set) - cannot be used if is\_autobid=true. 
 
"paced" will attempt to spread the budget evenly throughout the month. 
"unpaced" will attempt to spend the budget as fast as possible. 
 
Please reach out to partner-support@yelp.com if you're interested in using unpaced campaigns before using that setting. 
 |
| fee\_period | string | Yes | Possible values are: 
\* CALENDAR\_MONTH 
\* ROLLING\_MONTH 
 
The fee\_period determines the time frame for the CPC Program. If CALENDAR\_MONTH, then budgets will reset at the 1st of every month. If ROLLING\_MONTH, then budgets will reset every 30 days. Default is CALENDAR\_MONTH. |
| ad\_categories | list of strings | Yes | You are able to choose any of the categories of the specified business and run the CPC campaign for only these categories. 
 
You get the categories of a business using the [Get business by ID](https://docs.developer.yelp.com/reference/v3_business_info) endpoint. 
Use the alias of the categories (field categories\[\].alias). 
 
Example: If the business has the categories hvac and plumbing, you can run two different campaigns for each category with a different budget each. |

**Usage Example for creating CPC program with $200.00 budget and maximum bid of $5.00 starting on Jan 1, 2016 and ending on Jan 31, 2016:**

**Example Request:**

JavaScript

`curl \   -X POST \   --user "{username}:{password}" \   https://partner-api.yelp.com/v1/reseller/program/create?business_id=WavvLdfdP6g8aZTtbBQHTw&program_name=CPC&budget=20000&max_bid=500&is_autobid=false&start=2016-01-01&end=2016-01-31` 

**Example Response:**

JavaScript

`Response:  { 	"job_id": "prvtN-nilb4mUynGGgKuBQ" }`

See [Receipting](https://docs.developer.yelp.com/#receipting) for responses after completion of the request

**Usage Example for adding Branded Profile program that starts immediately:**

**Example Request:**

JavaScript

`curl \   --user "{username}:{password}" \   -X POST \   https://partner-api.yelp.com/v1/reseller/program/create?business_id=WavvLdfdP6g8aZTtbBQHTw&program_name=BP`

**Example Response:**

JavaScript

`Response:  { 	"job_id": "prvtN-nilb4mUynGGgKuBQ" }`

See [Receipting](https://docs.developer.yelp.com/#receipting) for responses after completion of the request

**Usage Example for adding Enhanced Profile program that starts immediately:**

**Example Request:**

JavaScript

`curl \   --user "{username}:{password}" \   -X POST \   https://partner-api.yelp.com/v1/reseller/program/create?business_id=WavvLdfdP6g8aZTtbBQHTw&program_name=EP`

**Example Response:**

JavaScript

`Response:  { 	"job_id": "prvtN-nilb4mUynGGgKuBQ" }`

See [Receipting](https://docs.developer.yelp.com/#receipting) for responses after completion of the request

## 

Modify Program

### 

HTTP POST

[https://partner-api.yelp.com/v1/reseller/program/{program\_id}/edit](https://partner-api.yelp.com/v1/reseller/program/%7Bprogram_id%7D/edit)

**Request:**

JavaScript

`curl \   -X POST \   --user "{username}:{password}" \   https://partner-api.yelp.com/v1/reseller/program/<program_id>/edit?start=<date>&end=<date>`

**Description:**

This endpoint will allow modification to attributes of an existing program, <program\_id>. This endpoint will be incapable of setting the end date to be a date in the past, or modifying the start date of a program that has already started, or modifying the start date to be before the current time. Programs will end at the end of day of the end date.

**Common Program Parameters: (edit)** 
 
 
The following table describes the request parameters for all programs.

| Property Name | Value | Optional | Description |
| --- | --- | --- | --- |
| program\_id | string | No | The program\_id that needs to be modified. |
| start | date | Yes | Start date for the specified program |
| end | date | Yes | End date for the specified program |

 

**CPC Program Parameters: (edit)** 
 
The following table describes the request parameters for CPC programs.

| Property Name | Value | Optional | Description |
| --- | --- | --- | --- |
| budget | integer | Yes | Monthly budget in cents. |
| future\_budget\_date | date | Yes | Schedule an upcoming budget change for campaign. |
| max\_bid | integer | Yes | Maximum bid value in cents. Can only be changed if program is using max\_bid option. \* The minimum value is $0.50 which is "50" |
| pacing\_method | string | Yes | Possible values are: 
\* "paced" 
\* "unpaced" 
 |
| ad\_categories | list of strings | Yes | You are able to choose any of the categories of the specified business and run the CPC campaign for only these categories. 
 
You get the categories of a business using the [Get business by ID](https://docs.developer.yelp.com/reference/v3_business_info) endpoint. 
Use the alias of the categories (field categories\[\].alias). 
 
Example: If the business has the categories hvac and plumbing, you can run two different campaigns for each category with a different budget each. |

**Usage Example for modifying budget to $250.00 and maximum bid to $10.00:**

**Example Request:**

JavaScript

`curl \   --user "{username}:{password}" \   -X POST \   https://partner-api.yelp.com/v1/reseller/program/c6HT44PKCaXqzN_BdgKPCw/edit?budget=25000&max_bid=1000`

**Example Response:**

JavaScript

`Response:  { 	"job_id": "yf8sGfL9NNRpHoXmKudBwg" }`

See sample request & response when viewing status of a job id for a modified program:

**Example Request:**

JavaScript

`curl \   -X GET \   -H "Accept: application/json" \   --user "{username}:{password}" \   https://partner-api.yelp.com/v1/reseller/status/yf8sGfL9NNRpHoXmKudBwg`

**Response Format:**

{
 "status": "COMPLETED",
 "completed\_at": {datetime},
 "created\_at": {datetime}>,
 "business\_results": \[
 {
 "status": "COMPLETED",
 "identifier\_type": "PROGRAM",
 "identifier": {program\_id},
 "update\_results": {
 "program\_modified": {
 "budget": {
 "status": "COMPLETED",
 "requested\_value": {budget\_value}
 },
 "program\_id": {
 "status": "COMPLETED",
 "requested\_value":{program\_id}
 },
 "max\_bid": {
 "status": "COMPLETED",
 "requested\_value": {max\_bid\_value}
 }
 }
 }
 }
 \]
}

**Usage Example for changing end date:**

**Example Request:**

JavaScript

`curl \   --user "{username}:{password}" \   -X POST \   https://partner-api.yelp.com/v1/reseller/program/c6HT44PKCaXqzN_BdgKPCw/edit?end=<date>`

**Example Response:**

JavaScript

`Response:  { 	"job_id": "prvtN-nilb4mUynGGgKuBQ" }`

## 

Terminate Program

### 

HTTP POST

[https://partner-api.yelp.com/v1/reseller/program/{program\_id}/end](https://partner-api.yelp.com/v1/reseller/program/%7Bprogram_id%7D/end)

**Request:**

JavaScript

`curl \   -X POST \   --user "{username}:{password}" \   https://partner-api.yelp.com/v1/reseller/program/<program_id>/end`

**Description:**

This will immediately end the program specified by `<program_id>`.

| Property Name | Value | Optional | Description |
| --- | --- | --- | --- |
| program\_id | string | No | The program\_id to terminate |

**Usage:**

**Example Request:**

JavaScript

`curl \   -X POST \   --user "{username}:{password}" \   https://partner-api.yelp.com/v1/reseller/program/c6HT44PKCaXqzN_BdgKPCw/end`

**Example Response:**

JavaScript

`Response:  { 	"job_id": "prvtN-nilb4mUynGGgKuBQ" }`

See sample request & response when viewing status of a job id for a terminated program:

**Example Request:**

JavaScript

`curl \   -X GET \   -H "Accept: application/json" \   --user "{username}:{password}" \   https://partner-api.yelp.com/v1/reseller/status/prvtN-nilb4mUynGGgKuBQ`

**Example Response:**

{ 
 "status": "COMPLETED",
 "completed\_at": ,
 "created\_at": ,
 "business\_results": \[
 {
 "status": "COMPLETED",
 "identifier\_type": "PROGRAM",
 "identifier": ,
 "update\_results": {
 "program\_ended": {
 "status": "COMPLETED",
 "requested\_value": 
 }
 }
 }
 \]
}

## 

Receipting

### 

HTTP GET

[https://partner-api.yelp.com/v1/reseller/status/{job\_id}](https://partner-api.yelp.com/v1/reseller/status/%7Bjob_id%7D)

**Request:**

JavaScript

`curl \   -X GET \   --user "{username}:{password}" \   https://partner-api.yelp.com/v1/reseller/status/<job_id>`

**Description:**

This endpoint expects a job\_id, and will return the status of the updates associated with the job.

**Usage:**

**Example Request:**

JavaScript

`curl \   -X GET \   -H "Accept: application/json" \   --user "{username}:{password}" \   https://partner-api.yelp.com/v1/reseller/status/c6HT44PKCaXqzN_BdgKPCw`

Response:

 
Example for CPC program 
 

{
 "status": \[COMPLETED|PROCESSING\],
 "completed\_at": {datetime},
 "created\_at": {datetime},
 "business\_results": \[
 {
 "status": \[COMPLETED|PROCESSING\],
 "identifier\_type": "BUSINESS",
 "identifier": {yelp\_business\_id},
 "update\_results": {
 "program\_added": {
 "start": {
 "status": \[COMPLETED|PROCESSING\],
 "requested\_value": {datetime},
 },
 "program\_name": {
 "status": \[COMPLETED|PROCESSING\],
 "requested\_value": {program\_name}
 },
 "end": {
 "status": \[COMPLETED|PROCESSING\],
 "requested\_value": {datetime},
 },
 "program\_id": {
 "status": \[COMPLETED|PROCESSING\],
 "requested\_value": {program\_id}
 },
 "yelp\_business\_id": {
 "status": \[COMPLETED|PROCESSING\],
 "requested\_value": {yelp\_business\_id}
 },
						"is\_autobid": {
 "status": \[COMPLETED|PROCESSING\],
 "requested\_value": \[true|false\]
 },
						"max\_bid": {
 "status": \[COMPLETED|PROCESSING\],
 "requested\_value": {max\_bid\_value}
 },
						 "budget": {
 "status": \[COMPLETED|PROCESSING\],
 "requested\_value": {budget\_value}
 }
 }
 }
 }
 \]
}

 
Example for BP program 

{
 "status": \[COMPLETED|PROCESSING\],
 "completed\_at": {datetime},
 "created\_at": {datetime},
 "business\_results": \[
 {
 "status": \[COMPLETED|PROCESSING\],
 "identifier\_type": "BUSINESS",
 "identifier": {yelp\_business\_id},
 "update\_results": {
 "program\_added": {
 "start": {
 "status": \[COMPLETED|PROCESSING\],
 "requested\_value": {datetime},
 },
 "program\_name": {
 "status": \[COMPLETED|PROCESSING\],
 "requested\_value": {program\_name}
 },
 "end": {
 "status": \[COMPLETED|PROCESSING\],
 "requested\_value": {datetime},
 },
 "program\_id": {
 "status": \[COMPLETED|PROCESSING\],
 "requested\_value": {program\_id}
 },
 "yelp\_business\_id": {
 "status": \[COMPLETED|PROCESSING\],
 "requested\_value": {yelp\_business\_id}
 }
 }
 }
 }
 \]
}

## 

Pause Program

### 

HTTP POST

[https://partner-api.yelp.com/program/{program\_id}/pause/v1](https://partner-api.yelp.com/program/%7Bprogram_id%7D/pause/v1)

**Request:**

`javascript curl \   -X POST \   --user "{username}:{password}" \   https://partner-api.yelp.com/program/<program_id>/pause/v1`

**Response:**

`HTTP 202` Empty response

**Description:**

This endpoint will allow a currently running CPC program to be paused. The campaign will temporarily stop running until it is resumed by the [Program Resume](https://docs.developer.yelp.com/#program-resume) endpoint.

> ## 📘
> 
> This feature is coming soon
> 
> Please get in touch if you would like to get early access

## 

Resume Program

### 

HTTP POST

[https://partner-api.yelp.com/program/{program\_id}/resume/v1](https://partner-api.yelp.com/program/%7Bprogram_id%7D/resume/v1)

**Request:**

JavaScript

`curl \   -X POST \   --user "{username}:{password}" \   https://partner-api.yelp.com/program/<program_id>/resume/v1`

**Response:**

`HTTP 202` Empty response

**Description:**

This endpoint will allow a currently paused CPC program to be resumed.

> ## 📘
> 
> This feature is coming soon
> 
> Please get in touch if you would like to get early access

# 

Advertising API Errors

## 

Error Codes

The following general error codes may be returned by the Advertising API:

| Error code | Message | Description |
| --- | --- | --- |
| 503 | Service Unavailable | The API is currently unavailable |
| 403 | Authorization Error | Sent when the partner is not authorized for a particular request (e.g. They don’t have access to either the business, metric, or time range requested.) |
| 500 | Internal Error | Something went wrong. |
| 202 | Job not complete | The job has been submitted and is being worked on. Please resubmit at another time. |
| 400 | Invalid Request | The request submitted is invalid |
| 401 | Authentication Error | The user is not who they seem or their credentials are incorrect. |
| 404 | Not Found | Resource not found |

## 

Error Messages

When the Advertising API returns a job\_id, the response from the [/reseller/status/](https://docs.developer.yelp.com/#receipting) endpoint may contain errors.

The **business\_results.status** field can be set to REJECTED if the business is closed or removed from search or if the program is no longer active. The possible error codes may be returned in the **business\_results.error.code** field:

| Error code | Message |
| --- | --- |
| BUSINESS\_NOT\_ACTIVE | This business cannot be accessed because it is closed. |
| PROGRAM\_NOT\_ACTIVE\_CLOSED\_BUSINESS | This program is no longer active because has been closed. Contact partner-support@yelp.com if the business is erroneously closed. |
| PROGRAM\_NOT\_ACTIVE\_BUSINESS\_REMOVED\_FROM\_SEARCH | This program is no longer active because the business has been removed from search by Yelp due to duplicate, eligibility status, etc. Contact partner-support@yelp.com if the business is erroneously removed. |
| PROGRAM\_HAS\_EXPIRED | This program cannot be modified. The program is no longer active because the program end date has passed, or the business has been removed from search by Yelp due to being a duplicate listing, eligibility status, etc. Contact partner-support@yelp.com with the yelp\_business\_id if the business was erroneously ended or removed. |

Here is an example error response:

{
 "status": "COMPLETED",
 "completed\_at": {datetime},
 "created\_at": "{datetime},
 "business\_results": \[
 {
 "status": **"REJECTED"**,
 "identifier\_type": "BUSINESS",
 "identifier": {yelp\_business\_id},
 "error": {
 "message": "This program is no longer active because the business has been removed from search by Yelp due to duplicate, eligibility status, etc. Contact partner-support@yelp.com if the business is erroneously removed.",
 "code": "PROGRAM\_NOT\_ACTIVE\_BUSINESS\_REMOVED\_FROM\_SEARCH"
 }
 }
 \]
}

Even if the **business\_results.status** field is set to COMPLETED, there may be errors in when the **update\_results.program\_added.status** or **update\_results.program\_modified.status** is set to REJECTED. The possible error codes may be returned in the **update\_results.program\_added.error.code** or **update\_results.program\_modified.error.code** field in this scenario:

| Error code | Message |
| --- | --- |
| INVALID\_OR\_MISSING\_KEY | Invalid or missing required key(s): {required\_keys} |
| PROGRAM\_ALREADY\_RUNNING\_BY\_ANOTHER\_PROVIDER | You cannot run this program because the client has already purchased this product from another provider. |
| CANNOT\_ADD\_PROGRAM\_IN\_PAST | Cannot add a program that starts in the past. |
| PROGRAM\_ALREADY\_REQUESTED | You already requested to enable this product for this client. |
| CONFLICTS\_WITH\_ANOTHER\_ACTIVE\_PROGRAM | This program conflicts with a currently active or recently ended program. If you are trying to add a new program, please use a start date subsequent to the end date of any conflicting programs. |
| PARENT\_WAS\_REJECTED | Another part of your request failed, check the other attributes of our response to find the root error cause. |
| CANNOT\_DECREASE\_BUDGET\_BELOW\_AMOUNT\_ALREADY\_SPENT | Campaign has already spent {amount\_spent}. Cannot decrease budget below actual spend. |
| CURRENCY\_MISMATCH | Cannot change current type; currency must remain consistent. |
| BUSINESS\_RESTRICTED\_FROM\_ADVERTISING | Yelp has blocked this locations ability to purchase advertising. Reach out to partner-support@yelp.com to request an exception to this block. |
| INVALID\_PRICE | Invalid price. Must be numerical formatted in cents. |
| UNSUPPORTED\_CATEGORIES | Category is not supported: The category of the business you are trying to advertise is declined due to policy restrictions. |
| BID\_TOO\_HIGH\_FOR\_BUDGET | Bid exceeds total prorated budget. Please increase budget to increase your chances of ad display. |
| COULD\_NOT\_MODIFY\_PROGRAM | Could not modify specified program. |
| NO\_CATEGORIES | The business does not have categories or they are awaiting approval. |
| CAMPAIGN\_BUDGET\_VIOLATES\_PROMO\_RESTRICTIONS | Campaign budgeted outside of restrictions set by associated promo. |

Here is an example error response:

{
 "status": "COMPLETED",
 "completed\_at": {datetime},
 "created\_at": "{datetime},
 "business\_results": \[
 {
 "status": "COMPLETED",
 "identifier\_type": "BUSINESS",
 "identifier": {yelp\_business\_id},
 "update\_results": {
 "program\_added": {
 "status": **"REJECTED"**,
 "requested\_value": {
 ...

 

 

\`\`\`
\`\`\`

> 📘 Check out our Advertising API Reference Page
> 
> :owlbert: \[Advertising API Endpoints\](https://docs.developer.yelp.com/v1.0/reference#create-profile)

 

Copy Page