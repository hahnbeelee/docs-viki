# Source: https://docs.developer.yelp.com/docs/iframe-interactions

## 

Overview

A partner's menu page displayed in an Iframe(the iframe page) often has rich UI interactions such as dropdown, accordion or popup. These interactions oftentimes require communication and data passing between the iframe page and parent page in order to display things correctly. This document provides the guidelines of cross-domain communication for different interactions.

For any style or developer guidelines, please make sure you review [this](https://docs.developer.yelp.com/docs/iframe-style-developer-guidelines) guide.

## 

Requirements

The method used for cross-domain communication is `window.postMessage`. This method is supported by FF3+, IE8+, Chrome, Safari4+, Opera9.5+ ([http://caniuse.com/x-doc-messaging](http://caniuse.com/x-doc-messaging)). In the browsers that don't support `postMessage`, we will display a blank page with a message to upgrade the browsers.

Yelp uses the `setHeight` event to determine when to dismiss the webview's loading spinner. The partner is responsible for making sure that the iFrame contents are interactable before calling `setHeight`.

## 

Frame URL and Content

This is the URL that Yelp will specify in the iframe to initiate the ordering flow on the partner's site.

It must be HTTPS. The iframe page must use HTTPS assets as well or browsers will raise mixed content warnings.

A `yelp_site` query parameter will be added to iframe URLs to mitigate the risk of mixed experiences between a menu page and its host.

`yelp_site` will be one of `www` or `m`

yelp\_locale is described below

Currently, devices families supported by Yelp's mobile site are:

- iPhone
- iPod
- FirefoxOS
- Android (tablet and phones)

Note the exclusion of iPads, Windows phone and Blackberry devices for instance. Those device will be served Yelp's desktop site ([www.yelp.com](http://www.yelp.com)) and **should get a desktop menu page** to avoid mixed experiences.

## 

URL template

`https://<partner_domain_path>/<partner_business_id>/?opportunity_token=<oppotunity_token>&yelp_site=m&yelp_locale=en_US`

The `partner_domain_path` shall be pre-registered with Yelp.

## 

Request Params

| Property | Type | Description |
| --- | --- | --- |
| partner\_business\_id | utf8\_string | business\_id provided by partner in feed to Yelp |
| opportunity\_token | uuid\_hex | token with which Partner can use to lookup delivery address using Yelp Checkout API or to lookup in their caches if they stored it temporarily during the delivery address check on Yelp’s biz details page |
| yelp\_site | utf8\_string | will be one of `www` or `m` |
| yelp\_locale | utf8\_string | see below for more details |

## 

Sending Messages To Yelp

To send a message to its parent window, a partner's iframe must use the `postMessage` API:

JavaScript

`window.top.postMessage(message, targetOrigin)`

## 

message param

- Must contain information about the event type (e.g., `setHeight`, `scrollTop`. See table below for details)
- May contain more properties, depending on the event type
- Must be a JSON encoded string

## 

targetOrigin param

The value of this param must be computed by partners, based on two GET params added by Yelp to iframe URLs, yelp\_site and yelp\_locale

Partners must validate GET params to prevent against potential targetOrigin hijacking.

- `yelp_site` should be one of (`www`, `m`). If no valid `yelp_site` is provided, it is safe to throw an error.
- `yelp_locale` should be a valid yelp locale. If no valid `yelp_locale` is provided, it is safe to throw an error.

Here's a table showing mappings between different values of `yelp_site`, `yelp_locale` and `targetOrigin`.

| yelp\_site | yelp\_locale | targetOrigin |
| --- | --- | --- |
| www | en\_US | [https://www.yelp.com](https://www.yelp.com) |
| m | en\_US | [https://m.yelp.com](https://m.yelp.com) |
| www | en\_GB | [https://www.yelp.co.uk](https://www.yelp.co.uk) |
| m | en\_GB | [https://m.yelp.co.uk](https://m.yelp.co.uk) |
| www | fr\_FR | [https://www.yelp.fr](https://www.yelp.fr) |
| m | fr\_FR | [https://m.yelp.fr](https://m.yelp.fr) |
| www | fr\_CA | [https://fr.yelp.ca](https://fr.yelp.ca) |
| m | fr\_CA | [https://fr.m.yelp.ca](https://fr.m.yelp.ca) |
| www | it\_CH | [https://it.yelp.ch](https://it.yelp.ch) |
| m | it\_CH | [https://it.m.yelp.ch](https://it.m.yelp.ch) |
| www | ch\_CH | [https://www.yelp.ch](https://www.yelp.ch) |
| m | ch\_CH | [https://m.yelp.ch](https://m.yelp.ch) |
| www | cs\_CZ | [https://www.yelp.cz](https://www.yelp.cz) |
| m | cs\_CZ | [https://m.yelp.cz](https://m.yelp.cz) |
| www | da\_DK | [https://www.yelp.dk](https://www.yelp.dk) |
| m | da\_DK | [https://m.yelp.dk](https://m.yelp.dk) |
| www | de\_DE | [https://www.yelp.de](https://www.yelp.de) |
| m | de\_DE | [https://m.yelp.de](https://m.yelp.de) |
| www | de\_AT | [https://www.yelp.at](https://www.yelp.at) |
| m | de\_AT | [https://m.yelp.at](https://m.yelp.at) |
| www | de\_CH | [https://de.yelp.ch](https://de.yelp.ch) |
| m | de\_CH | [https://de.m.yelp.ch](https://de.m.yelp.ch) |
| www | en\_AU | [https://www.yelp.com.au](https://www.yelp.com.au) |
| m | en\_AU | [https://m.yelp.com.au](https://m.yelp.com.au) |
| www | en\_BE | [https://en.yelp.be](https://en.yelp.be) |
| m | en\_BE | [https://en.m.yelp.be](https://en.m.yelp.be) |
| www | en\_CA | [https://www.yelp.ca](https://www.yelp.ca) |
| m | en\_CA | [https://m.yelp.ca](https://m.yelp.ca) |
| www | en\_HK | [https://en.yelp.com.hk](https://en.yelp.com.hk) |
| m | en\_HK | [https://en.m.yelp.com.hk](https://en.m.yelp.com.hk) |
| www | en\_IE | [https://www.yelp.ie](https://www.yelp.ie) |
| m | en\_IE | [https://m.yelp.ie](https://m.yelp.ie) |
| www | en\_NZ | [https://nz.yelp.com](https://nz.yelp.com) |
| m | en\_NZ | [https://nz.m.yelp.com](https://nz.m.yelp.com) |
| www | en\_SG | [https://www.yelp.com.sg](https://www.yelp.com.sg) |
| m | en\_SG | [https://m.yelp.com.sg](https://m.yelp.com.sg) |
| www | es\_AG | [https://www.yelp.com.ar](https://www.yelp.com.ar) |
| m | es\_AG | [https://m.yelp.com.ar](https://m.yelp.com.ar) |
| www | es\_CL | [https://www.yelp.cl](https://www.yelp.cl) |
| m | es\_CL | [https://m.yelp.cl](https://m.yelp.cl) |
| www | es\_ES | [https://www.yelp.es](https://www.yelp.es) |
| m | es\_ES | [https://m.yelp.es](https://m.yelp.es) |
| www | es\_MX | [https://www.yelp.com.mx](https://www.yelp.com.mx) |
| m | es\_MX | [https://m.yelp.com.mx](https://m.yelp.com.mx) |
| www | fi\_FI | [https://fi.yelp.fi](https://fi.yelp.fi) |
| m | fi\_FI | [https://fi.m.yelp.fi](https://fi.m.yelp.fi) |
| www | fr\_BE | [https://fr.yelp.be](https://fr.yelp.be) |
| m | fr\_BE | [https://fr.m.yelp.be](https://fr.m.yelp.be) |
| www | fr\_CH | [https://fr.yelp.ch](https://fr.yelp.ch) |
| m | fr\_CH | [https://fr.m.yelp.ch](https://fr.m.yelp.ch) |
| www | it\_CH | [https://it.yelp.ch](https://it.yelp.ch) |
| m | it\_CH | [https://it.m.yelp.ch](https://it.m.yelp.ch) |
| www | it\_IT | [https://www.yelp.it](https://www.yelp.it) |
| m | it\_IT | [https://m.yelp.it](https://m.yelp.it) |
| www | ja\_JP | [https://www.yelp.co.jp](https://www.yelp.co.jp) |
| m | ja\_JP | [https://m.yelp.co.jp](https://m.yelp.co.jp) |
| www | nb\_NO | [https://www.yelp.no](https://www.yelp.no) |
| m | nb\_NO | [https://m.yelp.no](https://m.yelp.no) |
| www | nl\_NL | [https://www.yelp.nl](https://www.yelp.nl) |
| m | nl\_NL | [https://m.yelp.nl](https://m.yelp.nl) |
| www | nl\_BE | [https://nl.yelp.be](https://nl.yelp.be) |
| m | nl\_BE | [https://nl.m.yelp.be](https://nl.m.yelp.be) |
| www | pl\_PL | [https://www.yelp.pl](https://www.yelp.pl) |
| m | pl\_PL | [https://m.yelp.pl](https://m.yelp.pl) |
| www | pt\_PT | [https://www.yelp.pt](https://www.yelp.pt) |
| m | pt\_PT | [https://m.yelp.pt](https://m.yelp.pt) |
| www | pt\_BR | [https://www.yelp.com.br](https://www.yelp.com.br) |
| m | pt\_BR | [https://m.yelp.com.br](https://m.yelp.com.br) |
| www | sv\_FI | [https://sv.yelp.fi](https://sv.yelp.fi) |
| m | sv\_FI | [https://sv.m.yelp.fi](https://sv.m.yelp.fi) |
| www | sv\_SE | [https://www.yelp.se](https://www.yelp.se) |
| m | sv\_SE | [https://m.yelp.se](https://m.yelp.se) |
| www | tr\_TR | [https://www.yelp.com.tr](https://www.yelp.com.tr) |
| m | tr\_TR | [https://m.yelp.com.tr](https://m.yelp.com.tr) |
| www | zh\_HK | [https://zh.yelp.com.hk](https://zh.yelp.com.hk) |
| m | zh\_HK | [https://zh.m.yelp.com.hk](https://zh.m.yelp.com.hk) |

## 

Concrete example

Makes the parent Yelp page scroll to a vertical offset of 64px: 
(inside https://<partner\_domain\_path>/menu/123?opportunity\_token=&yelp\_locale=en\_US&yelp\_site=www)

JavaScript

`window.top.postMessage(     '{"eventType": "scrollTop", "offset": "64"}',     'https://www.yelp.com' );`

Same example, from the French mobile site:

(inside https://<partner\_domain\_path>/menu/123?opportunity\_token=&yelp\_locale=fr\_FR&yelp\_site=m)

JavaScript

`window.top.postMessage(     '{"eventType": "scrollTop", "offset": "64"}',     'https://m.yelp.fr' );`

## 

Mobile vs. Desktop context

A `yelp_site` URL param (values: `www` or `m`) is added by Yelp to iframe URLs. This indicates to partners if their pages are loaded in a desktop or mobile context.

Partners may use this to customize their iframe based on the current context.

## 

Testing

You can test your iframe and these API's once you've activated your test business widget.

Copy Page