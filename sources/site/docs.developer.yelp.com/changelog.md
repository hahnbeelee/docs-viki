# Source: https://docs.developer.yelp.com/changelog

improved

# [Unmasked Phone Numbers](https://docs.developer.yelp.com/changelog/unmasked-phone-numbers)

2 months ago by Austin Delong

Unmasked Phone Numbers: Consumer phone numbers are now available unmasked via the new phone\_number field in the Leads API response. The temporary\_phone\_number field continues to be populated for backward compatibility, with a far-future expiry date. Clients should migrate to phone\_number. Eligibility: leads where the consumer opted in on or after August 2025.

improved

# [Fusion AI API: Reservation support fields added](https://docs.developer.yelp.com/changelog/fusion-ai-api-reservation-support-fields-added)

12 months ago by Ankur Agrawal

Two new attributes — **reservation\_availability** and **accepts\_reservations\_through\_yelp**— have been added to each business in the response. These fields provide live reservation slots and show if bookings are available directly through Yelp Guest Manager.

added

# [AI-Assisted Reservations](https://docs.developer.yelp.com/changelog/ai-assisted-reservations)

12 months ago by Abhiraj Butala

Let users book restaurant tables conversationally with Fusion AI API. Tap into thousands of restaurants across US & Canada that manage reservations through Yelp Guest Manager.

improved

# [Fusion AI API enhanced: Smarter conversations & direct business questions](https://docs.developer.yelp.com/changelog/fusion-ai-api-enhancements-smarter-conversations-direct-business-questions)

over 1 year ago by Abhiraj Butala

We've enhanced the Fusion AI API with improved conversational search, multi-turn interactions, and direct business questions, all powered by Yelp's latest business data & reviews. These updates provide more accurate responses and a smoother user experience. Learn more: [Fusion AI API reference](https://docs.developer.yelp.com/reference/v2_ai_chat).

deprecated

# [Natural Language Search API endpoint deprecated](https://docs.developer.yelp.com/changelog/natural-language-search-api-endpoint-deprecated)

over 1 year ago by Abhiraj Butala

The Natural Language Search API endpoint is now deprecated. Please transition to the new Fusion AI API for conversational search, multi-turn interactions, and direct business questions, all powered by Yelp's latest business data and reviews. Learn more: [Fusion AI API reference](https://docs.developer.yelp.com/reference/v2_ai_chat).

added

# [Fusion AI API released: Next generation search & chat](https://docs.developer.yelp.com/changelog/new-ai-api-chat-endpoint-released)

almost 2 years ago by Ankur Agrawal

This endpoint delivers Yelp's trusted local content through conversational AI. With a simple API integration, your users can get local business recommendations and answers conversationally.

deprecated

# [New limits for Business Search endpoint](https://docs.developer.yelp.com/changelog/new-limits-for-business-search-endpoint)

almost 2 years ago by Sven Steinheißer

This update affects all non-paying users and reduces the maximum number of businesses returned from 1,000 to 240 with immediate effect.

deprecated

# [Fusion and GraphQL Daily Rate Limits Changed](https://docs.developer.yelp.com/changelog/fusion-daily-rate-limits-changed)

about 3 years ago by Sven Steinheißer

Today, May 16th 2023, we are changing the daily rate limits for both Fusion and GraphQL for new clients.

added

# [Business Subscriptions API published](https://docs.developer.yelp.com/changelog/business-subscriptions-api-published)

over 3 years ago by Florian Traber

The Business Subscriptions API has been published. This new API combines the Location Subscriptions, Listing Management and Webhooks subscriptions into one simply to use API.

added

# [Reporting API v3 published](https://docs.developer.yelp.com/changelog/reporting-api-v3-published)

over 3 years ago by Florian Traber

Reporting API v3 has been published. This new version includes easier authentication including self serve credential management, improved error messages and other small improvements, while the request and response schemas for successful responses stays the same.