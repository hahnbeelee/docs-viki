# Source: https://docs.developer.yelp.com/docs/yelp-insights

This set of endpoints lets Yelp Insights partners retrieve real-time Yelp data to better understand market trends and consumer preferences.

Please note that some of these endpoints are also available to Yelp Places partners. Each partner will have their own contract that governs the accessible endpoints and available data. This page is meant as a high-level guide, not a definitive source on data access.

Retrieving data via API is a two-step process: first resolve a business to its **Yelp business id**, then use that id to retrieve or send data.

## 

Step 1: Discover a Yelp business id

Most endpoints are keyed on a Yelp business id. Use one of the following endpoints to resolve a business to its Yelp business id, depending on what you know about it.

| Endpoint | What it does | Example |
| --- | --- | --- |
| [**Business Search**](https://docs.developer.yelp.com/reference/v3_business_search) | Find Yelp pages that match a set of filters (location, category, price, attributes). | • Coffee within 1km of lat `41.7873`, long `-123.0515` 
• Birria near `94123` 
• `$$` restaurants that take reservations in Mission District, SF 
• Starbucks in San Francisco |
| [**Business Match**](https://docs.developer.yelp.com/reference/v3_business_match) | Find the Yelp page that most closely matches an input name, address, and phone. | Name: McDonald's 
Address: 123 Main St 
City: San Francisco 
State: CA 
Zip: 94123 
Phone: +14152223333 |
| [**Phone Search**](https://docs.developer.yelp.com/reference/v3_business_phone_search) | Find all Yelp pages associated with a given phone number. | Phone: +12813308004 |

## 

Step 2: Retrieve or send data for a business id

Once you have a business id use these endpoints to pull insights or send data back to Yelp.

| Endpoint | Data available |
| --- | --- |
| [**Business Details**](https://docs.developer.yelp.com/reference/v3_business_info) | POI data, operating data, viability score, year-over-year growth, photos & captions |
| [**Private Reviews**](https://docs.developer.yelp.com/docs/private-reviews-api) | Yelp star rating, full-text reviews, review id |
| [**Food & Drinks Insights**](https://docs.developer.yelp.com/reference/v3_get_business_food_and_drinks_insights) | Food offered, drinks offered, food ingredients, count of mentions |
| [**Engagement Metrics**](https://docs.developer.yelp.com/docs/engagement-metrics-api) | Engagement metrics |
| [**Reporting**](https://docs.developer.yelp.com/docs/reporting-api) | Activity metrics |
| [**Risk Signal Insights**](https://docs.developer.yelp.com/reference/v3_get_business_risk_signals_insights) | Consumer intent / risk signal metrics |
| [**Business Insights**](https://docs.developer.yelp.com/reference/v3_businesses_insights) | Safety score, customer experience score |
| [**Respond to Reviews**](https://docs.developer.yelp.com/docs/respond-to-reviews-api-v2) | Post business owner responses to consumer reviews on Yelp \*intakes review id retrieved from private reviews endpoint instead of a Yelp business id |
| [**Business Subscriptions**](https://docs.developer.yelp.com/docs/business-subscriptions-api) | This endpoint toggles the partners data access on/off for specific Yelp business ids |

> ## 📘
> 
> Access note
> 
> The Insights data endpoints (Business Insights, Food & Drinks Insights, Risk Signal Insights, Engagement Metrics) require special permissions to be enabled on your Yelp API key. Contact your Yelp account team to configure access.

## 

Alternate data delivery method

Instead of pulling data on demand from the APIs above, partners can have Yelp deliver the same data in bulk. Yelp uploads daily or monthly data as JSON files to a S3 bucket on our account that you have access to. See [Partner Feeds](https://docs.developer.yelp.com/docs/partner-feeds).

## 

Learn more

Visit [business.yelp.com/data/products/insights-api/](https://business.yelp.com/data/products/insights-api/).

Copy Page