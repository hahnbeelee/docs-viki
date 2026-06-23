# Source: https://docs.developer.yelp.com/docs/checkout-api

> ## 📘
> 
> This is a Yelp Partner API
> 
> Access is disabled by default. See [Yelp Partner APIs](https://docs.developer.yelp.com/docs/yelp-partner-apis) on how to get access.

# 

Overview

This specifies the API provided by Yelp that allow partners to create/update/cancel orders that were initiated on the Yelp website/app.

## 

Authentication

The Checkout API uses HTTP Basic Auth over HTTPS. A username and password will be assigned to you, which you should specify in the "Authorization" HTTP header for all Checkout API requests.

## 

API Errors

When there is an error with any of the API calls, the response will have a non-200 HTTP status code and a JSON body describing the error. Besides from the common API errors listed, each API call will have its own errors described in their respective sections.

JSON

`{   "error": {     "code": "401_UNAUTHORIZED",     "description": "This server could not verify that you are authorized to access the document requested.  Either you supplied the wrong credentials (e.g., bad password), or your browser doesn't understand how to supply the credentials required."   } }`

## 

Upgrading from v2 checkout APIs

- The v3 Order object has an additional attribute `collection_type`. For orders with `prepaid` collection\_type, users will be charged as soon as order will be submitted on Yelp, without requiring explicit/complete API call from partners.
- Update and cancel operations on orders will be asynchronous.
- [OrderStatusChangeNotification](https://docs.developer.yelp.com/docs/resources#section-orderstatuschangenotification) object now includes user's fulfillment information (email address, phone number etc if at\_customer option) and any Yelp coupon discount information, if applicable.

# 

IFrame URL and Content

This is the URL that Yelp will load in an iframe to initiate the ordering flow on the partner's site.

It must be HTTPS. The iframe page must use HTTPS assets as well or browsers will raise mixed content warnings.

A `yelp_site` query parameter will be added to iframe URLs to mitigate the risk of mixed experiences between a menu page and its host.

`yelp_site` will be one of {`www`|`m`}

Currently, devices families supported by Yelp's mobile site are:

- iPhone
- iPod
- FirefoxOS
- Android (tablet and phones)

Note the exclusion of iPads, Windows phone and Blackberry devices for instance. Those device will be served Yelp's desktop site ([www.yelp.com](https://www.yelp.com)) and should get a desktop menu page to avoid mixed experiences.

## 

URL template

`https://<partner_domain_path>/<partner_business_id>/?opportunity_token=<opportunity_token>&yelp_site=m&yelp_locale=en_US`

The `partner_domain_path` shall be pre-registered with Yelp.

### 

Request Params

| Property | Type | Description |
| --- | --- | --- |
| partner\_business\_id | utf8\_string(1..100) | business\_id provided by partner in feed to Yelp |
| opportunity\_token | uuid\_hex | token with which Partner can use to lookup delivery address using Yelp Checkout API or to lookup in their caches if they stored it temporarily during the delivery address check on Yelp’s biz details page |
| pickup | boolean | `true` if the user wants to pick up order |
| yelp\_site | utf8\_string | will be one of `www` or `m` for desktop and mobile sites |
| yelp\_locale | utf8\_string | see Iframe Specification for more details |

## 

Double Submit Behavior

Yelp strongly recommends that partners implement double submit protection. That is, partners should call `/checkout/orders/create/v3` only once per user order during the iframe flow.

Copy Page