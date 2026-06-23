# Source: https://docs.developer.yelp.com/docs/reporting-api

> ## 📘
> 
> This is a Yelp Partner API
> 
> Access is disabled by default. See [Yelp Partner APIs](https://docs.developer.yelp.com/docs/yelp-partner-apis) on how to get access.

> ## 👍
> 
> Migrating from v2?
> 
> Check out the [Migration Guide](https://docs.developer.yelp.com/docs/reporting-v2-to-v3-migration-guide)

# 

Overview

This API access is currently only available to Yelp [advertising](https://business.yelp.com/partners/), [listing management](https://business.yelp.com/partners/listing-management-partners/), & [knowledge](https://knowledge.yelp.com/) partners. Please inquire about becoming a partner on those pages if you'd like to access this API.

The Reporting API provides a means for Yelp partners to retrieve business metrics and CPC advertiser metrics for a specified set of businesses over a specified time range. Access to the Reporting API is reserved for contracted Yelp partners or direct Yelp advertisers that meet certain spend levels. Feature eligibility is subject to spend level, please reach out to your Yelp representative to learn more.

When a request is made for a report, a corresponding report ID will be returned. The report ID can then be used to retrieve data for the requested set of metrics across the requested set of businesses. A report usually takes 30 minutes to process.

Yelp metrics are batch processed once every 24 hours. Each analytics run captures one day of data (starting and ending at midnight PST). [Business Metrics](https://docs.developer.yelp.com/#business-metrics) are usually complete by 1:00 PM PST the following day. [Advertiser Metrics](https://docs.developer.yelp.com/#advertiser-metrics) are usually complete by 10:00 AM PST the following day. Once metrics are available in Reporting API, they do not change.

The metrics available in the Reporting API are simply tracking the different types of actions a consumer can take on either the Yelp profile page or the advertising unit/copy. Reporting information like pixels, store visit attribution, or call tracking are not reflected today in the reporting API.

There may be more than a 24-hour lag between delivery and reporting (e.g. if an ad is delivered at 12:01AM on Monday and our analytics run completes at 10AM on Tuesday). The batch itself runs every day.

# 

Video Overview

Check out a 3 minute video demo of the end to end flow [here](https://docs.google.com/videos/d/14vSlFQ9pSUq-E0_PpYByejLK7M0PNF1g5VLaoBrGluQ/edit?usp=sharing).

# 

Authentication

The API uses your Yelp Fusion Api Key for authentication. See [Fusion Authentication](https://docs.developer.yelp.com/docs/fusion-authentication) for details.

Your Yelp Fusion Client needs to be enabled for Reporting API. Please work with your Yelp rep to set up access.

Note: Reporting API requires separate set up from Data Ingestion or Ads API.

# 

Versioning

To maintain backwards-compatibility with partner-developed applications, the Yelp Reporting API is versioned with the version encoded in the URI. The current and latest version is v3 and all endpoints are located at `https://api.yelp.com/v3/reporting/`.

## 

Deprecation

| Version | Status | Description | Timeline |
| --- | --- | --- | --- |
| v1 | Deprecated | Superseded by v2 in October 2017 | End of Support: June - 2023 
Retirement: December 2023 |
| v2 | Deprecated | Superseded by v3 in December 2022 | End of new access: June - 2023 
Retirement: December 2024 |
| v3 | Current | | |

# 

Identifiers

Yelp identifiers are unique within its own type; they are not globally unique. For example, a report and business may share the same identifier, _WavvLdfdP6g8aZTtbBQHTw_, but no other report or business will have that same identifier.

# 

Value Types

All datetime properties should use the [ISO 8601 format](http://en.wikipedia.org/wiki/ISO_8601) and be stored in UTC.

All time properties should use the format HH:MM\[:SS\] and be timezone-agnostic.

# 

Yelp Business IDs

The Reporting API requires encrypted Business IDs to create reports. Please reference our [Business Match API documentation](https://docs.developer.yelp.com/reference/v3_business_match) on how to pull these values for Yelp listings. There is a maximum of 500 business ids per request.

# 

Metrics

Below are the metrics available for reporting through this API. Examples for querying our API with these metrics are presented in the [Endpoints](https://docs.developer.yelp.com/reference/create_daily_reports_v3) section.

## 

Business Metrics

Business Metrics count various kinds of interactions a user has with a business listing on Yelp. These counts are total metrics for the business\_id, inclusive of organic plus ad-driven.

| Business Metric | Display Name | Description |
| --- | --- | --- |
| num\_total\_page\_views | Total User Views | Number of total page views on desktop and mobile devices. |
| num\_calls | Mobile Calls | Number of phone calls initiated from the Yelp business profile. |
| num\_directions\_and\_map\_views | Directions & Map Views | Number of direction and map views from the Yelp business profile. |
| url\_clicks | Clicks to Website | Number of clicks to the business URL from the Yelp business profile. |
| num\_check\_ins | Mobile Check-ins | Number of mobile check-ins from the Yelp business profile. |
| num\_user\_photos | User Uploaded Photos | Number of user generated photos added to the Yelp business profile. |
| num\_bookmarks | Yelp Bookmarks | Number of times a business has been bookmarked by users. |
| num\_desktop\_cta\_clicks | Desktop Call to Action Clicks | Number of Call-to-Action clicks on desktop devices. |
| num\_mobile\_cta\_clicks | Mobile Call to Action Clicks | Number of Call-to-Action clicks on mobile devices. |
| num\_messages\_to\_business | Request a Quote - messages | Number of messages sent to a business, including messages sent through Request a Quote. |
| num\_desktop\_search\_appearances | Desktop Appearances in Search | Number of times a business listing appeared in search results on desktop devices. |
| num\_mobile\_search\_appearances | Mobile Appearances in Search | Number of times a business listing appeared in search results on mobile devices. |
| num\_desktop\_page\_views | Desktop User Views | Number of times the business page was accessed on desktop devices. |
| num\_mobile\_page\_views | Mobile User Views | Number of times the business page was accessed on mobile devices. |
| tracking\_calls | Calls Tracked | Number of calls tracked. |
| deals\_sold | Deals Sold | Number of deals sold. |
| online\_orders | Online Orders | Number of online orders. |
| online\_bookings | Online Bookings | Number of online bookings. |
| check\_in\_offer\_redemptions | Check In Offer Redemptions | The number of users that redeemed a check in offer for your listing (if applicable). |
| collection\_item\_added | Collections | The number of time your business was added to a collection other than the default bookmark collection. |
| rapc\_initiated | RaPC Initiated | Number of times RaPC (request a phone call) was initiated. |
| waitlist\_visit\_created | Waitlist Visit Created | Number of times someone got in line on the Yelp Waitlist. |
| median\_response\_time\_in\_sec | Median response time (secs) | The median time it took for your business to answer messages. |
| reply\_rate | Reply rate | The percentage of messages replied. |
| organic\_biz\_page\_views | Organic Page Visits | The amount of organic page views of your listing, which were not occurring as a consequence of ad clicks and ad impressions. |
| organic\_biz\_page\_views\_percentage | % Biz Page Views Organic | It measures which percentage of biz page views didn't derive from ads. |
| rating | Rating | Average Rating (1-5 star scale). |
| reviews | Reviews | The number of unfiltered reviews of your listing. |
| total\_leads | Total # of leads | Total # of leads (sums all Leads metrics). |

## 

Advertiser Metrics

Advertiser Metrics report cpc program related metrics. These include metrics like number of ad clicks or impressions but also various kinds of interactions a user has with a business listing which can be attributed to an ad impression. On Yelp they are identified as "ads" metrics. Campaign name, campaign id, and store code are not available in the reporting api.

| Advertiser Metric | Display Name | Description |
| --- | --- | --- |
| billed\_impressions | Billed Ad Impressions | Number of times an Ad is displayed and will be billed. |
| billed\_clicks | Billed Ad Clicks | Number of times a user clicked on an advertisement for the business and visited its business page. |
| ad\_cost | Ad Cost | Cost of Ad when billed (in cents). |
| ad\_driven\_bookmarks | Ad Driven Yelp Bookmarks | Number of times a business has been bookmarked by users that can be attributed to an Ad impression. |
| ad\_driven\_calls | Ad Driven Mobile Calls | Number of click to call call actions initiated from the Yelp business profile that can be attributed to an Ad impression. |
| ad\_driven\_cta\_clicks | Ad Driven Total Call to Action Clicks | Number of Call-to-Action clicks on desktop devices that can be attributed to an Ad impression. |
| ad\_driven\_check\_ins | Ad Driven Mobile Check-ins | Number of mobile check-ins from the Yelp business profile that can be attributed to an Ad impression. |
| ad\_driven\_deals\_sold | Ad Driven Deals Sold | Number of deals sold that can be attributed to an Ad impression. |
| ad\_driven\_directions\_and\_map\_views | Ad Driven Directions & Map Views | Number of direction and map views from the Yelp business profile that can be attributed to an Ad impression. |
| ad\_driven\_messages\_to\_business | Ad Driven Request a Quote - messages | Number of messages sent to a business, including messages sent through Request a Quote that can be attributed to an Ad impression |
| ad\_driven\_user\_photos | Ad Driven User Uploaded Photos | Number of user generated photos added to the Yelp business profile that can be attributed to an Ad impression. |
| ad\_driven\_online\_reservations | Ad Driven Online Reservations | Number of Yelp Reservations and Yelp Nowait bookings through Yelp that can be attributed to an Ad impression. |
| ad\_driven\_url\_clicks | Ad Driven Clicks to Website | Number of clicks to the business URL from the Yelp business profile that can be attributed to an Ad impression. |
| ad\_click\_through\_rate | Ad Click Through Rate | Ad CTR measures how well Yelp performs at getting users to click on your ads. |
| average\_cost\_per\_click | Average Cost Per Click | This metric measures, on average, the amount of cost per clicks that Yelp attributed to your Yelp business page for all clicks-based ad campaigns (if applicable). |
| billable\_ad\_clicks | Billable Ad Clicks | The number of times a user clicked on a search advertisement for your listing and came to its Yelp business page across all platforms. |
| billable\_ad\_impressions | Billable Ad Impressions | The number of times your listing was displayed in an advertisement. |
| ad\_driven\_biz\_page\_views | Ad Driven Page Visits | Ad Driven Yelp page visits is a measure of how many times your Yelp page was accessed or viewed on the Yelp website, mobile website, and mobile apps after seeing or clicking on an ad. This amount of pages visits is calculated using our 30 days attribution logic for ad clicks and 1 day for ad impressions. |
| ad\_driven\_calls\_tracked | Ad Driven Calls Tracked | The number of calls made by Yelp users after seeing or clicking on your ad which were successfully answered by your business, when you're using Yelp's Call Reporting feature. This metric doesn't include other call tracking numbers like Telemetrics etc. |
| ad\_driven\_rapc\_initiated | Ad Driven RaPC Initiated | Number of times RaPC was initiated. |
| ad\_driven\_waitlist\_visit\_created | Ad Driven Waitlist Visit Created | Number of times someone got in line on the Yelp Waitlist after seeing or clicking an ad. |
| ad\_driven\_total\_leads | Total # of ad driven leads | Total # of ad driven leads (sums all AdDrivenLeads metrics). |
| ad\_driven\_platform\_purchase\_made | Ad Driven Platform Purchases | Number of platform purchases that were to be fulfilled by third parties (GrubHub for food ordering, GoldStar for tickets etc.) and are attributed to an ad. |
| ad\_driven\_biz\_page\_views\_percentage | % Biz Page Views Ad Driven | It measures which percentage of biz page views derived from ads. |

# 

Endpoints

## 

Overview

| HTTP Method | Resource | Description |
| --- | --- | --- |
| POST | reporting/businesses/daily | Request a report containing daily business/advertiser metrics for a specified list of businesses over a date range. Daily metrics can be requested up to 89 days ago. |
| POST | reporting/businesses/monthly | Request a report containing monthly business/advertiser metrics for a specified list of businesses over a specified month range. Monthly metrics can be requested up to 2 months ago. |
| GET | reporting/businesses/daily/{report\_id} | Fetch the daily report associated with {report\_id}. |
| GET | reporting/businesses/monthly/{report\_id} | Fetch the monthly report associated with {report\_id}. |

## 

Details

The detailed description of the endpoints has moved into the API Reference section. Please see there for detailed description, request and response schemas and examples.

Click on any of the following Endpoints to view the API Reference section.

[![Request Daily Report](https://files.readme.io/08035d8-small-yelp-dev-portal.png)\\ \\ ![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Request Daily Report](https://docs.developer.yelp.com/reference/create_daily_reports_v3)

[![Get Daily Report](https://files.readme.io/08035d8-small-yelp-dev-portal.png)\\ \\ ![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Get Daily Report](https://docs.developer.yelp.com/reference/get_daily_reports_v3)

[![Request Monthly Report](https://files.readme.io/08035d8-small-yelp-dev-portal.png)\\ \\ ![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Request Monthly Report](https://docs.developer.yelp.com/reference/create_monthly_reports_v3)

[![Get Monthly Report](https://files.readme.io/08035d8-small-yelp-dev-portal.png)\\ \\ ![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Get Monthly Report](https://docs.developer.yelp.com/reference/get_monthly_reports_v3)

> ## 📘
> 
> Check out our Reporting API Reference Page
> 
> ![:owlbert:](https://docs.developer.yelp.com/public/img/emojis/owlbert.png) [Reporting API Endpoints](https://docs.developer.yelp.com/reference/create_daily_reports_v3)

# 

Revision History

| Revision Number | Date | Editor | Summary |
| --- | --- | --- | --- |
| 1.0 | | | Initial Version. |
| 2.0 | October 11, 2017 | Cathy Chou | 1\. Added 'Revision History' section 
2\. Added Descriptions to Business Metrics 
3.Revised Business Metrics nomenclature: num\_total\_page\_views, num\_user\_photos, num\_desktop\_page\_views 
4.Minor style fixes |
| 3.0 | December 2022 | Florian Traber | Release of Reporting API V3 |

Copy Page