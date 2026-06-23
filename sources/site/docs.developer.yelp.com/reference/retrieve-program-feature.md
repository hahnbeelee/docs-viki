# Source: https://docs.developer.yelp.com/reference/retrieve-program-feature

> ## 📘
> 
> Note
> 
> This endpoint returns the program features that are available for the specified program. For each available feature type, the `features` object will contain the corresponding feature object as described below. If the program does not support any of the available feature types the `features` object will be empty.

### 

LINK\_TRACKING

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `website` | string _or_ null | Yes | Tracking URL or parameter(s) for the website link |
| `menu` | string _or_ null | Yes | Tracking URL or parameter(s) for the menu link |
| `url` | string _or_ null | Yes | Tracking URL or parameter(s) for the CTA link |

### 

NEGATIVE\_KEYWORD\_TARGETING

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `suggested_keywords` | list of string | No | List of search terms for which your biz ad might be shown. 
**Please note:** This list consists of up to 25 possible keywords where your ad may appear. Those suggestions are based on common searches associated with the business category. The 25 suggestions are not exhaustive, your ad will also appear on searches not shown in the list of suggestions. |
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
| `ad_goal` | bool | Yes | Must be one of `DEFAULT`, `CALLS`, or `WEBSITE_CLICKS` |

### 

CALL\_TRACKING

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `enabled` | bool | Yes | Indicates whether call tracking is enabled or disabled on a campaign level. |
| `businesses` | list\[object\] | Yes | List of all businesses that are part of the ad campaign. |
| `businesses[].business_id` | string | Yes | Business ID |
| `businesses[].metered_phone_number` | string _or_ null | Yes | Phone number which will be used as a call tracking number for the provided business in the ad campaign. |

### 

SERVICE\_OFFERINGS\_TARGETING

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `disabled_service_offerings` | list\[string\] | Yes | List of all service offerings that are disabled for an ad campaign. For a GET request, this field will be populated with the disabled service offerings for all categories in the ad campaign. For a POST request this field is required and should contain all the service offerings the caller wants to disable for the ad campaign. |
| `enabled_service_offerings` | list\[string\] | Yes | List of all service offerings that are enabled for an ad campaign. For a GET request, this field will be populated with the enabled service offerings for all categories in the ad campaign. For a POST request, this field can be omitted. |

### 

BUSINESS\_HIGHLIGHTS

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `active_business_highlights` | list\[string\] | Yes | Currently active business highlights enabled |
| `available_business_highlights` | list\[string\] | Yes | Valid business highlights available to select from |
| `mutually_exclusive_business_highlights` | list\[list\[string\]\] | Yes | Pairs of business highlights that can't be enabled together |

### 

VERIFIED\_LICENSE

| Parameter | Type | Required | |
| --- | --- | --- | --- |
| `licenses[].license_number` | string | Yes | License number provided by issuing agency/authority |
| `licenses[].license_expiry_date` | string | No | License expiry date (format YYYY-MM-DD) |
| `licenses[].license_trade` | string | No | Business or trade for which a license was issued |
| `licenses[].license_issuing_agency` | string | No | Agency/authority that issued the license |
| `licenses[].license_verification_status` | string | Yes | License verification status, one of PENDING, VERIFIED or REJECTED |
| `licenses[].license_verification_failure_reason` | string | No | License verification failure reason |

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
| custom\_text | string | No | Custom text to be shown. |

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

> ## 📘
> 
> This endpoint is part of the Program Feature API, visit [Program Feature API](https://docs.developer.yelp.com/docs/program-feature-api) to learn more.

program\_id

string

required

# 

200

200

# 

400

400

Updated over 3 years ago

---

Did this page help you?

Yes

No

Shell

:

xxxxxxxxxx

1

curl \\

2

\--user "{username}:{password}" \\ 

3

https://partner-api.yelp.com/program/hmPSQN\_57dtcE9fUJvWTDw/features/v1

Choose an example:

application/json

200 - Result400 - Result

Updated over 3 years ago

---

Did this page help you?

Yes

No