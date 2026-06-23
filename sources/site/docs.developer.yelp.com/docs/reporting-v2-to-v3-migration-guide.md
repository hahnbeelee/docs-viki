# Source: https://docs.developer.yelp.com/docs/reporting-v2-to-v3-migration-guide

# 

Migration Steps

1. Reach out to [partner-support@yelp.com](mailto:partner-support@yelp.com) to help you get started with your Yelp Fusion App. If you're already using other Yelp Fusion APIs you might be able to reuse that App.
 
2. Follow the changelog below to adjust your application.
 

# 

Changelog

- Requesting a monthly or daily report now returns a http status code `202` instead of `200`.
- There's no change in the available metrics and all `2XX` response formats.

## 

New urls

The urls changed and are now available on the `api` subdomain instead of the `partner-api` subdomain.

### 

Daily

#### 

Create

**Old:** `https://partner-api.yelp.com/analytics/v2/businesses/daily_reports` 
**New:** `https://api.yelp.com/v3/reporting/businesses/daily`

#### 

Get

**Old:** `https://partner-api.yelp.com/analytics/v2/businesses/daily_reports/{report_id}` 
**New:** `https://api.yelp.com/v3/reporting/businesses/daily/{report_id}`

### 

Monthly

#### 

Create

**Old:** `https://partner-api.yelp.com/analytics/v2/businesses/monthly_reports` 
**New:** `https://api.yelp.com/v3/reporting/businesses/monthly`

#### 

Get

**Old:** `https://partner-api.yelp.com/analytics/v2/businesses/monthly_reports/{report_id}` 
**New:** `https://api.yelp.com/v3/reporting/businesses/monthly/{report_id}`

## 

Authentication

Authentication was simplified and is now using a [Yelp Fusion App](https://docs.developer.yelp.com/docs/fusion-intro).

> ## 📘
> 
> Set up required
> 
> Please reach out to [partner-support@yelp.com](mailto:partner-support@yelp.com) to get your Fusion App set up for access to Reporting API

| Old | New |
| --- | --- |
| Username and password | API Key |
| Changing credentials is full serve | Refresh your API Key yourself on [Yelp](https://www.yelp.com/developers/v3/manage_app) |
| Getting credentials requires emailing Yelp a PGP Key and receiving an encrypted email | View your API Key yourself on [Yelp](https://www.yelp.com/developers/v3/manage_app) |

[Click here for all details of Yelp Fusion Authentication](https://docs.developer.yelp.com/docs/fusion-authentication)

## 

Errors

- Errors are now nested inside an `error` object
- `code` is no longer an int value equal to the http status code, it's a string value now describing the error in more detail. See the [endpoint](https://docs.developer.yelp.com/reference/create_daily_reports_v3) definitions for the expected values per endpoint and http status.
- renamed `message` to `description` for consistency with other Yelp API errors
- Improved documentation to clarify what kind of http statuses and error codes are expected in particular scenarios

### 

Example

Instead of

JSON

`HTTP Status Code: 413 {   "code": 413,   "description": "The number of businesses in the request exceeded the maximum (500)",   "more_info": null }`

the API will now return

JSON

`HTTP Status Code: 413 {   "error": {     "code": "NUMBER_OF_BUSINESS_LIMIT_ERROR",     "description": "The number of businesses in the request exceeded the maximum (500)"   } }`

Copy Page