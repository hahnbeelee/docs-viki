# Source: https://docs.developer.yelp.com/docs/program-feature-api

> ## 📘
> 
> This is a Yelp Partner API
> 
> Access is disabled by default. See [Yelp Partner APIs](https://docs.developer.yelp.com/docs/yelp-partner-apis) on how to get access.

# 

Overview

This document provides a reference to all endpoints of Program Feature API and contains sample request and responses. The Program Feature API allows retrieval and set-up of feature information for specific payment programs.

# 

Authentication

Authentication uses Basic HTTP Authentication over SSL. The credentials used for the Yelp Data Ingestion API should be used for the Program Feature API.

# 

Versioning

To maintain backwards-compatibility with partner-developed applications, the Program Feature API is versioned with the version encoded as the last path segment of the URL, i.e. `https://<host>/<endpoint>/<version>`. The current and latest version of the API is v1.

# 

Format

Request and response bodies use the application/json content type and should be encoded in UTF-8. This format supports special characters (e.g. ‘ & / % etc.).

# 

Identifiers

Yelp identifiers are unique within a type of object only; they are not globally unique. For example, a photo and business may share the same identifier, WavvLdfdP6g8aZTtbBQHTw, but no other photo or business will have that same identifier.

# 

Value Types

All date properties should use the YYYY-MM-DD format.

# 

Program Feature API Endpoints

The Program Feature API provides a means to retrieve/modify/delete features for specific payment programs by calling into one of the following four endpoints:

| Method | HTTP Endpoint | Description |
| --- | --- | --- |
| retrieve | GET /program/<program\_id>/features/v1 | Retrieve available and active features for the specified payment program |
| update | POST /program/<program\_id>/features/v1 | Set up or update program features for the specified payment program |
| delete | DELETE /program/<program\_id>/features/v1 | Delete certain program features from the specified payment program |

## 

Supported Feature Types

The following table describes the format for the various features types you can set up using this API. The format will be used in both response and request bodies.

| Feature Type Identifier | Object Format | Notes |
| --- | --- | --- |
| `LINK_TRACKING` | "LINK\_TRACKING": 
{ 
"website": {string|null}, 
"menu": {string|null}, 
"call\_to\_action": {string|null} 
} | If all properties of the object are null, then the feature is disabled (not active). |
| `NEGATIVE_KEYWORD_TARGETING` | "NEGATIVE\_KEYWORD\_TARGETING": 
{ 
"suggested\_keywords": \[string\], 
"blocked\_keywords": \[string\] 
} | If the list of blocked\_keywords is empty the feature is disabled (not active). |
| `STRICT_CATEGORY_TARGETING` | "STRICT\_CATEGORY\_TARGETING": 
{ 
"enabled": true|false 
} | |
| `AD_SCHEDULING` | "AD\_SCHEDULING": { 
"uses\_opening\_hours": true|false 
} | |
| `CUSTOM_LOCATION_TARGETING` | "CUSTOM\_LOCATION\_TARGETING": 
{ 
"businesses": \[{ 
"business\_id": "string", 
"locations": \[string\] 
}\] 
} | |
| `AD_GOAL` | "AD\_GOAL": 
{ 
"ad\_goal": string 
} | |
| `CALL_TRACKING` | "CALL\_TRACKING": 
{ 
"enabled": true|false, 
"businesses": \[{ 
"business\_id": "string", 
"metered\_phone\_number": {string|null} 
}\] 
} | |
| `BUSINESS_HIGHLIGHTS` | "BUSINESS\_HIGHLIGHTS": { 
"active\_business\_highlights": \["BH\_1"\], 
"available\_business\_highlights": \[ 
"BH\_1", 
"BH\_2" 
\], 
"mutually\_exclusive\_business\_highlights": \[ 
\["BH\_1", "BH\_2"\] 
\], 
} | When using **POST** to setup/modify BH, 
the format is: 
 
"BUSINESS\_HIGHLIGHTS": { 
"business\_highlights": \["BH\_1", "BH\_2"\], 
} |
| `VERIFIED_LICENSE` | "VERIFIED\_LICENSE": { 
"licenses": \[ 
{ "license\_number": "some\_license\_1234" }, 
{ "license\_number": "different\_license" } 
\] 
} | A **POST** request will append or edit a license indexed on license\_number. **DELETE** must be used to remove licenses (cannot send empty license list) |
| `CUSTOM_RADIUS_TARGETING` | "CUSTOM\_RADIUS\_TARGETING": { 
"custom\_radius": {float|null}, 
} | Radius in miles (1 to 60) 
By default, radius is null which means this feature is inactive. |
| `CUSTOM_AD_TEXT` | "CUSTOM\_AD\_TEXT": { 
"custom\_review\_id": {string|null}, 
"custom\_text": {string|null} 
} | Only one of the two fields here can be set at a time. 
By default, both are set to null, which means the ad text is set by Yelp. |
| `CUSTOM_AD_PHOTO` | "CUSTOM\_AD\_PHOTO": { 
"custom\_photo\_id": {string|null}, 
} | By default, this is set to null, which means the ad photo is set by Yelp. |
| `BUSINESS_LOGO` | "BUSINESS\_LOGO": { 
"business\_logo\_url": {string|null} 
} | URL set to null means this feature is inactive. 
In **POST**, url must be publicly accessible image file of type: jpeg / png / gif / tiff |
| `YELP_PORTFOLIO` | "YELP\_PORTFOLIO": { 
"projects": \[ 
{ 
"project\_id": {string}, 
"published": {boolean} 
}, ... 
\] 
} | **POST** will publish/unpublish a project created via Portfolio API. Body only needs to contain the project IDs to update 
 
**DELETE** endpoint deletes all projects |

## 

Feature Type Parameters

The following section describes the configurable parameters in each request/response object for each supported feature type.

### 

LINK\_TRACKING

You can either define tracking URLs, which will replace the URLs on your Yelp business pages, or tracking parameters, which will be attached to the existing URLs. You can use link tracking for your website, Call to Action URLs and menu URLs.

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `website` | string _or_ null | Yes | Tracking URL or parameter(s) for the website link |
| `menu` | string _or_ null | Yes | Tracking URL or parameter(s) for the menu link |
| `call_to_action` | string _or_ null | Yes | Tracking URL or parameter(s) for the CTA link |

### 

NEGATIVE\_KEYWORD\_TARGETING

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `suggested_keywords` | list of string | No | List of search terms for which your biz ad might be shown. 
**Please note:** This list consists of up to 25 possible keywords where your ad may appear. Those suggestions are based on common searches associated with the business category. The 25 suggestions are not exhaustive, your ad may also appear on searches not shown in the list of suggestions. |
| `blocked_keywords` | list of string | Yes | List of currently blocked keywords. You can use this field to update the list of terms you would like to block. 
**Please note:** You are allowed to add custom search terms outside of the suggested keywords list. Suggested keywords list is for guidance purposes. |

### 

STRICT\_CATEGORY\_TARGETING

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `enabled` | bool | Yes | |

### 

AD\_SCHEDULING

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `uses_opening_hours` | bool | Yes | Should the ad only be delivered while the business is open? 
 
i.e. if {'uses\_opening\_hours': true } and the business's hours are 8-5pm, a 6pm search wouldn't be eligible for this ad. |

### 

CUSTOM\_LOCATION\_TARGETING

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `businesses` | list\[object\] | Yes | List of all businesses that are part of the ad campaign. |
| `businesses[].business_id` | string | Yes | Business ID |
| `businesses[].locations` | list\[string\] | Yes | List of 0 up to 25 locations. These locations can be zip codes, cities, neighbourhoods, counties or state names but must be within the US. |

### 

AD\_GOAL

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `ad_goal` | string | Yes | Must be one of `DEFAULT`, `CALLS`, or `WEBSITE_CLICKS` |

### 

CALL\_TRACKING

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `enabled` | bool | Yes | Indicates whether call tracking is enabled or disabled on a campaign level. |
| `businesses` | list\[object\] | Yes | List of all businesses that are part of the ad campaign. |
| `businesses[].business_id` | string | Yes | Business ID |
| `businesses[].metered_phone_number` | string _or_ null | Yes | Phone number which will be used as a call tracking number for the provided business in the ad campaign |

### 

BUSINESS\_HIGHLIGHTS

| Request type | Parameter | Type | Required | Required |
| --- | --- | --- | --- | --- |
| GET | `active_business_highlights` | list\[string\] | No | Currently active business highlights enabled |
| GET | `available_business_highlights` | list\[string\] | No | Valid business highlights available to select from |
| GET | `mutually_exclusive_business_highlights` | list\[list\[string\]\] | No | Pairs of business highlights that can't be enabled together |
| POST | `business_highlights` | list\[string\] | Yes | List of desired business highlights to set |

### 

VERIFIED\_LICENSE

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `licenses[].license_number` | string | Yes | License number provided by issuing agency/authority |
| `licenses[].license_expiry_date` | string | No | License expiry date (format YYYY-MM-DD) |
| `licenses[].license_trade` | string | No | Business or trade for which a license was issued |
| `licenses[].license_issuing_agency` | string | No | Agency/authority that issued the license |

### 

CUSTOM\_RADIUS\_TARGETING

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| custom\_radius | float | No | Radius in miles (1 to 60) 
By default, custom\_radius is null which means this feature is inactive. |

### 

CUSTOM\_AD\_TEXT

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| custom\_review\_id | string | No | Identifier of the review from which to extract the text. |
| custom\_text | string | No | Custom text to be shown. Requirements: 
Minimum length: 15 
Max Length: 1500 
Does not allow urls 
Does not allow if it is only numbers 
Does not allow if there are too many capital letters 
Does not allow if there are too many consecutive capital letters. |

\*Note: Only one field can be set 
By default, this is set to null, which means the ad text is set by Yelp.

### 

CUSTOM\_AD\_PHOTO

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| custom\_photo\_id | string | No | Identifier of the photo to show on the custom ad. |

### 

BUSINESS\_LOGO

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| business\_logo\_url | string | No | URL to the business's brand logo if in use. 
In **POST**, URL must be publicly accessible image file of type: jpeg / png / gif / tiff |

### 

YELP\_PORTFOLIO

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| projects\[\].project\_id | string | Yes | Identifier of a project |
| projects\[\].published | boolean | Yes | Whether the project is published |

## 

Portfolio API

The Yelp Portfolio API helps users manage their business portfolios.

| Endpoint | Object Format | Notes |
| --- | --- | --- |
| GET 
`/program/{program_id}/ portfolio/{project_id}/v1` | { 
"name": {string}, 
"call\_to\_action": {"WEBSITE"|...}, 
"description": {string}, 
"service\_offerings": 
\[<so\_1>, <so\_2>,... 
\], 
"cost": {string-enum|null}, 
"duration": {string-enum|null}, 
"completion\_year": {int|null}, 
"completion\_month": {int|null}, 
"published": {boolean|true}, 
"id": {string} 
} | Fetch portfolio project details. 
 
Up to four service offerings 
 
Nullable fields are optional |
| PUT `/program/{program_id}/ portfolio/{project_id}/v1` | { 
"name": {string}, 
"call\_to\_action": {"WEBSITE"|...}, 
"description": {string}, 
"service\_offerings": 
\[<so\_1>, <so\_2>,... 
\], 
"cost": {string-enum|null}, 
"duration": {string-enum|null}, 
"completion\_year": {int|null}, 
"completion\_month": {int|null} 
} | Update an existing project 
 
Up to four service offerings |
| POST `/program/{program_id}/ portfolio/v1` | No request payload 
 
Returns 
{ 
"project\_id": {string} 
} | Create a new project draft |
| DELETE `/program/{program_id}/portfolio/ {project_id}/v1` | | Delete a project |
| POST `/program/{program_id}/portfolio/ {project_id}/photos/v1` | Request Payload 
{ 
"photo\_url": {string|null}, 
"biz\_photo\_id": {string|null} 
"is\_before\_photo": {boolean}, 
"caption": {string}, 
} 
 
Response Payload 
{ 
"photo\_id": {string} 
} 
or/and via Location header | For uploading photos 
First uploaded photo will be the cover photo 
 
is\_before\_photo adds a "before" label to the photo 
 
Either provide an existing biz photo ID or link to URL |
| GET `/program/{program_id}/portfolio/ {project_id}/photos/v1` | \[ 
{ 
"id": {string}, 
"photo\_url": {string}, 
"caption":{string|null}, 
"is\_before\_photo": {boolean}, 
"is\_cover\_photo": {boolean} 
} 
\] | List photos belonging to the project |
| DELETE `/program/{program_id}/portfolio/ {project_id}/photos/{photo_id}/v1` | | Delete a photo from the project |

For more information about each of the parameters, please refer to the [Program Feature API Reference Page](https://docs.developer.yelp.com/reference#retrieve-program-feature)

> ## 📘
> 
> Check out our Program Feature API Reference Page
> 
> ![:owlbert:](https://docs.developer.yelp.com/public/img/emojis/owlbert.png) [Program Feature Endpoints](https://docs.developer.yelp.com/reference#retrieve-program-feature)

Updated over 2 years ago

---

Did this page help you?

Yes

No

Copy Page