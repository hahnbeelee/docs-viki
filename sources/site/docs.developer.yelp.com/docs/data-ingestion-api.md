# Source: https://docs.developer.yelp.com/docs/data-ingestion-api

> ## 📘
> 
> This is a Yelp Partner API
> 
> Access is disabled by default. See [Yelp Partner APIs](https://docs.developer.yelp.com/docs/yelp-partner-apis) on how to get access.

# 

Overview

The Yelp Data Ingestion API provides a means for partners to programmatically perform updates on a large number of businesses asynchronously. Partners can perform updates on various attributes. The businesses and fields that can be updated are contract-dependent. Access to the Data Ingestion API is reserved for contracted Yelp partners.

The API has two endpoints:

1. **Creating an ingestion job** 
 Given a set of businesses and desired attribute updates, an ingestion job will be created. The job represents a set of updates that will be performed on Yelp businesses.
2. **Querying the status of an ingestion job** 
 Given an ingestion job ID, return the status of the job. The status will describe whether the job as a whole has been completed as well as the status of individual updates.

# 

Authentication

Authentication uses basic HTTP authentication over SSL. Credentials are provided separately.

# 

Versioning

To maintain backwards-compatibility with partner-developed applications, the Yelp Data Ingestion API is versioned with the version encoded in the URI. The current and latest version is v1 and all endpoints are located at `https://partner-api.yelp.com/v1/`.

# 

Format

Request and response bodies use the application/json content type and should be encoded in UTF-8. This format supports special characters (e.g. ‘ & / % etc.).

# 

Identifiers

Yelp identifiers are unique within a type of object only; they are not globally unique. For example, a photo and business may share the same identifier, WavvLdfdP6g8aZTtbBQHTw, but no other photo or business will have that same identifier. 

# 

Value Types

All datetime properties should use the [ISO 8601 format](http://en.wikipedia.org/wiki/ISO_8601) and be stored in UTC.

All time properties should use the format HH:MM\[:SS\] and be timezone-agnostic.

Submitting values as an empty string will attempt to delete that current value for that attribute. Generally speaking, please don't send empty string values for attributes. The only exception is for metered\_phone - if you'd like to delete the shown call tracking number, that's fine.

# 

Rate Limiting

The default rate limits are: 
**Creating an ingestion job** - 2500 requests per 30 minutes. 
**Querying the status of an ingestion job** - 2500 requests per 30 minutes.

# 

Standards and Best Practices

Please reference our business submission standards [guide](https://docs.developer.yelp.com/docs/yelp-data-quality-guidelines).

**How empty "" and _null_ values are treated**: 
Anything included in the "update" section will be applied to the location. Please only include updates when you're intentionally changing the value of a specific attribute. Submitting empty "" & _null_ values will delete the current Yelp value for that attribute. For example, submitting an update of _{"address1": ""}_ will delete the current value of address1.

# 

Resource Types

The Data Ingestion API currently supports the following resources:

- [Business](https://docs.developer.yelp.com/#di_api_resource_types_business)
- [Business Photo](https://docs.developer.yelp.com/#di_api_resource_types_business_photo)
- [Business Result](https://docs.developer.yelp.com/#di_api_resource_types_business_result)
- [Call to Action – Desktop](https://docs.developer.yelp.com/#di_api_resource_types_cta_desktop)
- [Call to Action – Mobile](https://docs.developer.yelp.com/#di_api_resource_types_cta_mobile)
- [Currency](https://docs.developer.yelp.com/#di_api_resource_types_currency)
- [Error](https://docs.developer.yelp.com/#di_api_resource_types_error)
- [Job](https://docs.developer.yelp.com/#di_api_resource_types_job)
- \[Job Response\](#di\_api\_resource\_types\_job response)
- \[Job Status\](#di\_api\_resource\_types\_job status)
- [Menu Data](https://docs.developer.yelp.com/#di_api_resource_types_menu_data)
- [Menu Item](https://docs.developer.yelp.com/#di_api_resource_types_menu_item)
- [Menu Text](https://docs.developer.yelp.com/#di_api_resource_types_menu_text)
- [Platform Service](https://docs.developer.yelp.com/#di_api_resource_types_platform_service)
- [Platform Service Area](https://docs.developer.yelp.com/#di_api_resource_types_platform_service_area)
- [Platform Service Area Polygon](https://docs.developer.yelp.com/#di_api_resource_types_platform_service_area_polygon)
- [Platform Service Type](https://docs.developer.yelp.com/#di_api_resource_types_platform_service_type)
- [Linkout Data Type](https://docs.developer.yelp.com/#di_api_resource_types_linkout_data)
- [Medical Provider Location Type](https://docs.developer.yelp.com/#di_api_resource_types_medical_provider_locations)
- [Promotions Data Type](https://docs.developer.yelp.com/#di_api_resource_types_promotions_data)
- [Result](https://docs.developer.yelp.com/#di_api_resource_types_result)

## 

Business

JavaScript

`{ 	"matching_criteria": { 		"address1": {string}, 		"address2": {string}, 		"address3": {string}, 		"city": {string}, 		"country": {string}, 		"latitude": {double}, 		"longitude": {double}, 		"name": {string}, 		"phone": {string}, 		"postal_code": {string}, 		"state": {string}, 		"yelp_business_id": {string} 	}, 	"options": { 		"create_if_missing": {boolean}, 		"use_matching_criteria_for_update": {boolean}, 	}, 	"partner_business_id": {string}, 	"update": { 		"about_this_business_history": {string}, 		"about_this_business_specialties": {string}, 		"about_this_business_year_established": {string}, 		"about_this_business_bio": {string}, 		"about_this_business_bio_first_name": {string}, 		"about_this_business_bio_last_name": {string}, 		"accepts_credit_cards": {boolean}, 		"accepts_insurance": {boolean}, 		"address1": {string}, 		"address2": {string}, 		"address3": {string}, 		"alcohol": {string}, 		"by_appointment_only": {boolean}, 		"categories": [ 			{string} 		], 		"caters": {boolean}, 		"city": {string}, 		"closed": {boolean}, 		"coat_check": {boolean}, 		"comment": {string}, 		"contactless_delivery": {boolean}, 		"contactless_payment": {boolean}, 		"country": {string}, 		"covid_19_virus_response": {string}, 		"curbside_pickup": {boolean}, 		"customers_must_wear_masks": {boolean}, 		"delivery": {boolean}, 		"desktop_cta": Call to Action – Desktop Object, 		"display_url": {string}, 		"dogs_allowed": {boolean}, 		"drive_thru": {boolean}, 		"employees_wear_gloves": {boolean}, 		"employees_wear_masks": {boolean}, 		"group_bookings": {boolean}, 		"group_name": {string}, 		"happy_hour": {boolean},     "has_storefront_address": {boolean}, 		"has_tv": {boolean}, 		"hours": [ 			{ 				"day": {string}, 				"date": {date}, 				"open": {time}, 				"close": {time}, 				"action": {string} 			} 		], 		"in_store_shopping": {boolean}, 		"is_customer": {boolean}, 		"is_black_owned": {boolean}, 		"is_latinx_owned": {boolean}, 		"is_owner_verified": {boolean}, 		"latitude": {double}, 		"limited_capacity": {boolean}, 		"longitude": {double}, 		"menu_data": Menu Data Object, 		"menu_url": {string}, 		"mobile_cta": Call to Action – Mobile Object, 		"name": {string}, 		"parking": { 			"garage": {boolean}, 			"lot": {boolean}, 			"street": {boolean}, 			"valet": {boolean}, 			"validated": {boolean} 		}, 		"metered_phone": {string}, 		"outdoor_seating": {boolean}, 		"opening_date": {date}, 		"on_premise_access": {boolean}, 		"phone": {string}, 		"photos": [ 			Business Photo Object, 		], 		"platform_service": Platform Service Object, 		"postal_code": {string}, 		"provides_santizers_to_customers": {boolean}, 		"proof_of_vaccination_required": {boolean}, 		"sanitizing_between_customers": {boolean}, 		"service_area": [ 			{string} 		], 		"service_offerings": Service Offerings Object,  		"jobs_data": Jobs Data Object (Coming soon), 		"smoking": {string}, 		"social_distancing": {boolean}, 		"staff_fully_vaccinated": {boolean}, 		"state": {string}, 		"store_code": {string}, 		"take_out": {boolean}, 		"takes_reservations": {boolean}, 		"temperature_check": {boolean}, 		"temporarily_closed": {date}, 		"url": {string}, 		"waiter_service": {boolean}, 		"wheelchair_accessible": {boolean}, 		"wifi": {string}, 		"linkout_data": [Linkout Data Object], 		"medical_provider_locations": [Medical Provider Location Object], 		"promotions_data":[Promotions Data Object]  	} }`

| Property Name | Value | Required | Description |
| --- | --- | --- | --- |
| matching\_criteria | object | | Provides information to find a matching business on Yelp. |
| matching\_criteria.address1 | string | No | The first line of the business’s address. Maximum length is 64; only digits, letters, spaces, and \_-’/#&,.': are allowed. |
| matching\_criteria.address2 | string | No | The second line of the business’s address. Maximum length is 64; only digits, letters, spaces, and \_-’/#&,.': are allowed. |
| matching\_criteria.address3 | string | No | The third line of the business’s address. Maximum length is 64; only digits, letters, spaces, and \_-’/#&,.': are allowed. |
| matching\_criteria.city | string | Yes | The city of the business. Maximum length is 64; only digits, letters, spaces, and \_-’.() are allowed. In the US when updating businesses in Washington DC, please submit as city: "Washington" state: "DC" not as city: "Washington, DC" |
| matching\_criteria.country | string | Yes | The ISO 3166-1 alpha-2 country code of the business. Maximum length is 2. |
| matching\_criteria.latitude | double | No | The WGS84 latitude of the business in decimal degrees. Must be between -90 and 90. |
| matching\_criteria.longitude | double | No | The WGS84 longitude of the business in decimal degrees. Must be between -180 and 180. |
| matching\_criteria.name | string | Yes | The name of the business. Maximum length is 64; only digits, letters, spaces, and \_!#$%&+,-.’/:?@' are allowed. |
| matching\_criteria.phone | string | No | The phone number of the business, either (a) locally-formatted with digits only (e.g., 016703080) or (b) internationally-formatted with a leading + sign and digits only after (+35316703080). Maximum length is 32. |
| matching\_criteria.postal\_code | string | Yes | The postal code of the business. Maximum length is 12. If submitting zip+4 for US listings use this format "xxxxx-xxxx" |
| matching\_criteria.state | string | Yes | The ISO 3166-2 code for the region/province of the business. Maximum length is 3. |
| matching\_criteria.yelp\_business\_id | string | No (Required in phase 1 only) | Unique Yelp identifier of the business if available. Used as a hint when finding a matching business. |
| options | object | | Options for handling the business. |
| options.create\_if\_missing | boolean | | Whether to create the business if no matching business is found. Defaults to true if not specified. |
| options.use\_matching\_criteria\_for\_update | boolean | | Whether to use the information in the matching criteria to also update the business. When true, the fields from the matching\_criteria are merged into the update object. Any fields already present in the update object take precedence. Defaults to false if not specified. |
| partner\_business\_id | string | | Optional unique partner identifier for the business. Must not contain leading or trailing spaces. When provided, partner identifiers cannot change and must remain unique. Maximum length is 100. |
| update | object | | Provides rich content for the business. |
| update.about\_this\_business\_history | string | | The history of the business. Minimum length is 15, maximum is 1,000; URLs, all caps, and HTML tags are not allowed. Please note: "about\_this\_business\_year\_established" also needs to be populated for this field to be visible on the listing. This field is reserved for current Yelp advertisers. |
| update.about\_this\_business\_specialties | string | | The specialties of the business. Minimum length is 15, maximum is 1,500; URLs, all caps, and HTML tags are not allowed. Business description will map to this attribute. This field is reserved for current Yelp advertisers. |
| update.about\_this\_business\_year\_established | string | | The 4-digit year that the business was established. Year must be no greater than the year following today’s date (e.g., 2015 on 5/1/2014). Please note: "about\_this\_business\_history" also needs to be populated for this field to be visible on the listing. This field is reserved for current Yelp advertisers. |
| update.about\_this\_business\_bio | string | | Brief biographical information about the business account holder. Minimum length is 15, maximum is 1,000; URLs, all caps, and HTML tags are not allowed. This field is reserved for current Yelp advertisers. |
| update.about\_this\_business\_bio\_first\_name | string | | The first name of the business owner. Maximum length is 59. This field is reserved for current Yelp advertisers. |
| update.about\_this\_business\_bio\_last\_name | string | | The first initial of the business owner’s last name. Minimum length is 1, maximum is 1. This field is reserved for current Yelp advertisers. |
| update.accepts\_credit\_cards | boolean | | Whether the business accepts credit cards for payments. |
| update.accepts\_insurance | boolean | | Whether the business accepts insurance for payment. |
| update.address1 | string | | The first line of the business’s address. Maximum length is 64; only digits, letters, spaces, and \_-’/#&,.: are allowed. |
| update.address2 | string | | The second line of the business’s address. Maximum length is 64; only digits, letters, spaces, and \_-’/#&,.: are allowed. |
| update.address3 | string | | The third line of the business’s address. Maximum length is 64; only digits, letters, spaces, and \_-’/#&,.: are allowed. |
| update.alcohol | string | | Whether the business serves alcohol. Possible values are: 
 
**"none"** - No alcohol is served. 
**"beer\_and\_wine"** – Only beer & wine are available. 
**"full\_bar"** – Beer, wine & spirits are available. |
| update.by\_appointment\_only | boolean | | Whether the business views patrons by appointment only. |
| update.categories\[\] | list | | The categories, as [Yelp aliases](https://docs.developer.yelp.com/docs/resources-categories), for the business. Case-sensitive. Maximum of 3 leaf categories. Please Note: categories can only be added to locations that don't currently have a category. Any update attempts to change/update existing categories will fail. 
 
Yelp aliases can be found at the [Category List Page](https://docs.developer.yelp.com/docs/resources-categories) or using the [Categories API endpoint.](https://docs.developer.yelp.com/reference/v3_all_categories) |
| update.caters | boolean | | Whether the business offers catering. |
| update.city | string | | The city of the business. Maximum length is 64; only digits, letters, spaces, and -’.() are allowed. |
| update.closed | boolean | | Whether the business is permanently closed. |
| update.coat\_check | boolean | | Whether the business offers a coat check. |
| update.comment | string | | Optional comment, preferably from the end user, for this update. Maximum length is 4,500; all caps and HTML tags are not allowed. |
| update.contactless\_delivery | boolean | | Does the business offer contactless delivery? |
| update.contactless\_payment | boolean | | Apply if business allows contactless payments such as Apple Pay, Android Pay, etc. |
| update.country | string | | The ISO 3166-1 alpha-2 country code of the business. Maximum length is 2. |
| update.covid\_19\_virus\_response | string | | A covid related message that's relevant and useful for consumers. Phone numbers, websites link, social media links that represent the business may be included. 1500 characters maximum. 
 
Example of an acceptable message: “Effective March 17th, all locations will be closed. Our plan is to reopen on April 7th depending on the COVID-19 situation at that time. Thank you” |
| update.curbside\_pickup | boolean | | Does the business offer curbside pickup? |
| update.customers\_must\_wear\_masks | boolean | | Apply if business requires all customers to wear a mask. |
| update.delivery | boolean | | Whether the business offers delivery. |
| update.desktop\_cta | nested object | | Create, update, or end a desktop call to action offer using a Call to Action – Desktop resource. |
| update.display\_url | string | | What will display on the Yelp page as the external url to direct to. Note the "url" field dictates the destination of a consumer's click, display\_url is simply what's displayed. We suggest keeping it simple like www.brand.com or location subpages are fine too like www.brand.com/locations/abc. Please don't include UTMs or other tracking parameters. |
| update.dogs\_allowed | boolean | | Whether dogs are allowed at the business. |
| update.drive\_thru | boolean | | Whether the business has a drive-thru. Only available for businesses with a 'restaurants' parent category. |
| update.employees\_wear\_gloves | boolean | | Apply if business employees wear gloves when in contact with customers or goods. |
| update.employees\_wear\_masks | boolean | | Apply if business employees wear masks when in contact with customers or goods. |
| update.group\_bookings | boolean | | Whether business offers group bookings. |
| update.group\_name | string | | The group name for this location. |
| update.happy\_hour | boolean | | Whether the business has a happy hour. |
| update.has\_storefront\_address | boolean | | Whether the business has a physical address that consumers can visit. For businesses like plumbers who travel to the consumer's location and don't have a physical office that's consumer facing, this field should be set to False. |
| update.has\_tv | boolean | | Whether the business has televisions. |
| update.hours\[\] | list | | The operating hours of the business. Multiple entries can exist for the same day (e.g., a business is open for lunch and dinner but closes in between). To set a business open 24 hours, set both the "open" and "close" fields to 00:00. To set a business to be closed for a specific day of the week, don't include that day in the list. |
| update.hours\[\].day | string | | The full day of the week, in English, for the hours. Possible values are: 
 
"monday" 
"tuesday" 
"wednesday" 
"thursday" 
"friday" 
"saturday" 
"sunday" |
| update.hours\[\].date | date | | Used to denote special hours for a specific date. This is typically used for holidays where the location will have hours that differ from their standard hours. Display rules for special hours on yelp.com: we'll show hours for the current week (today - Sunday). For example, if on Wednesday you submit special hours for the coming Tuesday, those hours will be displayed on the page on the coming Monday. The expected format when submitting special hours will look like below, don't include day if sending us a date: 
 
{ "date": "2019-12-31", "close": "01:00", "open": "11:00" } |
| update.hours\[\].open | time | | The time the business opens on the specified day or date. |
| update.hours\[\].close | time | | The time the business closes on the specified day or date. The close time can be earlier than the open time if the business closes the following day (e.g., opens at 7 PM and closes at 2 AM). |
| update.hours\[\].action | string | | This field should be used in conjunction with hours\[\].date to denote what kind of special hours apply to a specific calendar date. The accepted values are: 
 
**"usual"**\- regular business hours apply. 
**"closed"**\- the business is closed. 
**"delete"**\- deletes the previously set special hours. 
 
Sample request format: 
{ "date": "2020-04-17", "action": "usual" } |
| update.in\_store\_shopping | boolean | | Apply if the business is open for in-store shopping. This is especially important during COVID-19, as many businesses are open but allow only curbside pickup or offer only online services. Only avialable in select categories, see here: https://docs.google.com/spreadsheets/d/1acWX0FYvLgzBlaq\_3KGKi6CMQpw7SKbcoVC1k0xf6MQ/edit#gid=1565462503 |
| update.is\_customer | boolean | | Whether the business is a paying client. This is used to indicate the relationship a partner has with the business. false is assumed unless provided. |
| update.is\_black\_owned | boolean | | Whether the business is black owned. |
| update.is\_latinx\_owned | boolean | | Whether the business is latinx owned. |
| update.is\_owner\_verified | boolean | | Whether the owner of the business has verified its information. false is assumed unless provided. |
| update.jobs\_data | object | | A list of the jobs a services business can offer to its customers. To understand how to submit this data, please request support from partner-support@yelp.com. |
| update.latitude | double | | The WGS84 latitude of the business in decimal degrees. Must be between -90 and 90. |
| update.limited\_capacity | boolean | | Apply if business accepts customers in limited capacity (in order to comply with social distancing guidelines. |
| update.longitude | double | | The WGS84 longitude of the business in decimal degrees. Must be between -180 and 180. |
| update.menu\_data | nested object | | Menu data, as a Menu Data resource, for the business. |
| update.menu\_url | string | | The business’s menu URL. Maximum length is 2,000; only digits, ASCII letters, and !"#$%&'()\*+,-./:;<=>?@\[\\\]^\_\`{|}~ are allowed. Must start with http:// or https://. Links to Facebook, Twitter, Google Plus, or other directories are not allowed in most cases. |
| update.mobile\_cta | nested object |  | Create, update, or end a mobile call to action offer using a Call to Action – Mobile resource. |
| update.name | string |  | The name of the business. Maximum length is 64; only digits, letters, spaces, and \_!#$%&+,-./:?@' are allowed. |
| update.opening\_date | date |  | The estimated opening date of a business. Expected format: mm/dd/yyyy |
| update.parking | object |  | The types of parking available for the business. |
| update.parking.garage | boolean |  | Whether a garage or deck is available. |
| update.parking.lot | boolean |  | Whether a lot is available. |
| update.parking.street | boolean |  | Whether street parking is available. |
| update.parking.valet | boolean |  | Whether valet parking is available. |
| update.parking.validated | boolean |  | Whether validated parking is available. |
| update.metered\_phone | string |  | The call tracking number of the business, either (a) locally-formatted with digits only (e.g., 016703080) or (b) internationally-formatted with a leading + sign and digits only after (+35316703080). Maximum length is 32. If metered\_phone is sent, then the phone must also be sent. |
| update.on\_premise\_access | boolean |  | Apply if business is open for in-store visit, this is equivalent of sit down for restaurants. Only avialable in select categories, see here: https://docs.google.com/spreadsheets/d/1acWX0FYvLgzBlaq\_3KGKi6CMQpw7SKbcoVC1k0xf6MQ/edit#gid=1565462503 |
| update.phone | string |  | The phone number of the business, either (a) locally-formatted with digits only (e.g., 016703080) or (b) internationally-formatted with a leading + sign and digits only after (+35316703080). Maximum length is 32. |
| update.photos\[\] | list |  | Photos, as Business Photo resources, for the business. |
| update.platform\_service | nested object |  | Platform service information, as a Platform Service resource, for the business. |
| update.postal\_code | string |  | The postal code of the business. Maximum length is 12. |
| update.provides\_santizers\_to\_customers | boolean |  | Apply if business provides sanitizers or wipes to customers. |
| update.proof\_of\_vaccination\_required | boolean |  | Apply if business requires proof of covid-19 vaccination by customers. |
| update.outdoor\_seating | boolean |  | Whether the business offers outdoor seating. |
| update.sanitizing\_between\_customers | boolean |  | Let users know whether the business regularly conducts disinfection practices after each customer visit. |
| update.service\_area\[\] | list of strings |  | The additional locations serviced by the business. Locations must be expressed as unambiguous postal codes or neighborhood- city-state-country combinations. Maximum of 6 locations; distance between locations cannot exceed 100 miles. Example of an acceptable input: \["73768","Ringwood,OK"\] \*Please note: this attribute is used to show what areas a plumber might service. This attribute is different from "Platform Service Area". |
| update.service\_offerings\[\] | object |  | A list of the services a business can offer to its customers. To request a list of currently available service offerings, please request this from partner-support@yelp.com. |
| update.service\_offerings\[\].alias | string |  | The alias of the service offerings. Example:"offers\_virtual\_classes" |
| update.service\_offerings\[\].value | boolean |  | Wheter this service offerings is available . |
| update.smoking | string |  | Whether smoking is allowed at the business. Possible values are:  
  
**"no"** – Smoking is not allowed.  
**"yes"** – Smoking is allowed.  
**"outdoor"** – Smoking is only allowed outside. |
| update.social\_distancing | boolean |  | Apply for businesses adhering to social distancing norms for its customers. Every business type is different, for example, a business could provide increased spacing between persons to maintain at least six feet distance at all times. This could also mean additional spacing between booths, divider shields or other makeshift partitions . |
| update.staff\_fully\_vaccinated | boolean |  | Apply if the business staff is fully vaccinated against covid-19. |
| update.state | string |  | The ISO 3166-2 code for the region/province of the business. Maximum length is 3. |
| update.store\_code | string |  | The store code for this location. |
| update.take\_out | boolean |  | Whether the business offers take-out. |
| update.takes\_reservations | boolean |  | Whether the business takes reservation. |
| update.temperature\_check | boolean |  | Apply if business checks customers temperature at the store front. |
| update.temporarily\_closed | date |  | A future date the business should be temporarily closed until. Temporarily closing a business means that not only is the storefront closed, but it's also not conducting any business or providing any services at all (for example, no takeout, delivery, any virtual services, etc.). In addition, temporarily closed businesses will not be shown in search results, unless searched by name.  
  
Expected format is mm/dd/yyyy.  
  
  
To end the temporarily closed status of a business, aka reopen the business immediately, submit an empty string "" in place of a real date.  
  
Example request format to remove the temporarily closed status:  
{"temporarily\_closed": ""} |
| update.url | string |  | The business’s website URL. Maximum length is 255; only digits, ASCII letters, and !"#$%&'()\*+,-./:;<=>?@\[\\\]^\_\`{|}~ are allowed. Must start with http:// or https://. Links to Facebook, Twitter, Google Plus, or other directories are not allowed in most cases. |
| update.waiter\_service | boolean | | Whether the business has waiter service. |
| update.wheelchair\_accessible | boolean | | Whether the business is wheelchair-accessible. |
| update.wifi | string | | Whether the business offers Wi-Fi. Possible values are: 
 
**"no"** – WiFi is not available. 
**"paid"** – Paid WiFi is available. 
**"free"** – Free WiFi is available. |
| update.linkout\_data | List of nested object Linkout Data Type | | Linkout Data information, as a Linkout Data resource, for the business. |

## 

Business Photo

JavaScript

`{ 	"caption": {string}, 	"url": {string} }`

Note that photos must be larger than 100x100 and smaller than 8000x8000 to be considered valid.

If you want to delete photos, please goto the [Delete Photo](https://docs.developer.yelp.com/#di_api_delete_photo) section.

| Property Name | Value | Description |
| --- | --- | --- |
| caption | string | The caption of the photo. Maximum length is 128, only digits, letters, spaces, and !"#$%&\\'()\*+,-./:;=?@\[\\\\\]^\_\`{|}~ are allowed. |
| url | string | The photo’s full-size image URL. |

## 

Business Result

JavaScript

`{ 	"error": Error Object, 	"partner_business_id": {string}, 	"status": {string}, 	"update_results": { 		{(key)}: Result Object 	}, 	"yelp_business_id": {string} }`

| Property Name | Value | Description |
| --- | --- | --- |
| error | nested object | Error that occurred when processing the business. Only present if the status is "REJECTED" or "FAILED". |
| partner\_business\_id | string | Partner business ID provided in the original request. If no ID was provided, this field is not present. |
| status | string | Overall status of the business. Possible values are:  
  
**"PROCESSING"** – the business is being processed  
**"COMPLETED"** – the business is completed  
**"REJECTED"** – the business was rejected  
**"FAILED"** – the business update failed due to an internal error |
| update\_results | object | Status of individual attributes. |
| update\_results.(key) | string | Name of the attribute. |
| yelp\_business\_id | string | Unique Yelp identifier for the business.  
  
Note: It takes 30-60 seconds for Yelp to process each job, so the yelp\_business\_id will be set to ‘null’ temporarily. We recommend that you wait at least 5 minutes before you poll the job, though most jobs will return yelp\_business\_id within 1 minute. |

## 

Call to Action – Desktop

JavaScript

`{ 	"create": { 		"button_text": {string}, 		"end_date": {date}, 		"text": {string}, 		"url": {string} 	}, 	"end": {boolean} }`

| Property Name | Value | Description |
| --- | --- | --- |
| create | object | Create a new CTA or replace a currently running CTA. Either "create" or "end" must be specified, but both can’t be used in the same request. |
| create.button\_text | string | Text for the button. Must be one of the following values in the appropriate language (French, German, English, or Spanish):  
  
Apply Now  
Book Appointment  
Book Now  
Buy Tickets  
Check Availability  
Contact Us  
Enroll Now  
Get Directions  
Get Offer  
Get Quote  
Join Now  
Learn More  
Make Reservation  
Order Online  
Print Coupon  
Print Voucher  
Reserve Now  
Schedule Appointment  
View Now  
Visit Location  
  
If a button is specified, "url" must also be provided. Set to null if no button is desired. Required. |
| create.end\_date | date | End date for the offer. if not specified, offer runs indefinitely. |
| create.text | string | Additional information about the offer (e.g., "$1 First Month’s Rent! No credit card required"). Maximum length is 50, new lines and brackets (<>) are not allowed. Required. |
| create.url | string | URL for the offer. Maximum length is 2,000; only digits, ASCII letters, and !"#$%&'()\*+,-./:;<=>?@\[\\\]^\_\`{|}~ are allowed. Must start with http:// or https://. Links to Facebook, Twitter, Google Plus, or other directories are not allowed in most cases. Required if "button" is not null. |
| end | boolean | End a currently running CTA if set to true. Either "create" or "end" must be specified, but both can’t be used in the same request. |

## 

Call to Action – Mobile

JavaScript

`{ 	"create": { 		"action_text": {string}, 		"description_text": {string}, 		"end_date": {date}, 		"url": {string} 	}, 	"end": {boolean} }`

| Property Name | Value | Description |
| --- | --- | --- |
| create | object | Create a new CTA or replace a currently running CTA. Either "create" or "end" must be specified, but both can’t be used in the same request. |
| create.action\_text | string | Call to action text (e.g., "Call Now for $1 First Month!"). Maximum length is 30, new lines and brackets (<>) are not allowed. Required. |
| create.description\_text | string | Additional information about the offer (e.g., "No credit card required, no obligation."). Maximum length is 50, new lines and brackets (<>) are not allowed. Required. |
| create.end\_date | date | End date for the offer. If not specified, offer runs indefinitely. |
| create.url | string | URL for the offer. Maximum length is 2,000; only digits, ASCII letters, and !"#$%&'()\*+,-./:;<=>?@\[\\\]^\_\`{|}~ are allowed. Must start with http://, https://, or tel: for phone number (e.g., "tel:+14159083801"). Links to Facebook, Twitter, Google Plus, or other directories are not allowed in most cases. Required. |
| end | boolean | End a currently running CTA if set to true. Either "create" or "end" must be specified, but both can’t be used in the same request. |

## 

Call Tracking Number (CTN) Enablement

**Overview**

The Yelp Data Ingestion API allows partners to set Call Tracking Numbers (CTNs) for Yelp business listings by programmatically sending the CTN and Ring-To-Number values in the data ingestion job.

**Enable CTN**

The following business attributes must be sent in the data ingestion job. Both attributes are required in order for the update to be successful:

**metered\_phone**: Set the CTN value to this attribute

**phone**: Set the Ring-To-Number value to this attribute

Example:

Request

JavaScript

`{ 	"businesses": [ 		{ 			"matching_criteria": { 				"address1": "800 N Point St", 				"address2": null, 				"address3": null, 				"city": "San Francisco", 				"country": "US", 				"latitude": 37.8058024, 				"longitude": -122.420582, 				"name": "Gary Danko", 				"phone": "+14157492060", 				"postal_code": "94109", 				"state": "CA" 				"yelp_business_id": "WavvLdfdP6g8aZTtbBQHTw" 			}, 			"options": { 				"create_if_missing": false, 				"use_matching_criteria_for_update": false, 			}, 			"partner_business_id": "12345", 			"update": { 							"metered_phone": "+18005551212", 							"phone": "+14157492060" 			} 		} 	] }`

**Disable CTN**

If the CTN is no longer active, the CTN can be disabled by one of two methods:

1.) By ending the Branded Profile or CPC or EP program for the business listing. Please refer to the [Ads API](https://docs.developer.yelp.com/docs/ads-api)\] document for details on terminating a Branded or Enhanced Profile Program

2.) By setting the metered\_phone attribute to an empty string. This will remove the CTN from the Yelp listing and display the phone number again on the listing. Please note that both the metered\_phone and phone attributes need to be sent and set to the following values:

**metered\_phone**: Set the value to empty string ('') to remove the CTN

**phone**: Set the Ring-To-Number value to this attribute

Example:

Request

JavaScript

`{ 	"businesses": [ 		{ 			"matching_criteria": { 				"address1": "800 N Point St", 				"address2": null, 				"address3": null, 				"city": "San Francisco", 				"country": "US", 				"latitude": 37.8058024, 				"longitude": -122.420582, 				"name": "Gary Danko", 				"phone": "+14157492060", 				"postal_code": "94109", 				"state": "CA" 				"yelp_business_id": "WavvLdfdP6g8aZTtbBQHTw" 			}, 			"options": { 				"create_if_missing": false, 				"use_matching_criteria_for_update": false, 			}, 			"partner_business_id": "12345", 			"update": { 							"metered_phone": "", 							"phone": "+14157492060" 			} 		} 	] }`

  
##Currency

JavaScript

`{ 	"amount": {string}, 	"currency_code": {string} }`

| Property Name | Value | Description |
| --- | --- | --- |
| amount | string | Currency amount with exact precision. the number of decimal places should follow [ISO 4217](http://en.wikipedia.org/wiki/ISO_4217). |
| currency\_code | string | The [ISO 4217](http://en.wikipedia.org/wiki/ISO_4217) 2-character code for the currency. Maximum length is 3. |

## 

Error

JavaScript

`{ 	"code": {string}, 	"message": {string} }`

| Property Name | Value | Description |
| --- | --- | --- |
| code | string | Standard description of the error. |
| message | string | Human-readable description of the problem, potentially including additional information for troubleshooting. |

See Appendix B: Error Code Reference for a list of possible error codes and messages.

## 

Job

JavaScript

`{ 	"businesses": [ 		Business Object 	] }`

| Property Name | Value | Description |
| --- | --- | --- |
| businesses\[\] | list | List of the businesses to create or update for this job. Maximum of 10 businesses. |

## 

Job Response

JavaScript

`{ 	"job_id": {string}, 	"error": Error Object, }`

| Property Name | Value | Description |
| --- | --- | --- |
| job\_id | string | Unique ID used to identify a Data Ingestion API job. Use to query for the status of a job. |
| error | nested object | Error that occurred when creating the job. |

## 

Job Status

JavaScript

`{ 	"business_results": [ 		Business Result Object 	], 	"error": Error Object, }`

| Property Name | Value | Description |
| --- | --- | --- |
| business\_results\[\] | list | List of the business results. Note that the results are in the same order as the original job.  
  
This list can be empty if the job is still processing. |
| error | nested object | Error that occurred when retrieving the status of the job. |

## 

Menu Data

JavaScript

`{ 	"attribution_image_url": {string}, 	"attribution_link_url": {string}, 	"attribution_text": {string}, 	"items": [ 		Menu Item Object or Menu Text Object 	], 	"menu_id": {string}, 	"menus": [ 		{ 			"description": {string}, 			"items": [ 				Menu Item Object or Menu Text Object 			], 			"name": {string}, 			"sections": [ 				{ 					"description": {string}, 					"items": [ 						Menu Item Object or Menu Text Object 					], 					"name": {string}, 					"sub_sections": [ 						{ 							"description": {string}, 							"items": [ 								Menu Item Object or Menu Text Object 							], 							"name": {string} 						} 					] 				} 			] 		} 	] }`

| Property Name | Value | Description |
| --- | --- | --- |
| attribution\_image\_url | string | URL to the image to display for attribution purposes. Maximum length is 2,000; only digits, ASCII letters, and !"#$%&'()\*+,-./:;<=>?@\[\\\]^\_\`{|}~ are allowed. Must start with http:// or https://. |
| attribution\_link\_url | string | Destination URL for the attribution image or text. URL to the image to display for attribution purposes. Maximum length is 2,000; only digits, ASCII letters, and !"#$%&'()\*+,-./:;<=>?@\[\\\]^\_\`{|}~ are allowed. Must start with http:// or https://. |
| attribution\_text | string | Text to display for attribution purposes. Maximum length is 300; only digits, letters, spaces, and !"#$%&'()\*+,-./:;=?@\[\\\]^\_\`{|}~ are allowed. |
| items\[\] | list | List of top-level items (not contained in any menu). |
| menu\_id | string | Unique identifier for the menu. Maximum length is 4,096; only digits, letters, spaces, and #$-\\&/,."\*'()% are allowed. Required. |
| menus\[\] | list | List of menus. Required. |
| menus\[\].description | string | Description for the menu. Maximum length is 7,000; only digits, letters, spaces, and !"#$%&'()\*+,-./:;=?@\[\\\]^\_\`{|}~ are allowed. |
| menus\[\].items\[\] | list | Items in the menu. |
| menus\[\].name | string | Name for the menu. Maximum length is 4,096; only digits, letters, spaces, and #$-\\&/,."\*'()% are allowed. Required. |
| menus\[\].sections\[\] | list | Sections in the menu. |
| menus\[\].sections\[\].description | string | Description for the section. Maximum length is 7,000; only digits, letters, spaces, and !"#$%&'()\*+,-./:;=?@\[\\\]^\_\`{|}~ are allowed. |
| menus\[\].sections\[\].items\[\] | list | Items in the section. |
| menus\[\].sections\[\].name | string | Name for the section. Maximum length is 4,096; only digits, letters, spaces, and #$-\\&/,."\*'()% are allowed. |
| menus\[\].sections\[\].sub\_sections\[\] | list | Sub-sections in the section. At least one of description, name, or items must be specified for sub-sections. |
| menus\[\]...sub\_sections\[\].description | string | Description for the sub-section. Maximum length is 7,000; only digits, letters, spaces, and !"#$%&'()\*+,-./:;=?@\[\\\]^\_\`{|}~ are allowed. |
| menus\[\]...sub\_sections\[\].items | string | Items in the sub-section. |
| menus\[\]...sub\_sections\[\].name | string | Name for the sub-section. Maximum length is 4,096; only digits, letters, spaces, and #$-\\&/,."\*'()% are allowed. |

## 

Menu Item

JavaScript

`{ 	"description": {string}, 	"item_options": [ 		{ 			"label": {string}, 			"price": {string} 		} 	], 	"name": {string}, 	"price": {string}, 	"type": {string} }`

| Property Name | Value | Description |
| --- | --- | --- |
| description | string | Description for the section. Maximum length is 7,000; only digits, letters, spaces, and !"#$%&'()\*+,-./:;=?@\[\\\]^\_\`{|}~ are allowed. |
| item\_options\[\] | list | Options for the item (e.g., sizes, add-ons). |
| item\_options\[\].label | string | Label for the option. Maximum length is 4,096; only digits, letters, spaces, and #$-\\&/,."\*'()% are allowed. |
| item\_options\[\].price | string | Price of the option. Maximum length is 256; only digits, ASCII letters, spaces, and $+. are allowed. When specifying a price (vs. "Market Price"), value must include currency symbol and have 2 decimal places (e.g., "$1.00"). |
| name | string | Name of the item. Maximum length is 4,096; only digits, letters, spaces, and #$-\\&/®,."\*'()% are allowed. Required. |
| price | string | Price of the item. Maximum length is 256; only digits, ASCII letters, spaces, and $+. are allowed. When specifying a price (vs. "Market Price"), value must include currency symbol and have 2 decimal places (e.g., "$1.00"). |
| type | string | Must be "MENU\_ITEM". |

## 

Menu Text

JavaScript

`{ 	"text": {string}, 	"type": {string} }`

| Property Name | Value | Description |
| --- | --- | --- |
| text | string | Text to display. Maximum length is 7,000; only digits, letters, spaces, and !"#$%&'()\*+,-./:;=?@\[\\\]^\_\`{|}~ are allowed. |
| type | string | Must be "MENU\_TEXT". |

## 

Platform Service

JavaScript

`{ 	"active": {boolean}, 	"areas": [ 		Platform Service Area Object 	], 	"ownership": {string}, 	"partner_service_id": {string}, 	"types": [ 		Platform Service Type Object 	], 	"ordering_phone": {string} }`

| Property Name | Value | Description |
| --- | --- | --- |
| active | boolean | Whether the business’s offerings are currently available. Required. |
| areas\[\] | list | List of service areas. |
| ownership | string | Provider of the offerings. Required. Possible values are:  
  
**"business"** – the business provides fulfillment-  
**"third\_party"** – a 3rd party provider provides fulfillment |
| partner\_service\_id | string | Optional unique partner identifier for the service. Must not contain leading or trailing spaces. Maximum length is 50. |
| types\[\] | list | List of service types. Required. |
| ordering\_phone | string | Optional phone number for placing an order, either (a) locally-formatted with digits only (e.g., 016703080) or (b) internationally-formatted with a leading + sign and digits only after (+35316703080). Maximum length is 32. Currently available only for select food partners. |

## 

Platform Service Area

JavaScript

`{ 	"area": {string} or Platform Service Area Polygon, 	"estimated_arrival": { 		"maximum": {integer}, 		"minimum": {integer} 	}, 	"minimum_order": Currency Object, 	"service_charges": { 		"charge": {string} or Currency Object, 		"description": {string}, 		"maximum_subtotal": Currency Object, 		"minimum_subtotal": Currency Object, 		"type": {string} 	}, 	"type": {string} }`

| Property Name | Value | Description |
| --- | --- | --- |
| area | string or nested object | Definition of the service area. Value depends on the "type" property:  
  
**"polygon"** – list of latitude/longitude pairs as a Platform Service Area Polygon resource  
**"postal\_code"** – postal code for the area as a string  
**"radius"** – radius, in miles, around the business as a string. |
| estimated\_arrival | object | Estimated arrival time window for the service area in minutes. |
| estimated\_arrival.maximum | integer | Maximum time, in minutes, for the estimated arrival time. |
| estimated\_arrival.minimum | integer | Minimum time, in minutes, for the estimated arrival time. |
| minimum\_order | nested object | Required minimum order subtotal for this service area. |
| service\_charges\[\] | list | List of service charges. |
| service\_charges\[\].charge | string or nested object | Amount of the service charge. Value depends on "type" property:  
  
**"fixed"** – the amount to charge as a Currency resource  
**"percentage"** – the percentage of the order subtotal to charge as a string. |
| service\_charges\[\].description | string | Optional description for the service charge. If not specified, "Service Charge" is used. |
| service\_charges\[\].maximum\_subtotal | nested object | Maximum order subtotal for which this service charge applies. If not specified, service charge has no upper subtotal limit. |
| service\_charges\[\].type | string | Type of service charge. Possible values are:  
  
**"fixed"** – the charge is a fixed amount  
**"percentage"** – the charge is a percentage of the order subtotal |
| type | string | Type of service area. Possible values are:  
  
**"polygon"** – an area defined by a list of latitude/longitude pairs  
**"postal\_code"** – an area defined by a postal code  
**"radius"** – an area defined by a radius, in miles, around the business. |

## 

Platform Service Area Polygon

JavaScript

`[ 	{ 		"latitude": {double}, 		"longitude": {double} 	} ]`

| Property Name | Value | Description |
| --- | --- | --- |
| latitude | double | The WGS84 latitude of a polygon point in decimal degrees. Must be between -90 and 90. |
| longitude | double | The WGS84 longitude of a polygon point in decimal degrees. Must be between -180 and 180. |

## 

Platform Service Type

JavaScript

`{ 	"exceptions": [ 			{ 				"date": {date}, 				"start": {time}, 				"end": {time} 			} 	], 	"hours": [ 			{ 				"day": {string}, 				"start": {time}, 				"end": {time} 			} 	], 	"estimate": { 		"maximum": {integer}, 		"minimum": {integer} 	}, 	"service_type": {string} }`

| Property Name | Value | Description |
| --- | --- | --- |
| exceptions\[\] | list | List of exceptions to the standard available hours of the service type. |
| exceptions\[\].date | date | The date of the exception. |
| exceptions\[\].start | time | The time the service type starts being available on the specified date. |
| exceptions\[\].end | time | The time the service type ends being available on the specified date. The end time can be earlier than the start time if the service type ends the following day (e.g., starts at 7 PM and ends at 2 AM). |
| hours\[\] | list | RThe available hours of the service type. Multiple entries can exist for the same day (e.g., a service type is available for lunch and dinner but not available in between). |
| hours\[\].day | string | The full day of the week, in English, for the hours. Possible values are:  
  
"monday"  
"tuesday"  
"wednesday"  
"thursday"  
"friday"  
"saturday"  
"sunday" |
| hours\[\].start | time | The time the service type starts being available on the specified day. Send midnight as 00:00 not 24:00 |
| hours\[\].end | time | The time the service type ends being available on the specified day. The end time can be earlier than the start time if the service type ends the following day (e.g., starts at 7 PM and ends at 2 AM). Send midnight as 00:00 not 24:00. |
| estimate | object | Estimated fulfillment time window for the service type in minutes. |
| estimate.maximum | integer | Maximum time, in minutes, for the estimated fulfillment time. |
| estimate.minimum | integer | Minimum time, in minutes, for the estimated arrival time. |
| service\_type | string | Type of service offered. Possible values are:  
  
**"booking\_at\_business"** – the business offers appointments or reservations at its location  
**"booking\_at\_customer"** – the business offers appointments or reservations at the customer’s location  
**"delivery"** – the business offers food order delivery  
**"pickup"** – the business offers food order pickup.  
**"hotel\_reservation"** – the business offers hotel room reservation,  
**"restaurant\_reservation"** – the business offers restaurant table reservation,  
**"goods\_at\_business"** – the business offers items (not food) for sale at its location,  
**"goods\_at\_customer"** – the business offers items (not food) for sale to be brought to the customer’s location (i.e. delivery),  
**"club\_service"** – the business offers club service (i.e. tables, ticketing),  
**"medical\_compliant"** – reach out to Yelp to use this service type,  
**"waitlist\_reservation"** – the business offers waitlist reservations. |

## 

Linkout Data

JavaScript

`[ 	{ 		"service_active": {boolean}, 		"service_type": {string}, 		"linkout_url": {string} 	} ]`

| Property Name | Value | Description |
| --- | --- | --- |
| service\_active | boolean | Whether the business’s service is currently available. Required. |
| service\_type | string | Service types offered by the business. Possible values are:  
  
**"pickup"** – Business offers takeout service.  
**"delivery"** – Business offers delivery service.  
**"booking"** – Business offers booking on their own site.  
  
Required. |
| linkout\_url | string | Url to linkout to external partner business. Required. |

## 

Medical Provider Locations

JavaScript

 `[ { "provider_location_id": "string", "npi": "string (optional)", "first_name": "string", "last_name": "string", "default_visit_reason_id": "string (optional)", "main_specialty_id": "string", "location": { "id": "string", "address1": "string", "address2": "string (optional)", "city": "string", "state": "string", "zip": "string", "visit_type": "string (enum: in_person | video | phone)" }, "accepted_insurance_plan_ids": ["string"], "visit_reason_ids": ["string"] } ]`

| Property Name | Value | Description |
| --- | --- | --- |
| provider\_location\_id | string | Unique identifier for the provider location. Required. |
| npi | string | National Provider Identifier (NPI) - a unique 10-digit identification number for healthcare providers in the United States. Optional. |
| first\_name | string | First name of the medical provider. Required. |
| last\_name | string | Last name of the medical provider. Required. |
| default\_visit\_reason\_id | string | Default visit reason identifier for this provider location. Optional. |
| main\_specialty\_id | string | Primary specialty identifier for the medical provider. Required. |
| location | object | Physical location details for the medical provider. See location object properties below. Required. |
| accepted\_insurance\_plan\_ids | array of strings | Array of insurance plan identifiers accepted at this provider location. Required. |
| visit\_reason\_ids | array of strings | Array of visit reason identifiers available at this provider location. Required. |

### Location Object Properties

| Property Name | Value | Description |
| --- | --- | --- |
| id | string | Unique identifier for the location. Required. |
| address1 | string | Street address of the provider location. Required. |
| address2 | string | Street address of the provider location, continued. Optional. |
| city | string | City of the provider location. Required. |
| state | string | State code of the provider location. Required. |
| zip | string | Zip code of the provider location. Required. |
| visit\_type | string | Type of visit available at this location. Possible values are:  
  
**"in\_person"** – In-person visit at the provider's location.  
**"video"** – Virtual video consultation.  
**"phone"** – Phone consultation.  
  
Required. |

## 

Promotions Data

JavaScript

`[ { "title": {string}, "description": {string}, "type": {string}, "service_type": [{string}], "starts_at": {string}, "expires_at": {string} } ]`

| Property Name | Value | Description |
| --- | --- | --- |
| title | string | The title of the promotion. Required. |
| description | string or null | A description of the promotion. |
| type | string | The source of the promotion. Possible values are:  
  
**"merchant"** – Promotion created by the merchant.  
**"platform"** – Promotion created by the platform/partner.  
  
Required. |
| service\_type | array of strings | The service types this promotion applies to. Possible values are:  
  
**"delivery"** – Business offers delivery service.  
**"takeout"** – Business offers takeout service.  
 |
| starts\_at | string or null | The start time of the promotion in ISO 8601 format. |
| expires\_at | string or null | The expiration time of the promotion in ISO 8601 format. |

  

## 

Result

JavaScript

`{ 	"error": Error Object, 	"requested_value": {string}, 	"status": {string} }`

| Property Name | Value | Description |
| --- | --- | --- |
| error | nested object | Error that occurred when processing the attribute. Only present if the status is "REJECTED" or "FAILED". |
| requested\_value | string | Requested value as provided in the original request. |
| status | string | Status of the attribute. Possible values are:  
  
**"PROCESSING"** – the attribute is being processed  
**"APPLIED"** – the attribute has been updated but is still pending review  
**"COMPLETED"** – the attribute has been updated and reviewed  
**"REJECTED"** – the attribute was rejected  
**"FAILED"** – the attribute update failed due to an internal error. |

## 

Service Offerings

JavaScript

`{ 	"alias": {string}, 	"value": {boolean} }`

| Property Name | Value | Description |
| --- | --- | --- |
| alias | string | The services offered, as Yelp aliases, by the business. Case-sensitive. Service offerings availability is dependant on the business's categories. |
| value | boolean | Does the business offer this service? true=yes, false=no. |

## 

Jobs Data

Naming note: While we talk about more generic “Jobs” to submit to this system, when we use the term “Jobs Data”, we refer to the services provided by a business. That is, the “jobs” that a service business performs, such as job\_plumbing\_repair or job\_flooring\_installation.

Jobs Data has a complex structure. If you’re interested in submitting Jobs Data, please contact us at [partner-support@yelp.com](mailto:partner-support@yelp.com) for assistance and onboarding.

JavaScript

`[ { "job_alias": {string}, "value": {boolean}, "job_attributes": [Job Attribute Object] } ]`

| Property Name | Value | Description |
| --- | --- | --- |
| job\_alias | string | The Jobs offered, as Yelp aliases, by the business. Case-sensitive. Jobs availability is dependent on a business' Categories. Always prefixed with job\_\*. |
| value | boolean | Whether this Job is enabled for this business. |
| job\_attributes | \[Job Attribute\] | Optional. Attributes are additional qualifiers on a Job. For example a Metal Working Job can be made more specific that the business can work with specific materials such as Steel. |

## 

Job Attribute

JavaScript

`[ { "value": {boolean}, "relation": {string}, "entities": [{string}] } ]`

| Property Name | Value | Refers to whether this Job Attribute is enabled. |
| --- | --- | --- |
| relation | string | An Attribute alias, always prefixed with rel\_\*. Case-sensitive. Relation availability is dependent on the Job. Example: rel\_works\_on\_item |
| entities | \[string\] | List of Attribute values that the business works with via the specified Relation. Case-sensitive. Must specify at least one value in the list. Entity availability depends on the combination of Job and Relation. Example: \[item\_toilet, item\_sump\_pump, item\_shower\] |

# 

API Reference

The following methods are available via the Data Ingestion API. URLs are relative to [https://partner-api.yelp.com/v1/ingest/](https://partner-api.yelp.com/v1/ingest/) unless otherwise noted.

| Method | HTTP Request | Description |
| --- | --- | --- |
| create | POST /create | Create a new ingestion job. |
| status | GET / status/ {job\_id} | Obtain the status of an existing ingestion job. |

## 

Create

Creates a new ingestion job for the provided resources.  
  
  
**Request**  
  
_HTTP Request_  

Create

`POST https://partner-api.yelp.com/v1/ingest/create`

_Parameters_  
  
Do not supply parameters with this method.  
  
  
_Request Body_  
  
In the request body, supply a Job resource with the following required properties:

| Property Name | Value | Description |
| --- | --- | --- |
| businesses\[\] | list | List of the businesses to create or update for this job. |

**Response**

If successful, this method returns a Job Response resource in the response body.  
  
  
**Example**  
  
_Request_

JavaScript

`{ 	"businesses": [ 		{ 			"matching_criteria": { 				"address1": "800 N Point St", 				"address2": null, 				"address3": null, 				"city": "San Francisco", 				"country": "US", 				"latitude": 37.8058024, 				"longitude": -122.420582, 				"name": "Gary Danko", 				"phone": "+14157492060", 				"postal_code": "94109", 				"state": "CA" 				"yelp_business_id": "WavvLdfdP6g8aZTtbBQHTw" 			}, 			"options": { 				"create_if_missing": false, 				"use_matching_criteria_for_update": false, 			}, 			"partner_business_id": "12345", 			"update": { 				"accepts_credit_cards": true, 				"alcohol": "full_bar", 				"categories": [ 					"newamerican" 				], 				"caters": false, 				"delivery": false, 				"has_tv": false, 				"hours": [ 					{ 						"day": "monday", 						"open": "17:30:00", 						"close": "22:00:00" 					}, { 						"day": "tuesday", 						"open": "17:30:00", 						"close": "22:00:00" 					}, { 						"day": "wednesday", 						"open": "17:30:00", 						"close": "22:00:00" 					}, { 						"day": "thursday", 						"open": "17:30:00", 						"close": "22:00:00" 					}, { 						"day": "friday", 						"open": "17:30:00", 						"close": "22:00:00" 					}, { 						"day": "saturday", 						"open": "17:30:00", 						"close": "22:00:00" 					}, { 						"day": "sunday", 						"open": "17:30:00", 						"close": "22:00:00" 					} 				], 				"is_customer": false, 				"is_owner_verified": true, 				"parking": { 					"garage": false, 					"lot": false, 					"street": false, 					"valet": true, 					"validated": false 				}, 				"platform_service": { 			"active": true, 					"ownership": "business", 					"partner_service_id": "12345-delivery", 					"areas": [ 						{ 							"type": "postal_code", 							"area": "94133", 							"service_charges": [ 								{ 									"type": "fixed", 									"minimum_subtotal": { 										"amount": "20.00", 										"currency_code": "USD" 									}, 									"charge": { 										"amount": "5.00", 										"currency_code": "USD" 									} 								}, { 									"type": "percentage", 									"description": "Service Charge (10%)", 									"maximum_subtotal": { 										"amount": "20.00", 										"currency_code": "USD" 									}, 									"charge": "10.00" 								} 							], 							"minimum_order": { 								"amount": "10.00", 								"currency_code": "USD" 							}, 							"estimated_arrival": { 								"minimum": 45, 								"maximum": 60 							} 						}, { 							"type": "radius", 							"area": "10.5", 							"service_charges": [ 								{ 									"type": "fixed", 									"charge": { 										"amount": "10.00", 										"currency_code": "USD" 									} 								} 							], 							"minimum_order": { 								"amount": "15.00", 								"currency_code": "USD" 							}, 							"estimated_arrival": { 								"minimum": 60, 								"maximum": 75 							} 						}, { 							"type": "polygon", 							"area": [ 								{ 									"latitude": 37.70796096626821, 									"longitude": -122.51380219886479 								}, { 									"latitude": 37.70796096626821, 									"longitude": -122.3568857615554 								} 							], 							"minimum_order": { 								"amount": "20.00", 								"currency_code": "USD" 							}, 							"estimated_arrival": { 								"minimum": 75, 								"maximum": 90 							} 						} 					], 					"service_types": [ 						{ 							"service_type": "delivery", 							"hours": [ 								{ 									"day": "monday", 									"start": "17:30:00", 									"end": "22:00:00" 								} 							], 							"exceptions": [ 								{ 									"date": "2013-07-04", 									"start": "18:00:00", 									"end": "21:00:00" 								} 							] 						} 					] 				}, 				"outdoor_seating": false, 				"take_out": false, 				"takes_reservations": true, 				"url": "http://www.garydanko.com/", 				"waiter_service": true, 				"wheelchair_accessible": true, 				"wifi": "no" 			} 		} 	] } Response If the request was successful: { 	"job_id": "c6HT44PKCaXqzN_BdgKPCw" } If the request was not successful: { 	"error": { 		"code": "INVALID_JSON", 		"message": "The submitted JSON is invalid", 	} }`

## 

Status

Obtain the status of a Data Ingestion job and its individual parts.

**Request**  

_HTTP Request_  

Status

`GET https://partner-api.yelp.com/v1/ingest/status/{job_id}`

| Property Name | Value | Description |
| --- | --- | --- |
| jod\_id | string | Identifier of the job as returned from the create call. Job\_ids are retained for 14 days on Yelp's end, after this the job won't be queryable. |
| detail\_level | integer | Parameter to check if business attributes have been applied |

_Request Body_  
  
Do not supply a request body with this method.  
**Response**  
If successful, this method returns a Job Status resource in the response body.  
  
  
**Example**  
_Request_

Status

`GET https://partner-api.yelp.com/v1/ingest/status/c6HT44PKCaXqzN_BdgKPCw`

_Response_

JavaScript

`{ 	"business_results": { 		"partner_business_id": "12345", 		"results": { 			"name": { 				"requested_value": "Gary Danko", "status": "COMPLETED", 			}, 			"photos": [ 				{ 					"error": { 						"code": "PHOTO_FAILED_TO_DOWNLOAD", 		"message": "The submitted photo failed to download" 					}, 					"requested_value": { 							"caption": "Entrance off North Point St", 							"url": "http://www.partner.com/photos/invalid.jpg", 					}, 	"status": "REJECTED", 				}, 				{ 					"caption": { 						"requested_value": "Ahi Tuna", 		"status": "COMPLETED" 					}, 					"url": { 						"requested_value": "http://www.partner.com/photos/1.jpg", 		"status": "COMPLETED" 					} 				}, 				{ 					"caption": { 						"error": { 							"code": "TEXT_TOO_LONG", 			"message": "Inputted text exceeds maximum length." 						}, 						"requested_value": "Some really long text...", 		"status": "REJECTED" 					}, 					"url": { 						"requested_value": "http://www.partner.com/photos/2.jpg", 		"status": "COMPLETED" 					} 				} 			], 			"url": { 				"requested_value": "http://www.garydanko.com", "status": "PROCESSING", 			}, 		}, 		"status": "PROCESSING", 		"yelp_business_id": "WavvLdfdP6g8aZTtbBQHTw", 	} }`

For attributes where Yelp has granted you Publish-Then-Review fast-tracking, you can set the 'detail\_level' parameter to 2 which will reflect the job status state for when updated attributes are live on Yelp's site.

**Example**  
_Request_

Status

`GET https://partner-api.yelp.com/v1/ingest/status/c6HT44PKCaXqzN_BdgUYv7?detail_level=2`

_Response_

JavaScript

`{ 	"status": "APPLIED", 	"completed_at": null, 	"created_at": "2018-09-18T23:15:04+00:00", 	"business_results": [ 		{ 			"status": "APPLIED", 			"yelp_business_id": "4ojWppqh0YFoU9NQ7532PQ", 			"update_results": { 				"accepts_credit_cards": { 					"status": "APPLIED", 					"requested_value": "true" 				}, 				"name": { 					"status": "COMPLETED", 					"requested_value": "Musikal" 				}, 				"city": { 					"status": "COMPLETED", 					"requested_value": "Gunnison" 				}, 				"address1": { 					"status": "COMPLETED", 					"requested_value": "600 E Tomichi Ave" 				}, 				"address2": { 					"status": "COMPLETED", 					"requested_value": "Ste 200" 				}, 				"wifi": { 					"status": "COMPLETED", 					"requested_value": "true", 					"error": { 						"message": "This value can not be set on this attribute.", 						"code": "VALUE_NOT_AVAILABLE_FOR_ATTRIBUTE" 					} 				}, 				"phone": { 					"status": "COMPLETED", 					"requested_value": "+19255058800" 				}, 				"state": { 					"status": "COMPLETED", 					"requested_value": "CO" 				}, 				"postal_code": { 					"status": "COMPLETED", 					"requested_value": "81230" 				}, 				"country": { 					"status": "COMPLETED", 					"requested_value": "US" 				}, 				"categories": [ 					{ 						"status": "APPLIED", 						"requested_value": "musicians" 					} 				] 			}, 			"partner_business_id": null 		} 	] }`

If a new business creation is rejected, the business receipt will show a business-level rejection, rather than listing the status of each individual attribute:

JavaScript

`{ 	"status": "COMPLETED", 	"completed_at": "2015-03-10T04:33:58+00:00", 	"created_at": "2015-03-10T04:28:37+00:00", 	"business_results": [ 		{ 			"status": "REJECTED", 			"yelp_business_id": "V-OGEpNaFIPb19H8l_9K8w", 			"partner_business_id": "a51d0f6b1f0a22a1066c", 			"error": { 				"message": "The created business was removed by our User Ops team.", 				"code": "BUSINESS_CREATE_REJECTED" 			} 		} 	] }`

## 

Delete Photos

**Steps:**

1.  Submit photos using Data Ingestion API
2.  Yelp returns unique photo IDs for each photo in the Data Ingestion API status.
3.  Save the photo IDs on your system.
4.  When you want to delete photo(s), send a Data Ingestion API call with the ID(s) of the photos you want to delete.
5.  You'll only be able to delete photos that you added.

**Example 1:** Data Ingestion job response with photo IDs.

The job response will contain **"photo\_id"** in the update\_results.photos object which contain the photo ID of the uploaded photo:

"photo\_id": "41y7HRzJFnnFEDWEMcIdzw"

"photo\_id": "Cd6bYfOenrCmfRTO1lKBxg"

JavaScript

`{ "status": "COMPLETED", "yelp_business_id": "H0bZzWNMSl8IbeMkr6ABYw", "update_results": { "photos": [ { "url": { "status": "COMPLETED", "requested_value": "http://s3-media1.fl.yelpcdn.com/bphoto/qIR9wKIPZkAlZFHLdC18pw/o.jpg" }, "caption": { "status": "COMPLETED", "requested_value": "Mug of Beer" }, "photo_id": { "status": "COMPLETED", "photo_id": "41y7HRzJFnnFEDWEMcIdzw" } }, { "url": { "status": "COMPLETED", "requested_value": "http://s3-media2.fl.yelpcdn.com/bphoto/Q5cg9EgsBu2zZCZYznSinA/o.jpg" }, "caption": { "status": "COMPLETED", "requested_value": "Loaded Nachos" }, "photo_id": { "status": "COMPLETED", "photo_id": "Cd6bYfOenrCmfRTO1lKBxg" } } ] }, "partner_business_id": null }`

**Example 2:** Data Ingestion job request to delete a photo.

Pass in a **"delete\_photos"** object with a comma-delimited list of photo ids:

JavaScript

`{ "businesses": [ { "matching_criteria": { "yelp_business_id": "vsI-zHdG7cFQzpGsyxpQnA" }, "update": { "delete_photos": [ "41y7HRzJFnnFEDWEMcIdzw", "Cd6bYfOenrCmfRTO1lKBxg" ] } } ] }`

**Important to Note:** Business Details API endpoint currently does not return photo IDs. All unique photo IDs are returned for each photo in the Data Ingestion API status.

You're only able to delete photos that you added. To enable Delete Photo access, please email [partner-support@yelp.com](mailto:partner-support@yelp.com)  
  

## 

Create Business

##### 

HTTP Request

Request

`POST https://partner-api.yelp.com/v1/ingest/create`

### 

Example

This example below shows how you can create a new business called "BoJack's Restaurant".

The Yelp User Operations team will need to approve the new business listing once created (1-2 days).

#### 

Request Body

JavaScript

`{ 	"businesses": [{ 		"matching_criteria": { 			"name": "BoJack's Restaurant", 			"address1": "15 Hollywoo St", 			"city": "Los Angeles", 			"state": "CA", 			"country": "US", 			"phone": "+13640222312", 			"latitude": 1.924122456, 			"longitude": 49.12122299 		}, 		"options": { 			"use_matching_criteria_for_update": "true", 			"create_if_missing": "true" 		}, 		"update": { 			"categories": ["pizza"] 		} 	}] }`

#### 

Response

JavaScript

`{ "status": "PROCESSING", "yelp_business_id": "9RKJAGex9lXjUReMcDETpg", "update_results": { "categories": [ { "status": "APPLIED", "requested_value": "pizza" } ] }, "partner_business_id": null }`

# 

Appendix A: Country & State Codes

## 

Overview

The Data Ingestion API uses ISO 3166-1 alpha2 country codes for the "country" field, and ISO 3166-2 subdivision codes (without country code) for the "state" field. This appendix clarifies edge cases and exceptions.

## 

Country

No exceptions of note.

## 

State (Country Subdivisions)

In several countries, there are several levels of subdivision; the Data Ingestion API may support some but not all of them.

### 

Subdivisions in countries with multiple layers

In countries with multiple layers of subdivisions with ISO 3166-2 codes, we may support some but not all.

| Country Code | Country Name | Description |
| --- | --- | --- |
| CZ | Czech Republic | [Regions](http://en.wikipedia.org/wiki/ISO_3166-2:CZ#Regions) are supported. 
[Districts](http://en.wikipedia.org/wiki/ISO_3166-2:CZ#Districts) are not supported. |
| ES | Spain | [Provinces](http://en.wikipedia.org/wiki/ISO_3166-2:ES#Provinces) and [autonomous cities](http://en.wikipedia.org/wiki/ISO_3166-2:ES#Autonomous_communities.3B_autonomous_cities_in_North_Africa) are supported. 
[Autonomous communities](http://en.wikipedia.org/wiki/ISO_3166-2:ES#Autonomous_communities.3B_autonomous_cities_in_North_Africa) are not supported. |
| FR | France | [Metropolitan departments](http://en.wikipedia.org/wiki/ISO_3166-2:FR#Metropolitan_departments) are supported. 
[Metropolitan Regions, Overseas Departments](http://en.wikipedia.org/wiki/ISO_3166-2:FR#Overseas_departments), and [Dependency and overseas territorial collectivities](https://docs.developer.yelp.com/ http://en.wikipedia.org/wiki/ISO_3166-2:FR#Dependency_and_overseas_territorial_collectivities) are not supported. |
| GB | United Kingdom | [Two-tier counties](http://en.wikipedia.org/wiki/ISO_3166-2:GB#List_of_subdivisions) are supported. 
[Unitary authorities](http://en.wikipedia.org/wiki/ISO_3166-2:GB#List_of_subdivisions) are supported. 
 
One custom state "XGL" (Greater London) covers the City of London and the 32 London boroughs. 
 
[Metropolitan counties](https://en.wikipedia.org/wiki/Metropolitan_county) are supported, with the following custom codes: 
 
XGM Greater Manchester 
XMS Merseyside 
XSY South Yorkshire 
XTW Tyne and Wear 
XWM West Midlands 
XWY West Yorkshire 
 
[London Boroughs](http://en.wikipedia.org/wiki/ISO_3166-2:GB#List_of_subdivisions) are not supported. 
[Metropolitan Districts](http://en.wikipedia.org/wiki/ISO_3166-2:GB#List_of_subdivisions) are not supported. 
[Countries](http://en.wikipedia.org/wiki/ISO_3166-2:GB#Three_countries_and_one_province) are not supported. |
| IE | Ireland | [Counties](http://en.wikipedia.org/wiki/ISO_3166-2:IE#Counties) are supported. 
[Provinces](http://en.wikipedia.org/wiki/ISO_3166-2:IE#Provinces) are not supported. |
| IT | Italy | [Provinces](http://en.wikipedia.org/wiki/ISO_3166-2:IT#Provinces) are supported. 
[Regions](http://en.wikipedia.org/wiki/ISO_3166-2:IT#Regions) are not supported. |
| NL | Netherlands | [Provinces](http://en.wikipedia.org/wiki/ISO_3166-2:NL#Provinces) are supported. 
[Countries and Special Municipalities](http://en.wikipedia.org/wiki/ISO_3166-2:NL#Countries_and_special_municipalities) are not supported. |
| PH | Philippines | [Provinces](https://en.wikipedia.org/wiki/ISO_3166-2:PH#Provinces) are supported. 
One custom province "NCR" covers Metro Manila. 
 
[Regions](https://en.wikipedia.org/wiki/ISO_3166-2:PH#Regions) are not supported. |
| SG | Singapore | One custom state "SG" is supported. 
[Districts](http://en.wikipedia.org/wiki/ISO_3166-2:SG#Current_codes) are not supported. |
| TW | Taiwan | [Districts](http://en.wikipedia.org/wiki/ISO_3166-2:TW#Current_codes) are supported, with the exception of: 
KHQ (see KHH) 
TXQ (see TXG) 
TNQ (see TNN) 
Note that TPQ refers to New Taipei City. 
 
[Municipalities](http://en.wikipedia.org/wiki/ISO_3166-2:TW#Current_codes) are supported. 
All currently assigned [special municipalities](http://en.wikipedia.org/wiki/ISO_3166-2:TW#Current_codes) are supported. 
 
Two custom codes cover additional counties: 
LCH Lienchiang County (incl. Lienchiang and Matsu Islands) 
KNM Kinmen County (incl. Kinmen and Quemoy) |

# 

Subdivisions included in ISO 3166-1

Some country subdivisions also have a dedicated ISO 3166-1 country code. In this case, the same code is used as both the country and state code.

## 

United States Outlying Areas

| Country Code | Country Name | State Code |
| --- | --- | --- |
| AS | American Samoa | AS |
| GU | Guam | GU |
| MP | Northern Mariana Islands | MP |
| PR | Puerto Rico | PR |
| UM | United States Minor Outlying Islands | UM |
| VI | US Virgin Islands | VI |

## 

United Kingdom Crown Dependencies

| Country Code | Country Name | State Code |
| --- | --- | --- |
| GG | Guernsey | GG |
| IM | Isle of Man | IM |
| JE | Jersey | JE |

# 

Appendix B: Error Code Reference

The following is a list of error codes that can be returned from the Data Ingestion API.

## 

Input Errors

Input errors indicate that something was wrong with the format or content of the request made to Data Ingestion. The request should be updated to fix the error and may then be resubmitted.

| Error Code | Error Message |
| --- | --- |
| ATTRIBUTES\_CONFLICT | The attributes {first\_attribute} and {second\_attribute} cannot both be set. |
| ATTRIBUTE\_ALREADY\_HAS\_VALUE | The value that was submitted for this attribute already exists on the business. (This means that your category updates did not get accepted because the categories already exist on Yelp) |
| ATTRIBUTE\_ALREADY\_IN\_QUEUE | The value that was submitted for this attribute is already in Yelp's User Ops queue. |
| ATTRIBUTE\_AUTHORIZATION\_FAILED | You are not authorized to update this attribute. |
| ATTRIBUTE\_CANNOT\_BE\_UPDATED\_ ON\_AN\_EXISTING\_PHOTO\_ERROR | This attribute cannot be updated on preexisting photos. |
| ATTRIBUTE\_LOCKED | The value that was submitted wasn't used because the attribute is locked.1 |
| ATTRIBUTE\_REMOVED\_FROM\_QUEUE | This attribute has been replaced in the queue by a more recent attribute change. |
| BUSINESS\_AUTHORIZATION\_FAILED | You are not authorized to change this business: {message}.2 Typically authorization is handled by a country whitelist (you'd encounter this error if updating a not whitelisted country) OR authorization is handled by the location subscription api, in this case you'd encounter this error if you haven't subscribed to the business before trying to update it. If you have questions about your authorization, reach out to partner-support@yelp.com |
| BUSINESS\_CREATE\_REJECTED | The created business was removed by our User Ops team. |
| BUSINESS\_DOES\_NOT\_HAVE\_ PRIMARY\_VIDEO | Business {business\_id} does not have an active advertiser video. |
| BUSINESS\_MATCH\_FAILED | Failed to find matching business.3 |
| BUSINESS\_NOT\_ACTIVE | This business cannot be accessed because it is {inactive\_type}. |
| BUSINESS\_NOT\_ELIGIBLE\_FOR\_ SERVICE\_AREA | Based on its categories, this business is not eligible for service areas. |
| CATEGORY\_ALIAS\_NOT\_RECOGNIZED | The provided category alias does not exist. |
| CATEGORY\_LIMIT\_EXCEEDED | The number of categories supplied exceeds the limit. |
| CTA\_BELONGS\_TO\_OTHER\_SOURCE | Cannot end a CTA that you do not own. |
| CTA\_UPDATE\_FAILED | Unable to update Call to Action buttons because this business does not have an active or future Branded Profile or Enhanced Profile program |
| DATA\_IS\_OBVIATED | Our User Ops team has determined that the submitted value is not as up to date as the value that we have in our records. |
| DISALLOWED\_CHARACTER | The disallowed character {disallowed\_character} was found at position {position} of the input string. |
| EMAIL\_IN\_USE\_ERROR | Email already in use. |
| INVALID\_ALIAS | The business alias you provided for yelp\_business\_id is not currently associated with any Yelp businesses. |
| INVALID\_CATEGORY\_FOR\_PARTNER | The provided category is invalid for the partner's configuration. |
| INVALID\_FORMAT | The format of this value is not consistent with what is expected. |
| INVALID\_HOURS | The submitted hours are invalid. |
| INVALID\_IMAGE\_DATA | The data at the provided url was not in a recognized image format. |
| INCOMPATIBLE\_JOB\_ATTRIBUTE\_VALUES | ValidationError: Job cannot be false if Attribute is true {job\_and\_attribute\_aliases}. |
| INVALID\_JOB\_ATTRIBUTE\_RELATIONSHIP | ValidationError: Job+Relation+Entity:{job\_relation\_entity\_aliases} are invalid together. |
| INVALID\_JSON | The submitted JSON is invalid. {reason}. |
| INVALID\_LIST\_INDEXES | The list expected all items to validate. However, it contains errors at the following indexes: ({indexes\_with\_errors}). |
| INVALID\_MONEY\_STRING | The amount provided is not a valid representation of money. |
| INVALID\_OR\_MISSING\_REQUIRED\_ KEY | Invalid or missing required key(s): {required\_keys}. |
| INVALID\_SERVICE\_AREA | The service area provided is not valid. |
| INVALID\_POLYGON\_INTERSECTING\_ EDGES | The polygon provided is not valid. Its edges are intersecting. |
| INVALID\_POLYGON\_INSUFFICIENT\_ POINTS | The polygon provided is not valid. It must be defined by at least three points. |
| INVALID\_POLYGON\_VOID | The polygon provided is not valid. Coordinates not provided. |
| INVALID\_SERVICE\_CHARGE | The service charge provided is not valid. |
| INVALID\_VALUE | The value is not consistent with what is expected. |
| INVALID\_YELP\_BUSINESS\_ID | The yelp business id is invalid. |
| JOB\_AUTHORIZATION\_FAILED | You are not authorized to retrieve this job. |
| JOB\_ID\_NOT\_RECOGNIZED | The provided job id was not found in our records. |
| MATCHING\_CRITERIA\_NOT\_A\_DICT | Matching criteria is expected to be a dictionary, but the value received was not a dictionary. |
| MATCHING\_CRITERIA\_NOT\_FOUND | Matching criteria is required. |
| MINIMUM\_GREATER\_THAN\_MAXIMUM\_ ARRIVAL\_TIME\_ERROR | The provided minimum arrival time ({minimum}) was greater than provided maximum arrival time ({maximum}). |
| MISSING\_ALL\_OPTIONAL\_KEYS | One key from this set of keys: ({optional\_set\_of\_keys}) must contain a valid value. However, none was given. |
| MISSING\_GEOGRAPHIC\_COORDINATES | Both latitude and longitude must be present and valid for manual geocoding. |
| MULTIPLE\_PHOTO\_TYPES | A photo cannot be a business owner photo and a user photo at the same time. |
| PARENT\_WAS\_FAILED | This item's parent was failed, and as a result this item was also failed. |
| PARENT\_WAS\_REJECTED | This item's parent was rejected, and as a result this item was also rejected. |
| PHOTO\_FAILED\_TO\_DOWNLOAD | The submitted photo failed to download. |
| PHOTO\_TYPE\_AUTHORIZATION\_FAILED | You are not authorized to add photos of this type. |
| REJECTED\_BY\_USER\_OPS | The value that was provided was rejected by the user ops team. |
| SERVICE\_AREA\_NOT\_FOUND | Unable to find the given location: {location}. |
| SERVICE\_AREA\_TOO\_WIDE | The service area is too wide as the submitted locations are more than {max\_distance} miles apart. The problematic locations were {location1} and {location2}. |
| TEXT\_TOO\_LONG | Inputted text exceeds maximum length. |
| TOO\_MANY\_CAPITAL\_LETTERS | Inputted text has too many capital letters. |
| TOO\_MANY\_CONSECUTIVE\_CAPITAL\_LETTERS | Inputted text has too many consecutive capital letters. |
| TOO\_MANY\_PARTNER\_BUSINESS\_ERROR | The number of businesses in the request exceeded the maximum of 200. |
| TOO\_MANY\_SERVICE\_AREAS | The number of service area locations in the request exceeded the maximum number of allowed service areas for a business. |
| TOO\_MANY\_SPECIAL\_CHARACTERS | Inputted text has too many special characters. |
| TYPE\_NOT\_ACCEPTED | Unknown item type: {type\_received}. |
| UNCATEGORIZED\_BUSINESS\_UPDATE\_NEEDS\_CATEGORIES | This business is uncategorized and requires a category update in order to update any other attribute. |
| UNKNOWN\_ATTRIBUTE | The specified attribute is not recognized by our system. |
| UNKNOWN\_OPTIONS | The specified keys are not recognized by our system: {keys}. |
| USER\_ID\_IS\_NOT\_VALID | The specified user id is not valid. |
| VALIDATION\_FAILED | {original\_message}4 |
| VALUE\_AUTHORIZATION\_FAILED | You are not authorized to update this attribute with the given value. |
| VALUE\_NOT\_AVAILABLE\_FOR\_ATTRIBUTE | This value can not be set on this attribute. |
| VALUE\_NOT\_AVAILABLE\_FOR\_COUNTRY | This value can not be set on businesses from this country. |
| VALUE\_NOT\_A\_DICT | The given value was not a dictionary, but a dictionary was expected. |
| VALUE\_NOT\_A\_LIST | The given value was not a list, but a list was expected. |
| VALUE\_NOT\_NULLABLE | Null was set as the value for this attribute, but this value is not nullable. |
| YELP\_BUSINESS\_ID\_MISMATCH | The business id you passed ({partner\_yelp\_business\_id}) did not match what we found ({matched\_yelp\_business\_id}). |
| ZERO\_GEOGRAPHIC\_COORDINATES | The given latitude and longitude values were zero. Please provide valid values. |

1\. Attributes typically become locked if a) the business is advertising on Yelp and doesn’t want any changes to their information (like phone number, URL, or metered phone) during the program or b) if the business owner made a recent change themselves. If a business owner recently changed service\_area in their Yelp Business Owner login, that would cause service\_area to be locked via API. If you believe this field should be unlocked please escalate to [partner-support@yelp.com](mailto:partner-support@yelp.com) and include why this field should be unlocked. 
 
2\. If provided, the message field will contain the authorization criteria that failed for the request. 
 
3\. This error occurs when the "matching\_criteria" submitted for the business does not match Yelp’s internal data. Please verify that the submitted "matching\_criteria" matches the data for the business as it appears on [http://www.yelp.com.](http://www.yelp.com.) Common attributes that cause this error are incorrect "yelp\_business\_id", "latitude", "longitude", and "phone" - these can usually be omitted from "matching\_criteria". Unusual formats of "address1", "address2", or "address3" can also cause a business match failure. 
 
4\. The original\_message field will contain a description of why validation failed for the submitted request.

## 

Internal Errors

Internal errors indicate a problem occurred within the Data Ingestion system. You may retry your request at a later time. If the problem persists, please report the issue to Yelp.

| Error Code | Error Message |
| --- | --- |
| BUSINESS\_MATCH\_INTERNAL\_ERROR | An internal error occurred while matching the business. |
| BUSINESS\_MEDIA\_INTERNAL\_ERROR | An internal error occurred while processing an update to business media. |
| INTERNAL\_ERROR | An error has occurred while processing your change. |

# 

Appendix C: Service Area Eligibility

## 

Service Area

See a full list of [Service Area Eligible Categories.](https://docs.google.com/spreadsheets/d/195cq0XAAgozbwX71qHbMLYM0rah6THh4w-H9sXjmklM/edit?usp=sharing)

> ## 📘
> 
> Check out our Data Ingestion API Reference Page
> 
> ![:owlbert:](https://docs.developer.yelp.com/public/img/emojis/owlbert.png) [Data Ingestion Endpoints](https://docs.developer.yelp.com/reference#business-update)

Updated 25 days ago

---

Did this page help you?

Yes

No

Copy Page