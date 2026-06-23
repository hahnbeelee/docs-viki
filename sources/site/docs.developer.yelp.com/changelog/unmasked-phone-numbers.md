# Source: https://docs.developer.yelp.com/changelog/unmasked-phone-numbers

[Back to All](https://docs.developer.yelp.com/changelog)

improved

Unmasked Phone Numbers: Consumer phone numbers are now available unmasked via the new phone\_number field in the Leads API response. The temporary\_phone\_number field continues to be populated for backward compatibility, with a far-future expiry date. Clients should migrate to phone\_number. Eligibility: leads where the consumer opted in on or after August 2025.