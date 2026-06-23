# Source: https://docs.developer.yelp.com/docs/data-ingestion-faqs

## 

Listing Updates

Q: How should we submit UTM parameters? 
A: UTM params not accepted through this API, please only submit the organic page.

Q: What countries are partners allowed to update via the data ingestion api? 
A: US, Canada, & US territories (PR, GU, & VI).

Q: How long do our updates take to be published on Yelp? 
A: This depends on the quality of your data. Based on quality, updates could be applied automatically or could be routed to a moderation queue, which could take up to 2 weeks to be reviewed/dispositioned. These permissions are set on an attribute level, so hours could be auto-published while the URL is sent to our moderation queue.

Q: If we create new locations, how long do these take to be reviewed by Yelp’s team? 
A: This depends on the volume of updates to our queue, but typically are reviewed in ~48 hours.

Q: What are the guidelines for the "About Business Specialties Field"? 
A: Yelp’s team will moderate these pushes. We advise against keyword stuffing as those updates are likely to be rejected.

Q: How does Yelp handle locations that have the same address, but the business names and contact numbers are different? Do you consider these as duplicates? I.e. Shopping malls with multiple businesses, Medical offices with multiple practitioners, Car dealers with different areas of operation. 
A: It depends:

- Yelp will list separate businesses at the same location if they are completely separate.
- If businesses are the same entity the page will be merged.
- This is on a case by case scenario dependent on the services.
- Different doctors would get separate listings as an example.
- The procedure for getting separate listings would be to send the request to Yelp [partner-support@yelp.com](mailto:partner-support@yelp.com) for analysis and recommendation/action.

Q: Can we update categories for a listing? 
A: If the location doesn’t have any categories yet, partners may add them (subject to Yelp’s moderation team's approval). If the location already has categories, we’ll block change attempts via API. If a change is needed please escalate to [partner-support@yelp.com](mailto:partner-support@yelp.com) or via our shared sheet/form.

Q: Are there any permanent banners on profile? That is accessible via API? 
A: There are 2 free-text fields that are displayed:

- “Covid\_19\_virus\_response”
- “About the Business Specialties” SMBs can populate this attribute freely. Businesses with 10+ locations need to be advertising to populate this field.

Q: Does Yelp support “Temporarily Closed” due to covid? 
A: Yes.

- Heres’ how to temp close a business: "temporarily\_closed": "12/31/2020"
- Here’s how to re-open the business: "temporarily\_closed": "" (empty string)

Q: How should we format the data for a location that is temporarily closed but there is no known re-opening date? 
A: Set temporarily\_closed\_until to 10+ years into the future, Yelp will show the location as temporarily closed without any estimated reopening date.

Q: What is the process to “merge” duplicate locations? 
A: Here’s the process:

- Our team will merge duplicate pages on their own as they find them.
- This [endpoint](https://docs.developer.yelp.com/docs/partner-support-api#business-migration-info-api) gives information on past merge activity.
- If you find apparent duplicates that need to be merged, we process these through a shared escalation sheet.

Q: Can we delete photos on Yelp? 
A: You can only delete photos that were added by your partner account.

Q: Do we have the availability to add/update call to action buttons? 
A: No, these are either advertising features that should be handled with Yelp CS, or are via a 3rd party and should be requested by the partner that’s managing that widget (typically food delivery partners).

Q: Does Yelp now have a posts section on their profiles? 
A: Posts are an advertising feature. They’re not available in the advertising API yet, but could be added in the future. “Yelp Connect” enables business owners to put news posts, limited time offers.This is a paid feature add on.

Q: If a customer stops advertising, what happens to their data? 
A: Customers lose metered phone numbers, any tracking URLS, and calls to action on their profile

Q: Can we send you menu data? 
A: Request this via [partner-support@yelp.com](mailto:partner-support@yelp.com)

Q: Does Yelp support split hours for business hours that are spread across two days (like 4pm to 2am) 
A: Yes, check update.hours\[\].close in the data ingestion [docs](https://docs.developer.yelp.com/docs/data-ingestion-api).

Q: Can we update unclaimed listings? 
A: Yes, permissions aren’t tied to claimed status.

Q: Where can we find Yelp’s category list? 
A: [Here](https://www.yelp.com/developers/documentation/v3/all_category_list).

## 

Billing and Subscriptions

Q: How do we enable a location for Yelp listing updates? 
A: You'll need to subscribe to business ids to unlock listing update permissions. Where and how to subscribe can vary slightly by partner. If you need additional clarity on where/how to subscribe to business\_ids, please request this via [partner-support@yelp.com](mailto:partner-support@yelp.com).

Q: How do we disable a location for Yelp listing updates? 
A: Unsubscribe aka “remove” business ids. Similar to the above, please reach out to [partner-support@yelp.com](mailto:partner-support@yelp.com) if more clarity is needed.

Q: How should we use the [location subscription](https://docs.developer.yelp.com/docs/location-subscription-api-v2) and [listing management subscription](https://docs.developer.yelp.com/docs/listing-management-api) APIs? 
A: These impact billing on Yelp’s end. We’ll send you a diagram of where you should subscribe to biz ids (this can vary by partner). The most important part about subscriptions is to “add” locations when they have access to the Yelp add-on, and to immediately “remove” them whenever that service has churned. If the location remains active and is subscribed, that location will be subject to an invoice. Please be sure to actively manage the Yelp subscriptions to ensure that status mirrors the customer’s status on the partner’s side.

Q: How do we identify Mutually Enterprise Customers (MECs)? 
A: When you send this [request](https://docs.developer.yelp.com/reference/v3_business_info) you'll see not publicly documented "is\_enterprise\_advertiser": true/false attribute come back in our response, which means is\_mec. If you're not seeing this attribute for your API key and you're a contracted Yelp partner, please reach out to [partner-support@yelp.com](mailto:partner-support@yelp.com) to have this enabled for you.

Copy Page