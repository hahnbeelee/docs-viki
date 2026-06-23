# Source: https://docs.developer.yelp.com/docs/conversions-api

> ## 🚧
> 
> Yelp Conversions API Availability
> 
> **Yelp Conversions is currently meant for larger businesses with 10+ locations**. If you do not meet this criteria, you may not receive attribution reporting at this time. If you’d like to tell us more about your interest in this integration, [please fill out this form](https://docs.google.com/forms/d/e/1FAIpQLSdWOpA1CnkrhqYNX21BsWFvaFKvwG8M99R7hY3EQGaTbFc3LA/viewform).

# 

Overview

If you would like access to Yelp's Conversions API, please ask for this directly from your assigned Yelp Sales or CS representative.

This technical documentation has been crafted to provide you with all the necessary information to get started with our Conversions API (CAPI). From setup instructions to data formatting, you'll find everything you need right here. We've made every effort to ensure that this document is comprehensive and user-friendly, providing you with everything you need to get up and running.

However, we understand that questions may arise along the way or there may be specific queries that are not addressed in this documentation. In such cases, please don't hesitate to reach out to your client success representative or solutions engineer.

Please note the below terms that govern use of Yelp's CAPI:

1. If you're a Yelp advertiser: by proceeding to use CAPI, you agree and acknowledge that attribution services are subject to [Yelp's Attribution terms](https://terms.yelp.com/attribution/).
2. If you're implementing Yelp's CAPI on behalf of an advertiser: by proceeding to use CAPI, you agree and acknowledge that attribution services are subject to [Yelp's Attribution terms](https://terms.yelp.com/attribution/) (the “Terms”) and that you will act as “agent” on behalf of the advertisers for purposes of the Terms.

Please see the below table of contents to help you navigate through this document. Both the API and S3 data methods will require you to prepare your data, however the GTM Tag Template will handle that step for you, so feel free to jump right into that.

# 

Video Intro

Check out this [brief video introduction](https://docs.google.com/videos/d/1OU9VipdjnC1lcVdtE14XvU7tlAS3lyhMfCDASjW9eLk/play) to our Conversions API to get up to speed quickly.

# 

Table of Contents

1. [General Steps for Implementation](https://docs.developer.yelp.com/docs/conversions-api#general-steps-for-implementation)
2. [What Data You’ll Need](https://docs.developer.yelp.com/docs/conversions-api#what-data-youll-need)
3. [Preparing Your Data](https://docs.developer.yelp.com/docs/conversions-api#preparing-your-data)
 1. [Conversion Data Format](https://docs.developer.yelp.com/docs/conversions-api#conversion-data-format)
 2. [Normalizing Data](https://docs.developer.yelp.com/docs/conversions-api#normalizing-data)
 3. [Hashing Data](https://docs.developer.yelp.com/docs/conversions-api#hashing-data)
 4. [Example Formatted Data](https://docs.developer.yelp.com/docs/conversions-api#example-formatted-data)
 5. [Conversion Deduplication](https://docs.developer.yelp.com/docs/conversions-api#conversion-deduplication)
4. [Data Transfer Methods](https://docs.developer.yelp.com/docs/conversions-api#data-transfer-methods)
 1. [Uploading Data via S3](https://docs.developer.yelp.com/docs/conversions-api#uploading-data-via-s3)
 2. [Sending Data via API](https://docs.developer.yelp.com/docs/conversions-api#sending-data-via-api)
 1. [Conversion APIs](https://docs.developer.yelp.com/docs/conversions-api#conversion-apis)
 2. [Rate Limiting](https://docs.developer.yelp.com/docs/conversions-api#test-events)
 3. [Errors](https://docs.developer.yelp.com/docs/conversions-api#errors)
 4. [Data Access](https://docs.developer.yelp.com/docs/conversions-api#data-access)
 3. [Google Tag Manager Integration](https://docs.developer.yelp.com/docs/conversions-api#google-tag-manager-integration)
 1. [Configure your Tagging Server URL](https://docs.developer.yelp.com/docs/conversions-api#configure-your-tagging-server-url)
 2. [Configure your GA4 User Data](https://docs.developer.yelp.com/docs/conversions-api#configure-your-ga4-user-data)
 3. [Configure GA4 Event Schema](https://docs.developer.yelp.com/docs/conversions-api#configure-ga4-event-schema)
 4. [Final Setup](https://docs.developer.yelp.com/docs/conversions-api#final-setup)
 4. [Appendix](https://docs.developer.yelp.com/docs/conversions-api#appendix)
 1. [Example API Requests](https://docs.developer.yelp.com/docs/conversions-api#example-api-requests)

 

# 

General Steps for Implementation

1. Collect the data needed to send to Yelp. See [Preparing Your Data section](https://docs.developer.yelp.com/docs/conversions-api#preparing-your-data).
2. Create a Yelp API app and retrieve client ID and API key. [See Data Access section](https://docs.developer.yelp.com/docs/conversions-api#data-access).
3. Send client ID to Yelp via the CAPI integration email thread. [See Data Access section](https://docs.developer.yelp.com/docs/conversions-api#data-access).
4. Yelp will activate the API key. [See Data Access section](https://docs.developer.yelp.com/docs/conversions-api#data-access).
5. Advertiser hashes the below data and sends it to the conversion endpoint at their desired frequency. We recommend sending data at least once every month. Weekly, daily, or in real-time are also fine.

 

# 

What Data You’ll Need

The following is the information we are asking for to run CAPI. While not all information is required, the more information you send the more accurate CAPI reports will be. Please send us all available information. Any information in **bold** is strongly encouraged. See “Preparing Your Data” for the chart that outlines the parameter names, constraints, and specifics on the description.

- **Timestamp for the conversion**
- **EventID**
- **Event name for the type of conversion**
- **Source from where the conversion took place**
- **Email address and/or phone number for the customer**
- First and last name
- Birth date
- Gender
- Country code
- City
- State
- Zip code
- Unique IDs (such as membership IDs or others that your business uses)
- IP address and user agent info
- Lead\_id \*if using Yelp's Leads API
- **Purchase amount (for measuring transactions only) If you want Yelp to give you a ROAS figure, you must send us this event\_name**

> ## 📘
> 
> Only send data that is relevant to the conversion you want to measure. For example, if you want to measure transactions, please do not send events such as page views, category views, or anything that does not contribute to the conversion being measured.

 
 

# 

Preparing Your Data

## 

Conversion Data Format

To properly ingest data into the CAPI system, conversion data must first be formatted as JSON and must match the provided schema below.

JavaScript

`{   "event_id": String,   "event_time": Integer,   "event_name": String,   "action_source": String,   "user_data": {     "em": Array[String],     "fn": String,     "ln": String,     "db": String,     "ge": String,     "ph": Array[String],     "country": Array[String],     "st": Array[String],     "zp": Array[String],     "lead_id": String,     "ct": Array[String],     "external_id": Array[String],     "client_ip_address": String,     "client_user_agent": String,     "madid": String   },   "custom_data": { 	  "value": Float, 	  "currency": String,     "order_id": String,     "content_category": String,     "content_ids": Array[String],     "contents": Array[Object],     "event_labels": Array[Object]   } }`

### 

Property descriptions and requirements

The following is a detailed description of each property within the schema:

| Parameter Name | Type | Required | Constraints | Description |
| --- | --- | --- | --- | --- |
| event\_id | String | No | length <= 128 chars | Represents a unique identifier for the conversion and will be used in the deduplication process. Although it is optional, it is highly recommended. |
| event\_time | Integer | Yes | < current time | Represents the date and time the conversion event occurred in the past. It should be formatted as a valid [Unix Timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds. |
| event\_name | String | Yes | Options: 
 
purchase 
lead 
custom\* 
 
length <= 50 chars | Indicates the type of conversion that occurred. Used for aggregation during the attribution process. This is also used in combination with event_id as part of the deduplication process. 
 
Custom values can be used, but must be prefixed with “custom_” and must only contain the following characters: A-Z a-z 0-9 \_- 
 
eg. custom\_file\_download. |
| action\_source | String | Yes | Options: 
 
“app”, 
“physical\_store”, “website” | Indicates where the conversion took place. Currently limited to “app”, “physical\_store” and “website”. |
| user\_data | Object | No | | Contains all user specific data that can be used during the matching process. The more data that is provided, the higher the chance and quality of a match occurring. |
| \[user\_data\] 
em | Array\[String\] | No | Normalized/Hashed | Customer’s email address(s). Can contain special characters but must be lowercase. Trim any leading and trailing spaces. |
| \[user\_data\] 
fn | String | No | Normalized/Hashed | Customer’s first name. Should be all lowercase with no spaces and no punctuation. |
| \[user\_data\] 
ln | String | No | Normalized/Hashed | Customer’s last name. Should be all lowercase with no spaces and no punctuation. |
| \[user\_data\] 
ph | Array\[String\] | No | Normalized/Hashed | Customer’s phone #(s). 
 
Should include country code, area code, and number. Digits only, no special characters and no leading zeros. 
 
eg. 12031231234 |
| \[user\_data\] 
db | String | No | Normalized/Hashed | Customer’s birth date in the format of YYYYMMDD. 
 
eg. 20010414 |
| \[user\_data\] 
ge | String | No | Normalized/Hashed | Customer’s gender. Should be one character of (f, m, n) to represent Female, Male, or Non-binary. |
| \[user\_data\] 
country | Array\[String\] | No | Normalized/Hashed | Customer’s country. Should be formatted as a two-character lowercase ISO-3166 country code. 
 
Example: 
us |
| \[user\_data\] 
st | Array\[String\] | No | Normalized/Hashed | Customer’s state or province. Should be formatted as a two-character lowercase abbreviation. 
 
Example: 
ca |
| \[user\_data\] 
zp | Array\[String\] | No | Normalized/Hashed | Customer’s zip or postal code. Should contain only lowercase alphanumeric characters. 
 
eg. 94101 or m3c0c1 |
| \[user\_data\] 
ct | Array\[String\] | No | Normalized/Hashed | Customer’s city. Should not contain spaces or punctuation. 
 
Example: 
newyork |
| \[user\_data\] 
external\_id | Array\[String\] | No | Hashed | Any unique ID from the advertiser, such as loyalty membership IDs, user IDs, and external cookie IDs. You can send one or more external IDs for a given event. 
If an External ID is being sent via other channels, it should be in the same format as when sent via our Conversions API. |
| \[user\_data\] 
client\_ip\_address | String | No | Not Hashed | Customer’s IP address in either IPV4 or IPV6 format. This should be included with client\_user\_agent to maximize match rates. 
 
eg. 111.111.111.111 or 2001:db8:3333:4444:5555:6666:7777:8888 |
| \[user\_data\] 
client\_user\_agent | String | No | Not Hashed | Customer’s user agent for their browser. This should be included with client\_ip\_address to maximize match rates. |
| \[user\_data\] 
madid | String | No | | Customer’s mobile advertiser ID. (IDFA/AAID) 
 
This is for mobile events only. |
| \[user\_data\] 
lead\_id | String | No | Not Hashed | The Yelp lead\_id associated with this transaction. This is only relevant if you're using Yelp's lead API. |
| custom\_data | Object | Yes | | Contains custom data specific to the conversion. |
| \[custom\_data\] 
value | Float | Only for "purchase" events | | Total monetary value of the conversion. This is a required field to determine ROAS, so must be included if event\_name is “purchase”. This value cannot be negative, Yelp's API will respond with an error if we receive a negative order value. 
 
This value is ignored if the event isn't "purchase". 
 
eg. 100.23 |
| \[custom\_data\] 
currency | String | No | Options: 
 
“USD” 
"CAD" | Currency must be a valid ISO 4217 three-digit currency code. Currently limited to “USD” and "CAD". |
| \[custom\_data\] 
order\_id | String | No | | Transaction ID or order ID tied to the conversion event. |
| \[custom\_data\] 
content\_category | String | No | | A custom category that the conversion belongs to. |
| \[custom\_data\] 
content\_ids | Array\[String\] | No | | Sub-item ids associated with this conversion. Could be the SKU ids of all the products included in the same purchase. 
 
Example: 
\["SKU\_ID\_1", "SKU\_ID\_2"\] |
| \[custom\_data\] 
contents | Array\[Object\] | No | | Additional information on the contents of this conversion in the form of a JSON object. 
 
Example: 
\[{'id': 'SKU\_ID\_1', 'quantity': 1, 'item\_price': 99.00}, {'id': 'SKU\_ID\_2', 'quantity': 1, 'item\_price': 1.23}\] |
| \[custom\_data\] 
event\_labels | Array\[Object\] | No | You may provide as many event\_label, event\_value pairs as desired, but no duplicate event\_labels are allowed. | Custom event labels for this conversion. 
 
Example: 
\[{'event\_label': 'customer\_type', 'event\_value': new\_customer}, {'event\_label': customer\_loyalty\_tier, 'event\_value': loyalty\_tier1}\] |

## 

Event Labels

Event labels are custom tags that you can attach to conversion events. They can help you gain better insights by segmenting conversions into different categories during reporting. These are completely customizable, with the only restrictions being they must come in the formatted pair of `event_label` and `event_value`. Also, we only allow 1 `event_value` per `event_label` in a single conversion.

Please don't send more than 10 unique event labels.

Examples:

- loyalty tier
- subscription type
- new vs. existing customer

## 

Normalizing Data

You’ll notice that some of the data is required to be normalized. Data is considered normalized when it has been converted to all lowercase characters, and all spaces are removed, including at the beginning and end of the string. Additionally, some data is required to have all special characters removed. If this is required, it will be noted in the description column of the table above.

For phone numbers specifically we expect 11 digits (numbers only) with a leading '1' as the country, not +1. Anything other than 11 digits with a leading 1 is incorrect. Example (281) 330 - 8004 should be sent to Yelp as 12813308004

Example data that has not been normalized:

> +1 (777) -111-1314
> 
> [FirstLast@gmail.com](mailto:FirstLast@gmail.com)
> 
> First

Example of the same data after being normalized.

> 17771111314
> 
> [firstlast@gmail.com](mailto:firstlast@gmail.com)
> 
> first

> ## 📘
> 
> Historically, advertisers often do not upload the phone numbers in the correct format. To prevent this issue, please refer to this phone number converter [tool](https://docs.google.com/spreadsheets/d/1xdzv6CGOaUgJ_3po6Sh41gBFFWSJwYiycne60pm0cfw/edit?usp=sharing).

 

## 

Hashing Data

For privacy and legal reasons, some user data is required to be encrypted before being sent to Yelp. In these cases, the data should be hashed using the hashing algorithm [SHA-256](https://en.wikipedia.org/wiki/SHA-2). This will ensure that the data remains private but also that it can be properly matched to Yelp events. If data is required to be hashed, it will be noted in the constraints column of the table above.

> ## ❗️
> 
> Please note that our system is designed to prevent unhashed personal identification data from being processed.

 

## 

Example Formatted Data

JavaScript

`{         "event_id":"bd15c2b0-2375-4f53-91b1-a959cfd30ee1",     "event_time":1685969768,     "event_name":"purchase",     "action_source": "physical_store",     "user_data":{       "em": [         "87924606b4131a8aceeeae8868531fbb9712aaa07a5d3a756b26ce0f5d6ca674"       ],       "fn": "96d9632f363564cc3032521409cf22a852f2032eec099ed5967c0d000cec607a",       "ln": "6627835f988e2c5e50533d491163072d3f4f41f5c8b04630150debb3722ca2dd",       "db": "d8f65f715e0ca17f3233cfc8033491ca844a33edc92f671404f6821391bce200",       "ge": "62c66a7a5dd70c3146618063c344e531e6d4b59e379808443ce962b3abd63c5a",       "ph": [         "9107723e93f766c6f93357d2968323fbf51c2846362eb0ae4ab7c3de3a443a8f"       ],       "country": [         "79adb2a2fce5c6ba215fe5f27f532d4e7edbac4b6a5e09e1ef3a08084a904621"       ],       "st": [         "6959097001d10501ac7d54c0bdb8db61420f658f2922cc26e46d536119a31126"       ],       "zp": [         "9de3888231a1021acddcaa006b2f2a1ead5e245ae44a6b50e997afa9371e081e"       ],       "ct": [         "fe3383cbbd5c28319f882b69e71ec83b62b5ab5b18db0e091a08b211f50e6ef0"       ],       "external_id": ["98e8c7b0d9b0d0000f6fa648addd30b9276a9bde5d8c3f6208556d6c6c612103"],       "client_ip_address": "111.111.111.111",       "lead_id": "CuOicsJesZgO8xC441gV8w",       "client_user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 13_5_1 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.1.1 Mobile/15E148 Safari/604.1",       "madid": "ABCABCAB-AAAA-1AAA-AAAA-ABCACBABCABA"     },     "custom_data": {       "value": 100.55,       "currency": "USD",       "content_category": "grocery",       "order_id": "bd15c2b0-2375-4f53-91b1-a959cfd30ee1",       "content_ids": [         "abf180ef-083b-45a4-852d-8d323756991b"       ],       "contents": [         {           "id": "abf180ef-083b-45a4-852d-8d323756991b",           "quantity": 1,           "item_price": 100.55         }       ],       "event_labels": [         {           "event_label": "customer_type",           "event_value": "new_customer"         }       ]     }   }`

 

## 

Conversion Deduplication

To ensure the highest reporting accuracy possible, we’ve provided two fields that can be populated to help with data deduplication. This ensures we only attribute an event you care about (e.g. transaction, lead) to Yelp ads once.

- event\_id
- event\_name

An event\_id can be any string that can be used to uniquely identify a conversion. This could be something like an order ID, or an internally assigned identifier. Including an event\_id is optional, but is highly recommended to help catch conversion duplicates from being included in attribution reports.

When combined, these two values form a unique key that Yelp can use to differentiate one conversion from another. If conversions are submitted without an event\_id, no deduplication can be performed and it is assumed that each conversion is unique and should be included in resulting reports. Additionally, if the same event\_id is used for multiple conversions, it could potentially lead to a loss of data.

 

# 

Data Transfer Methods

## 

Uploading Data via S3

When you have finished preparing your conversion data and have made it secure, it's time to upload it to Yelp. Don't worry, we have made the process easier for you. Here's what you need to do:

1. Data Format: Data needs to be in JSON format. Files containing multiple conversions should be written as NDJson (Newline Delimited JSON), and should contain one valid JSON formatted conversion per line.
2. Upload Location: We have created an account for you and provisioned access key pairs. These keys will grant you access to a special storage space called an S3 bucket controlled by Yelp. It allows you to upload files securely.
3. Access Key: We will provide you with a temporary 1Password link containing the access keys. It will require email verification to access but does not require a 1Password account.
4. Setting Up AWS Account: To proceed, you need to configure your AWS account with the correct access keys. You can install the AWS Command Line Interface (CLI) tool by following their documentation. Once installed, run the command:
 
 Unset
 
 `aws configure`
 
5. Uploading the File: Once your account is configured, uploading the file is a breeze. Use the following command to upload the JSON file to the Yelp S3 bucket:
 
 Unset
 
 `aws s3 cp {filename}.json s3://yelp-external-capi/{client_id}/{filename}.json`
 
 Replace {filename} with the name of your file (which should be unique every time you upload) and {client\_id} with the ID provided to you. It's recommended to include the date range of transactions in the file name for better organization.

### 

S3 data format

To properly ingest data into the CAPI system, conversion data must first be formatted as JSON and must match the provided schema below. Files containing multiple conversions should be written as NDJson (Newline Delimited JSON) and should contain one valid JSON formatted conversion per line.

JSON

`{ "event_id": String, "event_time": Integer, "event_name": String, "action_source": String, "user_data": { "em": Array[String], "fn": String, "ln": String, "db": String, "ge": String, "ph": Array[String], "country": Array[String], "st": Array[String], "zp": Array[String], "ct": Array[String], "external_id": Array[String], "client_ip_address": String, "client_user_agent": String, "madid": String, "lead_id": String }, "custom_data": { 	"value": Float, 	"currency": String, "order_id": String, "content_category": String, "content_ids": Array[String], "contents": Array[Object] } }`

 

That's it! Your data will be securely uploaded to Yelp's S3 bucket and ready for further processing.

 

## 

Sending Data via API

### 

Conversion APIs

To give you as much flexibility as you need, we have built and deployed two different API endpoints: Bulk and Single. The only difference between these two endpoints is that the bulk expects an array of Conversion Events and the single expects a single event.

If you're sending more than 100k events per day. We strongly suggest implementing the Bulk Events endpoint.

If your request to Yelp's API is successful, we'll respond with a '202' Accepted status.

 

| Name | API Request URL | Description |
| --- | --- | --- |
| Single Event | [https://api.yelp.com/v3/conversion/event](https://api.yelp.com/v3/conversion/event) | POST Endpoint which takes a single JSON object with the schema listed here. |
| Bulk Events | [https://api.yelp.com/v3/conversion/events](https://api.yelp.com/v3/conversion/events) | POST Endpoint which takes an array of JSON objects with the schema listed here. Limited to 1,000 events per request. |

 

### 

Test Events

Our APIs support an optional parameter named "**test\_event**," which is designed to facilitate the testing phase of integration. 
This parameter accepts a boolean value. When set to `true`, it enables the API to perform all validations as it would under normal operational conditions, yet it prevents the submission of data to the production environment. 
This feature is particularly useful for verifying that the data being sent conforms to our required structure and formatting specifications, without the risk of introducing test data into the production system. It is important to note that the "**test\_event**" parameter is not mandatory; in its absence, the system assumes a default value of `false`, indicating standard operation with data being directed to production.

 

### 

Rate Limiting

As part of our API, we do have some limits on how often you can send data. Each of our endpoints will accept up to 100 requests per second and 50,000 requests per day.

If you expect to send more events per day, let us know and we're happy to discuss the limits. Otherwise we recommend you batch your requests and send them through the Bulk Events endpoint.

 

### 

Errors

There are several error codes returned that might occur through your use of these endpoints.

| Name | Code | Reason |
| --- | --- | --- |
| Unauthorized | 401 | Verify API Key is correctly attached in the headers. The error will include which part of the authentication chain you are missing. Otherwise please reach out to us! |
| Bad Request | 400 | Fields which are marked required in the schema must be included and the fields marked hashed must be hashed. We will let you know if fields are not hashed or are not included where necessary. |
| Too Many Requests | 429 | You’ve hit the rate limits for these endpoints. Let us know if you need to modify these and we’re happy to work with you. |
| Not Found | 404 | Verify that our team has reached out to you to let you know that your key is active. The endpoints are currently delisted and not available without the correct API key. |

 

### 

Data Access

When you have finished preparing your system to generate your conversion data in JSON, normalized and hashed, it's time to send it to Yelp. Here's what you need to do:

1. Sign up for developer access: Head on over to [https://www.yelp.com/developers/v3/manage\_app](https://www.yelp.com/developers/v3/manage_app) and sign in with your consumer Yelp account.
 
2. Create New App: You will be presented with a screen asking you to create a new app. Pick a name that will help the application be identified in the future, and please use a contact email that will allow us to contact someone in the event of any discrepancies. In the description, feel free to describe how you intend to use this API. You might be asked to select a plan or tier, it does not matter what you select for this option since we'll be applying custom configurations to your account. When you’re satisfied, you must agree to the Yelp API Terms and Display Requirements. Let us know if you have any questions. Upon completion, click Create New App.
 
 ![](https://files.readme.io/87ca926-Screenshot_2024-07-30_at_4.15.44_PM.png)
3. App Setup: When you have created the application, you will be faced with a new screen which allows you to update the information listed previously, as well as show you two key pieces of information:
 
 ![](https://files.readme.io/c1c2263-Screenshot_2024-07-30_at_4.17.06_PM.png)
 1. Client ID: Please copy this ID and send it to your customer success representative. This will allow us to connect your account to this App, and give the API Key access to our Conversion API.
 2. API Key: This is required for using the Conversion API and will be attached to requests made. We will go into further detail in the next steps. Make note of this key and consider it secret. Do not give this to anyone you do not authorize to send conversion events to us. If you believe this key has been leaked or in any way compromised, there is a button further down the page which will allow you to refresh it. It will immediately disable the key and generate a new one.
4. Client Integration: Once you’ve given us your Client ID for your application, we will enable your API key to have access to our endpoints. CAPI will use the same authentication that’s detailed [here](https://docs.developer.yelp.com/docs/fusion-authentication).
 

That’s it! Once we’ve let you know that your client app is approved and ready, you can start hitting our endpoints with data. For example events, please see the Appendix for sample single or bulk events.

 

## 

Google Tag Manager Integration

We strongly encourage folks to use the API or the S3 method if possible. Debugging any issues that may arise with the Tag Manager implementation can be quite cumbersome.

This document is for integrating the Yelp CAPI Template Tag into your existing GTM Setup. This method will use [GTM Server-side tagging](https://developers.google.com/tag-platform/tag-manager/server-side/intro) with a [custom tag template](https://developers.google.com/tag-platform/tag-manager/templates), built on Google Analytics 4 (GA4) so please confirm your system is set up to support this.

Additionally, the GTM integration is slightly different from the API access above, but will use the API under the hood, so please familiarize yourself with the API integration. However the tag itself will handle normalizing and hashing the correct fields for ingestion, so you don’t need to worry about handling that yourself.

### 

Configure your Tagging Server URL

When configuring your web server to send data to your server container, make sure you set first\_party\_collection flag to true. You must do this to be able to pass the user\_data parameters to the Server-Side container. Under Fields to Set, click Add Row and set:

- Field name: first\_party\_collection
- Field value: true

![](https://files.readme.io/5ca2f4c-Screenshot_2024-07-30_at_4.21.55_PM.png) 

### 

Configure your GA4 User Data

You can create a Data Layer Variable for each of the common GTM event schema’s user\_data parameters. [You can read more about this here](https://support.google.com/tagmanager/answer/6164391?hl=en). For example, you can create a variable like user\_data\_email\_address that can be mapped to the Data Layer Variable name eventModel.user\_data.email\_address.

If you’re not using the data layer, you will need to configure variables for each parameter. See the below table for data mappings.

| Yelp Conversion API Parameter | GA4 Field Name | GTM Data Layer Variable | Priority |
| --- | --- | --- | --- |
| Email (em) | user\_data.email\_address | eventModel.user\_data.email\_address | Highest |
| Phone (ph) | user\_data.phone\_number | eventModel.user\_data.phone\_number | High |
| First Name (fn) | user\_data.address.first\_name | eventModel.user\_data.address.first\_name | Medium |
| Last Name (ln) | user\_data.address.last\_name | eventModel.user\_data.address.last\_name | Medium |
| Date of Birth (db) | user\_data.date\_of\_birth | N/A | Medium |
| Gender (ge) | user\_data.gender | N/A | Medium |
| Country (country) | user\_data.address.country | eventModel.user\_data.address.country | Medium |
| State/Province (st) | user\_data.address.region | eventModel.user\_data.address.region | Medium |
| Zip/Postal Code (zp) | user\_data.address.postal\_code | eventModel.user\_data.address.postal\_code | Medium |
| City (ct) | user\_data.address.city | eventModel.user\_data.address.city | |
| External ID (external\_id) | user\_data.external\_id | N/A | Medium |
| Mobile Ad ID (madid) | user\_data.madid | N/A | Medium |

 

### 

Configure GA4 Event Schema

You will need to set up an Event Name for your tag. You can set this as a static variable or from a variable. Yelp Event Names generally match Google equivalents, however, we are expecting to support the following events:

- add\_payment\_info
- add\_to\_cart
- add\_to\_wishlist
- purchase
- search
- checkout
- lead
- view\_content
- view\_category
- signup
- watch\_video

We will still ingest others, but will append custom\_ to the event name.

 

### 

Final Setup

You will need a listener on your server container to listen to GA4 events. This is normally configured by default.

Finally, install the Yelp Conversion API Template. It is a server-side tag that will convert the standard event model from the GA4 Client to the Conversions API event schema expected and send it to our API. To install this tag, you will need the Yelp API key from the Data Access section above and will need to enter it into the apiAccessToken template parameters in order to have this sent properly.

 

## 

Appendix

### 

Example API Requests

Single API

Unset

`curl --request POST \      --url https://api.yelp.com/v3/conversion/event \      --header 'Authorization: Bearer API_KEY' \      --header 'accept: application/json' \      --header 'content-type: application/json' \      --data ' { "event":{ "event_id":"unique_string_to_identify_this_conversion_event", "event_time":1693946978, "event_name":"purchase", "action_source":"website", "user_data": { "em": ["hashed_email_string"], "fn": "hashed_first_name_string", "ln": "hashed_last_name_string", "ph":["hashed_phone_number_string"], "db": "hashed_date_of_birth_string", "ge": "hashed_gender_string", "country":["hashed_country_string"], "st": ["hashed_street_name_string"], "lead_id": "CuOicsJesZgO8xC441gV8w", "zp": ["hashed_zipcode_string"], "ct": ["hashed_city_string"], "external_id": ["hashed_external_id_string"], "client_ip_address": "192.168.1.1", "client_user_agent": "Chrome/51.0.2704.103", }, "custom_data": { 		"value":10.0, 	"currency":"USD", } }, "test_event": true }'`

Bulk API

Unset

`curl --request POST \      --url https://api.yelp.com/v3/conversion/events \      --header 'Authorization: Bearer API_KEY' \      --header 'accept: application/json' \      --header 'content-type: application/json' \      --data ' { "events":[{ "event_id":"unique_string_to_identify_this_conversion_event", "event_time":1693946978, "event_name":"purchase", "action_source":"website", "user_data": { "em": ["hashed_email_string"], "fn": "hashed_first_name_string", "ln": "hashed_last_name_string", "ph":["hashed_phone_number_string"], "db": "hashed_date_of_birth_string", "ge": "hashed_gender_string", "country":["hashed_country_string"], "st": ["hashed_street_name_string"], "zp": ["hashed_zipcode_string"], "ct": ["hashed_city_string"], "external_id": ["hashed_external_id_string"], "client_ip_address": "192.168.1.1", "client_user_agent": "Chrome/51.0.2704.103", "lead_id": "CuOicsJesZgO8xC441gV8w" }, "custom_data": { 		"value":10.0, 		"currency":"USD", } }], "test_event": false }'`

### 

Tag Manager Template

`___INFO___  {   "type": "TAG",   "id": "cvt_temp_public_id",   "version": 1,   "securityGroups": [],   "displayName": "Yelp Conversion API",   "brand": {     "id": "brand_dummy",     "displayName": ""   },   "description": "A server-side tag template to send conversion events to Yelp\u0027s Conversion API",   "containerContexts": [     "SERVER"   ] }   ___TEMPLATE_PARAMETERS___  [   {     "type": "TEXT",     "name": "apiAccessToken",     "displayName": "Yelp API Access Key",     "simpleValueType": true,     "valueValidators": [       {         "type": "NON_EMPTY"       }     ],     "help": "To use the Conversion API you need an Access Key. Please talk to your rep on enabling this and see https://docs.developer.yelp.com/docs/places-intro for generating a token"   },   {     "type": "CHECKBOX",     "name": "testInput",     "checkboxText": "Is this a test event?",     "simpleValueType": true   } ]   ___SANDBOXED_JS_FOR_SERVER___  const getAllEventData = require('getAllEventData'); const sendHttpRequest = require('sendHttpRequest'); const JSON = require('JSON'); const Math = require('Math'); const getTimestampMillis = require('getTimestampMillis'); const sha256Sync = require('sha256Sync'); const getType = require('getType');  const eventModel = getAllEventData();  const DEFAULT_ACTION_SOURCE = 'website';  // Get Milliseconds since epoch, divided by 1000 to get seconds for Unix Timestamp const DEFAULT_EVENT_TIME = Math.round(getTimestampMillis() / 1000);  const EVENT_NAME_MAPPINGS = {     'checkout': 'checkout',     'buy': 'purchase',     'pay': 'purchase',     'payment': 'purchase',     'purchase': 'purchase',     'addtocart': 'add_to_cart',     'add_to_cart': 'add_to_cart',     'generate_lead': 'lead',     'lead': 'lead',     'addpaymentinfo': 'add_payment_info',     'add_payment_info': 'add_payment_info',     'addtowishlist': 'add_to_wishlist',     'add_to_wishlist':'add_to_wishlist',     'viewcontent': 'view_content',     'view_content': 'view_content',     'viewcategory': 'view_category',     'view_category': 'view_category',     'sign_up': 'signup',     'signup': 'signup',     'watchvideo': 'watch_video',     'watch_video': 'watch_video',     'search': 'search', };  const DEFAULT_EVENT_NAME = 'custom_event';   // Functions function isAlreadyHashed(input) {     return input && (input.match('^[A-Fa-f0-9]{64}$') != null); }  function replaceAll(string, search, replace) {   return string.split(search).join(replace); }  function hashFunction(input, removeSpaces) {     const shouldRemoveSpaces = removeSpaces || false;     const type = getType(input);     let formattedInput = input;     if (type == 'undefined' || input == null || input == 'undefined' || input == '') {         return undefined;     }      if (isAlreadyHashed(input)) {         return input;     }      if (shouldRemoveSpaces) {         formattedInput = replaceAll(input,' ', '');     }      return sha256Sync(formattedInput.trim().toLowerCase(), { outputEncoding: 'hex' }); }  function getYelpEventName(eventName) {     if (!eventName) return DEFAULT_EVENT_NAME;      const lowerEventName = eventName.toLowerCase();      return EVENT_NAME_MAPPINGS[lowerEventName] || 'custom_' + lowerEventName; }  function normalizeAndHashGender(inputGender) {     if (getType(inputGender) == 'string' && inputGender.length > 0) {         return hashFunction(inputGender.charAt(0));     }     return null; }  function normalizeAndHashPhone(inputPhone) {     if (getType(inputPhone) == 'string') {         return hashFunction(replaceAll(inputPhone, '-', '').replace('+', '').replace('(', '').replace(')', ''), true);     }     return null; }  function getContentIdsFromItems(items) {     return items.map(item => (item.item_id || item.item_name) || undefined); }  function getContentFromItems(items) {     return items.map(item => {         return {             "id": (item.item_id || item.item_name) || undefined,             "item_price": item.price || undefined,             "quantity": item.quantity || undefined,         };     }); }  function checkPreHashedUserData(userObject, field) {     const sha256PrefixedField = 'sha256_' + field;     if (userObject[sha256PrefixedField]) {         if (isAlreadyHashed(userObject[sha256PrefixedField])) {             return userObject[sha256PrefixedField];         }     }     if (userObject[field]) {         return hashFunction(userObject[field]);     }      return null; }  function setUserData(modelUserData) {     const userData = {};      const em = checkPreHashedUserData(modelUserData, 'email_address');      if (em) userData.em = [em];      const ph = checkPreHashedUserData(modelUserData, 'phone_number');      if (ph) userData.ph = [ph];      if (modelUserData.gender) {         userData.ge = normalizeAndHashGender(modelUserData.gender);     }      if (modelUserData.date_of_birth) {         userData.db = hashFunction(modelUserData.date_of_birth);     }      if (modelUserData.address != null) {         const addressData = modelUserData.address;          const fn = checkPreHashedUserData(addressData, 'first_name');          if (fn) userData.fn = fn;          const ln = checkPreHashedUserData(addressData, 'last_name');          if (ln) userData.ln = ln;          if (addressData.country)             userData.country = [hashFunction(addressData.country)];          if (addressData.region)             userData.st = [hashFunction(addressData.region)];          if (addressData.postal_code)             userData.zp = [hashFunction(addressData.postal_code, true)];          if (addressData.city)             userData.ct = [hashFunction(addressData.city, true)];     }      if (modelUserData.external_id) {         userData.external_id = [hashFunction(modelUserData.external_id)];     }      if (modelUserData.madid) {         userData.madid = modelUserData.madid;     }      return userData; }  // Event Data const event = {};  if (data.testEvent) {   event.test_event = true; }  if (eventModel.event_id) {     event.event_id = eventModel.event_id; }  event.event_time = eventModel.event_time ? eventModel.event_time : DEFAULT_EVENT_TIME;  event.event_name = getYelpEventName(eventModel.event_name);  event.action_source = eventModel.action_source ? eventModel.action_source : DEFAULT_ACTION_SOURCE;  event.user_data = eventModel.user_data ? setUserData(eventModel.user_data) : {};  event.user_data.client_ip_address = eventModel.ip_override; event.user_data.client_user_agent = eventModel.user_agent;  event.custom_data = {};  if (eventModel.value) {     event.custom_data.value = eventModel.value; }  if (eventModel.currency) {     event.custom_data.currency = eventModel.currency; }  if (eventModel.transaction_id) {     event.custom_data.order_id = eventModel.transaction_id; }  if (eventModel.items) {     const items = eventModel.items;     event.custom_data.content_ids = getContentIdsFromItems(items);      if (items.item_category) event.custom_data.content_category = items.item_category;      event.custom_data.contents = getContentFromItems(items); }  function sendEvent(capiEvent) {     const eventRequest = { event: capiEvent };      const apiEndpoint = 'https://api.yelp.com/v3/conversion/event';      const requestHeaders = {         headers: {             'content-type': 'application/json',             'Authorization': 'Bearer ' + data.apiAccessToken         },         method: 'POST'     };      return sendHttpRequest(         apiEndpoint,         (statusCode, headers, response) => {             if (statusCode >= 200 && statusCode < 300) {                 data.gtmOnSuccess();             } else {                 data.gtmOnFailure();             }         },         requestHeaders,         JSON.stringify(eventRequest)     ); }  sendEvent(event);   ___SERVER_PERMISSIONS___  [   {     "instance": {       "key": {         "publicId": "read_event_data",         "versionId": "1"       },       "param": [         {           "key": "eventDataAccess",           "value": {             "type": 1,             "string": "any"           }         }       ]     },     "clientAnnotations": {       "isEditedByUser": true     },     "isRequired": true   },   {     "instance": {       "key": {         "publicId": "send_http",         "versionId": "1"       },       "param": [         {           "key": "allowedUrls",           "value": {             "type": 1,             "string": "specific"           }         },         {           "key": "urls",           "value": {             "type": 2,             "listItem": [               {                 "type": 1,                 "string": "https://api.yelp.com/*/conversion/event"               }             ]           }         }       ]     },     "clientAnnotations": {       "isEditedByUser": true     },     "isRequired": true   } ]   ___TESTS___  scenarios: - name: On Event calls conversion API successfully   code: |-     runCode(testConfig);      // Verify that the tag finished successfully.     assertApi('sendHttpRequest').wasCalledWith(apiEndpoint, actualSuccessCallback, requestHeaders, JSON.stringify(eventRequest));      assertApi('gtmOnSuccess').wasCalled(); - name: Minimal Event still fires   code: |-     const genericEventName = 'generic_event';     const mockTime = 1000;      const minimalEvent = {       event_name: genericEventName,       ip_override: testEvent.user_data.ip_address,       user_agent: testEvent.user_data.user_agent,     };      const expectedMinimal = {       event_time: 1,       event_name: 'custom_' + genericEventName,       action_source: 'website',       user_data: {         client_ip_address: testEvent.user_data.ip_address,         client_user_agent: testEvent.user_data.user_agent,       },       custom_data: {},     };      const minimalEventRequest = { event: expectedMinimal };      mock('getTimestampMillis', () => {       return mockTime;     });      mock('getAllEventData', () => {       return minimalEvent;     });      // Call runCode to run the template's code.     runCode(testConfig);      // Verify that the tag finished successfully.     assertApi('sendHttpRequest').wasCalledWith(apiEndpoint, actualSuccessCallback, requestHeaders, JSON.stringify(minimalEventRequest));      assertApi('gtmOnSuccess').wasCalled(); - name: Pre-Hashed Fields   code: |-     // Setting the email to the hashed version of itself should     // just pass it through.     const hashedEmail = hashFunction(testEvent.user_data.email);     testEventModel.user_data.email_address = hashedEmail;      runCode(testConfig);      // Verify that the tag finished successfully.     assertApi('sendHttpRequest').wasCalledWith(apiEndpoint, actualSuccessCallback, requestHeaders, JSON.stringify(eventRequest));      assertApi('gtmOnSuccess').wasCalled(); - name: Sha256 fields   code: |-     // Hash the emails first     const hashedEmail = hashFunction(testEvent.user_data.email);     const hashedPhone = hashFunction(testEvent.user_data.phone);     const hashedFirst = hashFunction(testEvent.user_data.first_name);     const hashedLast = hashFunction(testEvent.user_data.last_name);      // Then set the sha256 versions of those fields with the hashed email     testEventModel.user_data.sha256_email_address = hashedEmail;     testEventModel.user_data.sha256_phone_number = hashedPhone;     testEventModel.user_data.address.sha256_first_name = hashedFirst;     testEventModel.user_data.address.sha256_last_name = hashedLast;      runCode(testConfig);      // Verify that the tag finished successfully.     assertApi('sendHttpRequest').wasCalledWith(apiEndpoint, actualSuccessCallback, requestHeaders, JSON.stringify(eventRequest));      assertApi('gtmOnSuccess').wasCalled(); - name: Check user data for empty string   code: |-     // Set the test event to empty     testEventModel.user_data.email_address = '';     testEventModel.user_data.phone_number = undefined;      // Update expected to be not defined     Object.delete(expectedEvent.user_data, 'em');     Object.delete(expectedEvent.user_data, 'ph');      runCode(testConfig);      // Verify that the tag finished successfully.     assertApi('sendHttpRequest').wasCalledWith(apiEndpoint, actualSuccessCallback, requestHeaders, JSON.stringify(eventRequest));      assertApi('gtmOnSuccess').wasCalled(); - name: Malformed json in fields   code: |-     const fakeObject = {       foo: 'bar',       bar: 'foo'     };      const stringFakeObject = JSON.stringify(fakeObject);     const halfObject = stringFakeObject.slice(0,stringFakeObject.length/2);      testEventModel.user_agent = halfObject;      expectedEvent.user_data.client_user_agent = halfObject;      runCode(testConfig);      const stringifiedEvent = JSON.stringify(eventRequest);      // Verify that the tag finished successfully.     assertApi('sendHttpRequest').wasCalledWith(apiEndpoint, actualSuccessCallback, requestHeaders, stringifiedEvent);      assertApi('gtmOnSuccess').wasCalled();      // And parsing it doesn't error     const output = JSON.parse(stringifiedEvent); setup: |-   // Imports   const sha256Sync = require('sha256Sync');   const JSON = require('JSON');   const Object = require('Object');    // Helper Functions   function hashFunction(input, removeSpaces) {     let formattedInput = input;      if (removeSpaces) {       formattedInput = input.replace(' ', '');     }      return sha256Sync(formattedInput.trim().toLowerCase(), { outputEncoding: 'hex' });   }    function normalizeAndHashGender(inputGender) {     return hashFunction(inputGender.charAt(0));   }    // Event Data    const testEvent = {     event_id: 'event_id_1',     event_time: 123456789,     event_name: "purchase",     action_source: "web",     user_data: {       email: "email@test.com",       first_name: "first",       last_name: "last",       phone: "11231234567",       date_of_birth: "20010414",       gender: "n",       country: "us",       state: "ca",       zip: "94105",       city: "san francisco",       external_id: "user_42",       madid: "madid_user_42",       ip_address: '192.168.1.0',       user_agent: 'Browser/1.0 (OS 1.0; x64)'     },     custom_data: {       value: 10,       currency: 'usd',       order_id: 'order_id_1',       content_ids: ['id_1', 'id_2'],       contents: [         {           id: 'id_1',           item_price: 2,           quantity: 3         },         {           id: 'id_2',           item_price: 4,           quantity: 1         }       ]     }   };    const testEventModel = {     event_id: testEvent.event_id,     event_time: testEvent.event_time,     event_name: testEvent.event_name,     action_source: testEvent.action_source,     user_data: {       email_address: testEvent.user_data.email,       phone_number: testEvent.user_data.phone,       gender: testEvent.user_data.gender,       date_of_birth: testEvent.user_data.date_of_birth,       address: {         first_name: testEvent.user_data.first_name,         last_name: testEvent.user_data.last_name,         country: testEvent.user_data.country,         region: testEvent.user_data.state,         postal_code: testEvent.user_data.zip,         city: testEvent.user_data.city       },       external_id: testEvent.user_data.external_id,       madid: testEvent.user_data.madid     },     ip_override: testEvent.user_data.ip_address,     user_agent: testEvent.user_data.user_agent,     value: testEvent.custom_data.value,     currency: testEvent.custom_data.currency,     transaction_id: testEvent.custom_data.order_id,     items: [       {         item_id: testEvent.custom_data.contents[0].id,         item_name: testEvent.custom_data.contents[0].id,         price: testEvent.custom_data.contents[0].item_price,         quantity: testEvent.custom_data.contents[0].quantity,       },       {         item_id: testEvent.custom_data.contents[1].id,         item_name: testEvent.custom_data.contents[1].id,         price: testEvent.custom_data.contents[1].item_price,         quantity: testEvent.custom_data.contents[1].quantity,       }     ]   };    const expectedEvent = {     event_id: testEvent.event_id,     event_time: testEvent.event_time,     event_name: testEvent.event_name,     action_source: testEvent.action_source,     user_data: {       em: [hashFunction(testEvent.user_data.email)],       ph: [hashFunction(testEvent.user_data.phone)],       ge: normalizeAndHashGender(testEvent.user_data.gender),       db: hashFunction(testEvent.user_data.date_of_birth),       fn: hashFunction(testEvent.user_data.first_name),       ln: hashFunction(testEvent.user_data.last_name),       country: [hashFunction(testEvent.user_data.country)],       st: [hashFunction(testEvent.user_data.state)],       zp: [hashFunction(testEvent.user_data.zip, true)],       ct: [hashFunction(testEvent.user_data.city, true)],       external_id: [hashFunction(testEvent.user_data.external_id)],       madid: testEvent.user_data.madid,       client_ip_address: testEvent.user_data.ip_address,       client_user_agent: testEvent.user_data.user_agent,     },     custom_data: {       value: testEvent.custom_data.value,       currency: testEvent.custom_data.currency,       order_id: testEvent.custom_data.order_id,       content_ids: testEvent.custom_data.content_ids,       contents: testEvent.custom_data.contents,     }   };    // Mocks    mock('getAllEventData', () => {     return testEventModel;   });    const apiEndpoint = 'https://api.yelp.com/v3/conversion/event';   const eventRequest = { "event": expectedEvent };   const testAPIAccessToken = 'testAPIAccessToken';   const requestHeaders = {     headers: {       'content-type': 'application/json',       'Authorization': 'Bearer ' + testAPIAccessToken     },     method: 'POST'   };    let actualSuccessCallback, httpBody;   mock('sendHttpRequest', (postUrl, response, options, body) => {     actualSuccessCallback = response;     httpBody = body;     actualSuccessCallback(200, {}, '');   });    const testConfig = {     apiAccessToken: testAPIAccessToken   };   ___NOTES___  Created on 8/2/2024, 4:12:43 PM`

Updated 8 months ago

---

Did this page help you?

Yes

No

Copy Page