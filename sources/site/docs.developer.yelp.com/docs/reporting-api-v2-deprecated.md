# Source: https://docs.developer.yelp.com/docs/reporting-api-v2-deprecated

> ## 🚧
> 
> Reporting API v2 is deprecated - End of Support June 2023
> 
> Please migrate to [Reporting API V3](https://docs.developer.yelp.com/docs/reporting-v2-to-v3-migration-guide).

# 

Overview

The Reporting API provides a means for Yelp partners to retrieve business metrics and CPC advertiser metrics for a specified set of businesses over a specified time range. Access to the Reporting API is reserved for contracted Yelp partners or direct Yelp advertisers that meet certain spend levels. Feature eligibility is subject to spend level, please reach out to your Yelp representative to learn more.

When a request is made for a report, a corresponding report ID will be returned. The report ID can then be used to retrieve data for the requested set of metrics across the requested set of businesses. A report usually takes 30 minutes to process.

Yelp metrics are batch processed once every 24 hours. Each analytics run captures one day of data (starting and ending at midnight PST). [Business Metrics](https://docs.developer.yelp.com/#business-metrics) are usually complete by 1:00 PM PST the following day. [Advertiser Metrics](https://docs.developer.yelp.com/#advertiser-metrics) are usually complete by 10:00 AM PST the following day. Once metrics are available in Reporting API, they do not change.

The metrics available in the Reporting API are simply tracking the different types of actions a consumer can take on either the Yelp profile page or the advertising unit/copy. Reporting information like pixels, store visit attribution, or call tracking are not reflected today in the reporting API.

There may be more than a 24-hour lag between delivery and reporting (e.g. if an ad is delivered at 12:01AM on Monday and our analytics run completes at 10AM on Tuesday). The batch itself runs every day.

# 

Revision History

| Revision Number | Date | Editor | Summary |
| --- | --- | --- | --- |
| 1.0 | | | Initial Version. |
| 2.0 | October 11, 2017 | Cathy Chou | 1\. Added 'Revision History' section 
2\. Added Descriptions to Business Metrics 
3.Revised Business Metrics nomenclature: num\_total\_page\_views, num\_user\_photos, num\_desktop\_page\_views 
4.Minor style fixes |

# 

Authentication

The API uses basic authentication over HTTPS. Credentials are provided separately.

Note: Reporting API requires separate credentials from Data Ingestion or Ads API. Please request access from your Yelp account team and solutions engineer.

# 

Versioning

To maintain backwards-compatibility with partner-developed applications, the Yelp Reporting API is versioned with the version encoded in the URI. The current and latest version is v2 and all endpoints are located at `https://partner-api.yelp.com/analytics/v2/`.

# 

Format

Response bodies use the application/json content type and should be encoded in UTF-8.

# 

Identifiers

Yelp identifiers are unique within its own type; they are not globally unique. For example, a report and business may share the same identifier, _WavvLdfdP6g8aZTtbBQHTw_, but no other report or business will have that same identifier.

# 

Value Types

All datetime properties should use the [ISO 8601 format](http://en.wikipedia.org/wiki/ISO_8601) and be stored in UTC.

All time properties should use the format HH:MM\[:SS\] and be timezone-agnostic.

# 

Yelp Business IDs

The Reporting API requires encrypted business IDs to create reports. Please reference our [Business Match API documentation](https://www.yelp.com/developers/documentation/v3/business_match) on how to pull these values for Yelp listings. There is a maximum of 500 business ids per request.

# 

Metrics

Below are the metrics available for reporting through this API. Examples for querying our API with these metrics are presented in the [Endpoints](https://docs.developer.yelp.com/reference/create_daily_reports_v2) section.

## 

Business Metrics

| Business Metric | Display Name | Value | Description |
| --- | --- | --- | --- |
| num\_total\_page\_views | Total User Views | String | Number of total page views on desktop and mobile devices. |
| num\_calls | Mobile Calls | String | Number of phone calls initiated from the Yelp business profile. |
| num\_directions\_and\_map\_views | Directions & Map Views | String | Number of direction and map views from the Yelp business profile. |
| url\_clicks | Clicks to Website | String | Number of clicks to the business URL from the Yelp business profile. |
| num\_check\_ins | Mobile Check-ins | String | Number of mobile check-ins from the Yelp business profile. |
| num\_user\_photos | User Uploaded Photos | String | Number of user generated photos added to the Yelp business profile. |
| num\_bookmarks | Yelp Bookmarks | String | Number of times a business has been bookmarked by users. |
| num\_desktop\_cta\_clicks | Desktop Call to Action Clicks | String | Number of Call-to-Action clicks on desktop devices. |
| num\_mobile\_cta\_clicks | Mobile Call to Action Clicks | String | Number of Call-to-Action clicks on mobile devices. |
| num\_messages\_to\_business | Request a Quote - messages | String | Number of messages sent to a business, including messages sent through Request a Quote. |
| num\_mobile\_page\_views | Mobile User Views | String | Number of page views on mobile devices. |
| num\_desktop\_search\_appearances | Desktop Appearances in Search | String | Number of times a business appeared in search on desktop devices. |
| num\_mobile\_search\_appearances | Mobile Appearances in Search | String | Number of times a business appeared in search on mobile devices. |
| num\_desktop\_page\_views | Desktop User Views | String | Number of page views on desktop devices. |
| tracking\_calls | Calls Tracked | String | Number of calls tracked. |
| deals\_sold | Deals Sold | String | Number of deals sold. |
| online\_orders | Online Orders | String | Number of online orders. |
| online\_bookings | Online Bookings | String | Number of online bookings |

## 

Advertiser Metrics

| Advertiser Metric | Display Name | Value | Description |
| --- | --- | --- | --- |
| billed\_impressions | Billed Ad Impressions | String | Number of times Ad is displayed and will be billed. |
| billed\_clicks | Billed Ad Clicks | String | Number of clicks from a billed impression. |
| ad\_cost | Ad Cost | String | Cost of Ad when billed (in cents). |
| ad\_driven\_bookmarks | AD DRIVEN Yelp Bookmarks | String | Number of times a business has been bookmarked by users that can be attributed to an Ad impression. |
| ad\_driven\_calls | AD DRIVEN Mobile Calls | String | Number of phone calls initiated from the Yelp business profile that can be attributed to an Ad impression. |
| ad\_driven\_cta\_clicks | AD DRIVEN Total Call to Action Clicks | String | Number of Call-to-Action clicks on desktop devices that can be attributed to an Ad impression. |
| ad\_driven\_check\_ins | AD DRIVEN Mobile Check-ins | String | Number of mobile check-ins from the Yelp business profile that can be attributed to an Ad impression. |
| ad\_driven\_deals\_sold | AD DRIVEN Deals Sold | String | Number of deals sold that can be attributed to an Ad impression. |
| ad\_driven\_directions\_and\_map\_views | AD DRIVEN Directions & Map Views | String | Number of direction and map views from the Yelp business profile that can be attributed to an Ad impression. |
| ad\_driven\_messages\_to\_business | AD DRIVEN Request a Quote - messages | String | Number of messages sent to a business, including messages sent through Request a Quote that can be attributed to an Ad impression |
| ad\_driven\_user\_photos | AD DRIVEN User Uploaded Photos | String | Number of user generated photos added to the Yelp business profile that can be attributed to an Ad impression. |
| ad\_driven\_online\_reservations | AD DRIVEN Online Reservations | String | Number of Yelp Reservations and Yelp Nowait bookings through Yelp that can be attributed to an Ad impression. |
| ad\_driven\_url\_clicks | AD DRIVEN Clicks to Website | String | Number of clicks to the business URL from the Yelp business profile that can be attributed to an Ad impression. |

# 

Endpoints

## 

Overview

| HTTP Method | Resource | Description |
| --- | --- | --- |
| POST | businesses/daily\_reports | Request a report containing daily business/advertiser metrics for a specified list of businesses over a date range. Daily metrics can be requested up to 89 days ago. |
| POST | businesses/monthly\_reports | Request a report containing monthly business/advertiser metrics for a specified list of businesses over a specified month range. Monthly metrics can be requested up to 2 months ago. |
| GET | businesses/daily\_reports/{report\_id} | Fetch the daily report associated with {report\_id}. |
| GET | businesses/monthly\_reports/{report\_id} | Fetch the monthly report associated with {report\_id}. |

## 

Details

The detailed description of the endpoints has moved into the API Reference section. Please see there for detailed description, request and response schemas and request and response examples.

Click on any of the following Endpoints to view the API Reference section.

[![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Request Daily Report](https://docs.developer.yelp.com/reference/create_daily_reports_v2)

[![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Get Daily Report](https://docs.developer.yelp.com/reference/get_daily_reports_v2)

[![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Request Monthly Report](https://docs.developer.yelp.com/reference/create_monthly_reports_v2)

[![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Get Monthly Report](https://docs.developer.yelp.com/reference/get_monthly_reports_v2)

> ## 📘
> 
> Check out our Reporting API Reference Page
> 
> ![:owlbert:](https://docs.developer.yelp.com/public/img/emojis/owlbert.png) [Reporting API Endpoints](https://docs.developer.yelp.com/reference/create_daily_reports_v2)

Copy Page