# Source: https://docs.developer.yelp.com/docs/partner-support-api

> ## 📘
> 
> This is a Yelp Partner API
> 
> Access is disabled by default. See [Yelp Partner APIs](https://docs.developer.yelp.com/docs/yelp-partner-apis) on how to get access.

# 

Overview

Partner Support API endpoints will allow partners to retrieve the latest business information, migration information and advertising program information about their businesses.

# 

Authentication

Authentication uses basic HTTP authentication over SSL. The Data Ingestion API credentials are used to make calls to these APIs. To gain access to these APIs, please email [partner-support@yelp.com](mailto:partner-support@yelp.com)

# 

Business Info API

Given a Yelp encrypted business id, this API returns business information, including business migration information and additional fields such as partner\_business\_id and cta values.

Business Info

`GET https://partner-api.yelp.com/v1/business_info/<business_ids>`

Request parameters

- business\_ids
- Comma-delimited list of yelp business ids. Supports up to 200 ids.

Response parameters

- name
- address1
- address2
- address3
- city
- country
- state
- postal\_code
- latitude
- longitude
- phone
- url
- display\_url
- is\_migrated (if true, the destination\_yelp\_business\_id contains migrated id)
- destination\_yelp\_business\_id
- is\_closed
- is\_removed\_from\_search
- additional\_biz\_info object
 - partner\_business\_id
 - metered\_phone
 - cta object
 - category\_list

# 

Business Migration Info API

Given a Yelp encrypted business id, this API provides information about the migration path of a business.

Business Migration Info

`GET https://partner-api.yelp.com/v1/business_migration_info/<business_ids>`

Request parameters

- business\_ids
- Comma-delimited list of yelp business ids. Supports up to 200 ids.

Response Parameters

- migration\_type (MIGRATED, NONE)
- destination\_business\_id (id that the requested yelp\_business\_id has been migrated to)
- merged\_business\_ids (list of ids that have been merged into this biz)

# 

Program Info API

Given a Yelp program id, this API returns the details of the advertising program.

Program Info

`GET https://partner-api.yelp.com/v1/programs/info/<program_ids>`

Request parameters

- Comma-delimited list of program\_ids (up to 200 program\_ids)
- start (what index should the list start at, used as an offset to paginate through the complete list of programs)

Response parameters

- partner\_business\_id
- program\_type (BP, CPC)
- start\_date
- end\_date
- program\_status (ACTIVE, INACTIVE)
- program\_pause\_status (PAUSED, NOT\_PAUSED)
- program\_metrics
 - budget
 - currency
 - is\_autobid
 - max\_bid
 - billed\_impressions
 - billed\_clicks
 - ad\_cost
 - fee\_period (Calendar Month, Rolling Month)
- future\_budget\_changes
 - new\_budget
 - start\_date
 - old\_budget
- page\_upgrade\_info
 - monthly\_rate
 - cost
- active\_features (LINK\_TRACKING, NEGATIVE\_KEYWORD\_TARGETING, STRICT\_CATEGORY\_TARGETING, AD\_SCHEDULING, CUSTOM\_LOCATION\_TARGETING, AD\_GOAL, CALL\_TRACKING, SERVICE\_OFFERINGS\_TARGETING)
- available\_features (LINK\_TRACKING, NEGATIVE\_KEYWORD\_TARGETING, STRICT\_CATEGORY\_TARGETING, AD\_SCHEDULING, CUSTOM\_LOCATION\_TARGETING, AD\_GOAL, 
 CALL\_TRACKING, SERVICE\_OFFERINGS\_TARGETING)

# 

Program List API

Given a Yelp encrypted business id, this API returns the list of past, current and future advertising programs with info for each program (status, start/end date).

Program List

`https://partner-api.yelp.com/v1/programs/list/<business_ids>start=0&limit=20`

Request parameters

- business\_ids - Comma-delimited list of yelp business ids. Supports up to 200 ids.
- Pagination for programs within each business:
 - start - Integer (Default: 0, Minimum: 0)
 - limit - Integer (Default: 20, Minimum: 0, Maximum: 40)

Response parameters

- yelp\_business\_id
- destination\_yelp\_business\_id
 - Contains the yelp business id that this business was merged into.
 - null if business wasn't merged. (most common case)
- advertiser\_status
- partner\_business\_id
- array of advertising programs\_id
 - program\_type (BP, CPC)
 - program\_id
 - start\_date
 - end\_date
 - program\_status (ACTIVE, INACTIVE)
 - program\_pause\_status (PAUSED, NOT\_PAUSED)
- program\_metrics
 - budget
 - currency
 - is\_autobid
 - max\_bid
 - billed\_impressions
 - billed\_clicks
 - ad\_cost
 - fee\_period (Calendar Month, Rolling Month)
- future\_budget\_changes
 - new\_budget
 - start\_date
 - old\_budget
- page\_upgrade\_info
 - monthly\_rate
 - cost
- available\_features (LINK\_TRACKING, NEGATIVE\_KEYWORD\_TARGETING, STRICT\_CATEGORY\_TARGETING, AD\_SCHEDULING, CUSTOM\_LOCATION\_TARGETING, AD\_GOAL, CALL\_TRACKING, SERVICE\_OFFERINGS\_TARGETING)
- active\_features (LINK\_TRACKING, NEGATIVE\_KEYWORD\_TARGETING, STRICT\_CATEGORY\_TARGETING, AD\_SCHEDULING, CUSTOM\_LOCATION\_TARGETING, AD\_GOAL, CALL\_TRACKING, SERVICE\_OFFERINGS\_TARGETING)

# 

Program List All API

Returns the entire the list of past, current and future advertising programs under a given payment account with info for each program (status, start/end date).

Program List All

`GET https://partner-api.yelp.com/programs/v1`

Request query parameters

- offset (optional - default: 0)
- limit (optional - default: 20 \[min: 1, max: 40\])
- program\_status \[PAST, PAUSED, CURRENT, FUTURE, ALL\] (optional - default: current)

Response parameters

- program\_status
- total (number of payment programs that match selected program status)
- limit
- offset
- array of payment\_programs
 - program\_type (BP, CPC, EP)
 - program\_id
 - start\_date
 - end\_date
 - program\_status (ACTIVE, INACTIVE)
 - program\_pause\_status (PAUSED, NOT\_PAUSED)
 - program\_metrics
 - budget
 - currency
 - is\_autobid
 - max\_bid
 - billed\_impressions
 - billed\_clicks
 - ad\_cost
 - fee\_period (Calendar Month, Rolling Month)
 - array of businesses
 - yelp\_business\_id
 - partner\_business\_id
 - future\_budget\_changes
 - new\_budget
 - start\_date
 - old\_budget
 - page\_upgrade\_info
 - monthly\_rate
 - cost
 - active\_features (LINK\_TRACKING, NEGATIVE\_KEYWORD\_TARGETING, STRICT\_CATEGORY\_TARGETING, AD\_SCHEDULING, CUSTOM\_LOCATION\_TARGETING, AD\_GOAL, CALL\_TRACKING, SERVICE\_OFFERINGS\_TARGETING)
 - available\_features (LINK\_TRACKING, NEGATIVE\_KEYWORD\_TARGETING, STRICT\_CATEGORY\_TARGETING, AD\_SCHEDULING, CUSTOM\_LOCATION\_TARGETING, AD\_GOAL, CALL\_TRACKING, SERVICE\_OFFERINGS\_TARGETING)

> ## 📘
> 
> Check out our Partner Support API Reference Page
> 
> ![:owlbert:](https://docs.developer.yelp.com/public/img/emojis/owlbert.png) [Endpoints](https://docs.developer.yelp.com/reference/get_program_list_all)

Updated over 2 years ago

---

Did this page help you?

Yes

No

Copy Page