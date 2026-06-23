# Source: https://docs.developer.yelp.com/reference/create_business_update_v1

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

Example JSON Payload

`{   "businesses": [     {       "matching_criteria": {         "address1": "800 N Point St",         "address2": null,         "address3": null,         "city": "San Francisco",         "country": "US",         "latitude": 37.8058024,         "longitude": -122.420582,         "name": "Gary Danko",         "phone": "+14157492060",         "postal_code": "94109",         "state": "CA",         "yelp_business_id": "WavvLdjbuy6g8aZTtbBQHTw"       },       "options": {         "create_if_missing": false,         "use_matching_criteria_for_update": false       },       "partner_business_id": "12345",       "update": {         "accepts_credit_cards": true,         "alcohol": "full_bar",         "categories": [           "newamerican"         ],         "caters": false,         "delivery": false,         "has_tv": false,         "is_customer": false,         "is_owner_verified": true,         "parking": {           "garage": false,           "lot": false,           "street": false,           "valet": true,           "validated": false         },         "wifi": "no"       }     }   ] }`

> ## 📘
> 
> Updatable Business Attributes
> 
> Please reference the table below for supported 'Business' attributes. To see other Data Ingestion supported resources please check out our [Data Ingestion Guide](https://docs.developer.yelp.com/docs/data-ingestion-api#di_api_resource_types)

| Property Name | Value | Required | Description |
| --- | --- | --- | --- |
| matching\_criteria | object | Yes | Provides information to find a matching business on Yelp. |
| matching\_criteria.address1 | string | No | The first line of the business’s address. Maximum length is 64; only digits, letters, spaces, and \_-’/#&,.': are allowed. |
| matching\_criteria.address2 | string | No | The second line of the business’s address. Maximum length is 64; only digits, letters, spaces, and \_-’/#&,.': are allowed. |
| matching\_criteria.address3 | string | No | The third line of the business’s address. Maximum length is 64; only digits, letters, spaces, and \_-’/#&,.': are allowed. |
| matching\_criteria.city | string | Yes | The city of the business. Maximum length is 64; only digits, letters, spaces, and \_-’.() are allowed. |
| matching\_criteria.country | string | Yes | The ISO 3166-1 alpha-2 country code of the business. Maximum length is 2. |
| matching\_criteria.latitude | double | No | The WGS84 latitude of the business in decimal degrees. Must be between -90 and 90. |
| matching\_criteria.longitude | double | No | The WGS84 longitude of the business in decimal degrees. Must be between -180 and 180. |
| matching\_criteria.name | string | Yes | The name of the business. Maximum length is 64; only digits, letters, spaces, and \_!#$%&+,-.’/:?@' are allowed. |
| matching\_criteria.phone | string | No | The phone number of the business, either (a) locally-formatted with digits only (e.g., 016703080) or (b) internationally-formatted with a leading + sign and digits only after (+35316703080). Maximum length is 32. |
| matching\_criteria.postal\_code | string | Yes | The postal code of the business. Maximum length is 12. |
| matching\_criteria.state | string | Yes | The ISO 3166-2 code for the region/province of the business. Maximum length is 3. |
| matching\_criteria.yelp\_business\_id | string | No (Required in phase 1 only) | Unique Yelp identifier of the business if available. Used as a hint when finding a matching business. |
| options | object | | Options for handling the business. |
| options.create\_if\_missing | boolean | | Whether to create the business if no matching business is found. Defaults to true if not specified. |
| options.use\_matching\_criteria\_for\_update | boolean | | Whether to use the information in the matching criteria to also update the business. When true, the fields from the matching\_criteria are merged into the update object. Any fields already present in the update object take precedence. Defaults to false if not specified. |
| partner\_business\_id | string | | Optional unique partner identifier for the business. Must not contain leading or trailing spaces. When provided, partner identifiers cannot change and must remain unique. Maximum length is 100. |
| update | object | | Provides rich content for the business. |
| update.about\_this\_business\_history | string | | The history of the business. Minimum length is 15, maximum is 1,000; URLs, all caps, and HTML tags are not allowed. |
| update.about\_this\_business\_specialties | string | | The specialties of the business. Minimum length is 15, maximum is 1,000; URLs, all caps, and HTML tags are not allowed. Business description will map to this attribute. |
| update.about\_this\_business\_year\_established | string | | The 4-digit year that the business was established. Year must be no greater than the year following today’s date (e.g., 2015 on 5/1/2014). |
| update.accepts\_credit\_cards | boolean | | Whether the business accepts credit cards for payments. |
| update.address1 | string | | The first line of the business’s address. Maximum length is 64; only digits, letters, spaces, and \_-’/#&,.: are allowed. |
| update.address2 | string | | The second line of the business’s address. Maximum length is 64; only digits, letters, spaces, and \_-’/#&,.: are allowed. |
| update.address3 | string | | The third line of the business’s address. Maximum length is 64; only digits, letters, spaces, and \_-’/#&,.: are allowed. |
| update.alcohol | string | | Whether the business serves alcohol. Possible values are: 
 
"none" - No alcohol is served. 
"beer\_and\_wine" – Only beer & wine are available. 
"full\_bar" – Beer, wine & spirits are available. |
| update.by\_appointment\_only | boolean | | Whether the business views patrons by appointment only. |
| update.categories\[\] | list | | The categories, as Yelp aliases, for the business. Case-sensitive. Maximum of 3 leaf categories. 
 
Yelp aliases can be found at the Category List Page or using the Categories API endpoint. |
| update.caters | boolean | | Whether the business offers catering. |
| update.city | string | | The city of the business. Maximum length is 64; only digits, letters, spaces, and -’.() are allowed. |
| update.closed | boolean | | Whether the business is permanently closed. |
| update.coat\_check | boolean | | Whether the business offers a coat check. |
| update.comment | string | | Optional comment, preferably from the end user, for this update. Maximum length is 4,500; all caps and HTML tags are not allowed. |
| update.country | string | | The ISO 3166-1 alpha-2 country code of the business. Maximum length is 2. |
| update.delivery | boolean | | Whether the business offers delivery. |
| update.desktop\_cta | nested object | | Create, update, or end a desktop call to action offer using a Call to Action – Desktop resource. |
| update.display\_url | string | | The URL to display on the page. This field can only be set when "url" is also set. "display_url" and "url" cannot have the same value. Maximum length is 255; only digits, ASCII letters, and !"#$%&'()\*+,-./:;<=>?@\[\]^_\`{|}~ are allowed. Must start with http:// or https://. Links to Facebook, Twitter, Google Plus, or other directories are not allowed in most cases. |
| update.dogs\_allowed | boolean |  | Whether dogs are allowed at the business. |
| update.group\_bookings | boolean |  | Whether business offers group bookings. |
| update.happy\_hour | boolean |  | Whether the business has a happy hour. |
| update.has\_tv | boolean |  | Whether the business has televisions. |
| update.hours\[\] | list |  | The operating hours of the business. Multiple entries can exist for the same day (e.g., a business is open for lunch and dinner but closes in between). To set a business open 24 hours, set both the "open" and "close" fields to 00:00. To set a business to be closed for a specific day of the week, don't include that day in the list. |
| update.hours\[\].day | string |  | The full day of the week, in English, for the hours. Possible values are:  
  
"monday"  
"tuesday"  
"wednesday"  
"thursday"  
"friday"  
"saturday"  
"sunday" |
| update.hours\[\].open | time |  | The time the business opens on the specified day. |
| update.hours\[\].close | time |  | The time the business closes on the specified day. The close time can be earlier than the open time if the business closes the following day (e.g., opens at 7 PM and closes at 2 AM). |
| update.is\_customer | boolean |  | Whether the business is a paying client. This is used to indicate the relationship a partner has with the business. false is assumed unless provided. |
| update.is\_owner\_verified | boolean |  | Whether the owner of the business has verified its information. false is assumed unless provided. |
| update.latitude | double |  | The WGS84 latitude of the business in decimal degrees. Must be between -90 and 90. |
| update.longitude | double |  | The WGS84 longitude of the business in decimal degrees. Must be between -180 and 180. |
| update.menu\_data | nested object |  | Menu data, as a Menu Data resource, for the business. |
| update.menu\_url | string |  | The business’s menu URL. Maximum length is 2,000; only digits, ASCII letters, and !"#$%&'()\*+,-./:;<=>?@\[\]^\_\`{|}~ are allowed. Must start with http:// or https://. Links to Facebook, Twitter, Google Plus, or other directories are not allowed in most cases. |
| update.mobile\_cta | nested object | | Create, update, or end a mobile call to action offer using a Call to Action – Mobile resource. |
| update.name | string | | The name of the business. Maximum length is 64; only digits, letters, spaces, and \_!#$%&+,-./:?@' are allowed. |
| update.parking | object | | The types of parking available for the business. |
| update.parking.garage | boolean | | Whether a garage or deck is available. |
| update.parking.lot | boolean | | Whether a lot is available. |
| update.parking.street | boolean | | Whether street parking is available. |
| update.parking.valet | boolean | | Whether valet parking is available. |
| update.parking.validated | boolean | | Whether validated parking is available. |
| update.metered\_phone | string | | The call tracking number of the business, either (a) locally-formatted with digits only (e.g., 016703080) or (b) internationally-formatted with a leading + sign and digits only after (+35316703080). Maximum length is 32. If metered\_phone is sent, then the phone must also be sent. |
| update.phone | string | | The phone number of the business, either (a) locally-formatted with digits only (e.g., 016703080) or (b) internationally-formatted with a leading + sign and digits only after (+35316703080). Maximum length is 32. |
| update.photo\[\] | list | | Photos, as Business Photo resources, for the business. |
| update.platform\_service | nested object | | Platform service information, as a Platform Service resource, for the business. |
| update.postal\_code | string | | The postal code of the business. Maximum length is 12. |
| update.opening\_date | date | | The date the business opened. Must be in the past. |
| update.outdoor\_seating | boolean | | Whether the business offers outdoor seating. |
| update.service\_area\[\] | list | | The additional locations serviced by the business. Locations must be expressed as unambiguous postal codes or neighborhood- city-state-country combinations. Maximum of 6 locations; distance between locations cannot exceed 100 miles. |
| update.smoking | string | | Whether smoking is allowed at the business. Possible values are: 
 
"no" – Smoking is not allowed. 
"yes" – Smoking is allowed. 
"outdoor" – Smoking is only allowed outside. |
| update.state | string | | The ISO 3166-2 code for the region/province of the business. Maximum length is 3. |
| update.take\_out | boolean | | Whether the business offers take-out. |
| update.takes\_reservations | boolean | | Whether the business takes reservation. |
| update.url | string | | The business’s website URL. Maximum length is 255; only digits, ASCII letters, and !"#$%&'()\*+,-./:;<=>?@\[\]^\_\`{|}~ are allowed. Must start with http:// or https://. Links to Facebook, Twitter, Google Plus, or other directories are not allowed in most cases. |
| update.waiter\_service | boolean |  | Whether the business has waiter service. |
| update.wheelchair\_accessible | boolean |  | Whether the business is wheelchair-accessible. |
| update.wifi | string |  | Whether the business offers Wi-Fi. Possible values are:  
  
"no" – WiFi is not available.  
"paid" – Paid WiFi is available.  
"free" – Free WiFi is available. |
| update.linkout\_data | nested object |  | linkout information as a Linkout Data resource, for the business. |

> ## 📘
> 
> This endpoint is part of the Data Ingestion API, visit [Data Ingestion API](https://docs.developer.yelp.com/docs/data-ingestion-api) to learn more.

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

Updated over 1 year ago

---

ShellNodeRubyPHPPython

:

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400 - Result

Updated over 1 year ago

---