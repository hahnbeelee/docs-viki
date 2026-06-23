# Source: https://docs.developer.yelp.com/docs/faqs

## 

General

Q: What clients have access to R2R? 
A: R2R is available for mutual enterprise customers and customers who have purchased Yelp + Listing Management. Mutual Enterprise Customers are defined as 10+ locations with enabled Branded Profiles, Enhanced Profiles, or CPC Ads from Yelp. Yelp Insights + Listing Management customers are those who have purchased this new product sku from Yelp approved partners (full list of partners at [https://business.yelp.com/partners/](https://business.yelp.com/partners/) and [https://business.yelp.com/data/products/insights-api/](https://business.yelp.com/data/products/insights-api/).

Q: Can clients respond privately and publicly in partner dashboards? 
A: Public response is available and ready to use via API. Private responses are not available in the API at the moment.

Q: How many public responses can a business owner post per day? 
A: A business owner can post up to 20 public responses per day per location.

Q: Should we offer any tips on responses if our clients ask? 
A: Yes, and keep it simple. Yelp publishes tips on responding to reviews [here](https://biz.yelp.com/support/responding_to_reviews).

Q: Can I offer a discount or ask customers to sign up for my email marketing list in my response? 
A: No, providing marketing offers or requesting email sign-ups is against Yelp’s R2R policy.

Q: Does it matter who replies to reviews? Can partners or agents reply on the business’s behalf? 
A: Only clients should be responding. Partner employees should never respond on behalf of a client.

Q: How many reviews are permitted to be retrieved per business location into the partner dashboard? 
A: The Yelp Insights Program allows the most recent 200 reviews.

Q: Can I export my reviews from the partner's dashboard? 
A: Exporting Reviews outside of the Partner's Dashboard is expressly prohibited.

## 

Business User Account and Claiming

Q: Can the client use a Logo instead of a Photo for setting up review response? Is having a profile image even required? 
A: R2R API requires a logo or photo of the owner in their Yelp BOA in order to enable review response functionality. Yes, logos are allowed, but we suggest real photos to improve your customer experience. If the client is receiving push-back about logos from Yelp’s vetting team, please escalate to Yelp via [partner-support@yelp.com](https://docs.developer.yelp.com/partner-support@yelp.com) and Yelp will share logo with our User Ops team for approval (typically 48 hours or less turnaround).

Q: What if my client is an individual franchisee, how will this work? 
A: Franchisees will be able to respond under the Corporate Admin account or "Customer Support" to respond to reviews. Each individual Franchisee can also respond depending on how Corporate would like to handle. Yelp AMs have ability to turn off review response for individual franchisees if necessary, but the API can support both Corporate and Franchisee response.

Q: What if the business wants to respond as “Customer Service” or “Manager”? 
A: No problem. Corporate is allowed to respond as “Customer Support” and this can be updated in the Yelp Business Owner Dashboard. Other options are Owner or Employee. If Owner, Manager or Employee is chosen response will be shown as “Comment from John D. of Business X” with “Owner, Manager or Employee” written underneath.

Q: How does a client create a Yelp Business Owner Account “BOA” and what happens after they create an account? 
A: Please see Creating a Yelp Biz Owner Admin Flow in the Policies Section.

Q: For this [endpoint](https://docs.developer.yelp.com/reference/get_businesses_associated_with_access_token) to get all business\_ids associated with an oauth token, what does ‘associated with’ mean? Does this return business which the user with the oauth\_token has “claimed”? Or could this also return ids for which a user is in a ‘CUSTOMER\_SUPPORT’ role or something similar? 
A: The returned biz ids are a list of every location that a business owner has claimed. The CUSTOMER SUPPORT vs. OWNER vs. MANAGER are just labels on our end and don’t dictate any different permission levels, they’re all effectively the same.

Q: Can one Yelp business be claimed by multiple entities? For example, the owner of the biz plus an agency that manages it. 
A: Yes, multiple business owner accounts can be claimed on the same biz id at the same time. This is common with Franchises and larger brands where corporate folks and local branch/CS managers all need access to the same location for various reasons (advertising, listing management, review response etc.)

Q: Is it possible to make 2 separate calls to this [endpoint](https://docs.developer.yelp.com/docs/respond-to-reviews-api#retrieve-businesses-associated-with-access-token) with 2 separate oauth\_tokens, and get back the same biz\_id? 
A: Yes.

## 

API Validation and Errors

Q: What is the order of priorities when validating a submitted review response? 
A: Outlined below:

- Has the partner subscribed to the location?
- Has the business owner claimed the location?
- Does the business owner have an approved name?
- Does the business owner have an approved photo?
- Has that review been responded to already?
- Is the business owner’s oAuth token active?
- Does the review response contain disallowed characters? (check for emojis, UTF-8 characters supported)

Q: How do we resolve: “This location does not include the respond-to-reviews feature. Contact your official Yelp Partner for more information.”? 
A: This error means you haven’t subscribed to the location before trying to respond to reviews. If you subscribe then retry you should be successful.

Q: Can we export Yelp reviews to a 3rd party platform like a CRM? 
A: No, Yelp Reviews are not able to be exported out of the partners platform to any third party system.

Q: How soon do the APIs reflect updates after a webhook event occurs? The use case is if we receive a REVIEW\_REMOVED\_EVENT from the webhook and immediately make a request to the Private Reviews API, would the response exclude that removed review? 
A: Yes, the Private Reviews API should be the same as the review webhook i.e. if you get a review\_removed webhook, that id should be removed from the API response.

Q: Do we have to use the whitelist add endpoint if we’re already subscribing to a biz id via the LOCATION SUBSCRIPTION API? 
A: Yes, opting into webhook notifications is a different endpoint than the location subscription API referenced above. You’ll use your Fusion API credentials and add businesses that you want webhooks for via this endpoint.

Q: When our customers go through the oAuth flow, they see a prompt to “Grant \[partner\] access to your Yelp for Business Account”, can we change the \[partner\] name that displays? 
A: Yes we can change that name, but it will be a static name, we can’t dynamically change that display name for different biz owners.

Q: Can we use the graphql endpoints to retrieve bulk biz information rather than one at a time? 
A: Yes, request this via [partner-support@yelp.com](mailto:partner-support@yelp.com)

Q: Do we get image urls uploaded by the review author in the Private Reviews API? 
A: No, we can expose photos via the JSON feed but id doesn’t explicitly tie the review\_id to the photo\_id. You could use user\_id and timestamp though to effectively tie those two together.

Q: What is the process to “merge” duplicate locations? 
A: Here’s the process: 
Our team will merge duplicate pages when they find them. 
This endpoint gives information on past merge activity. 
If you find apparent duplicates that need to be merged, we’ll process these through a shared escalations sheet.

Q: For the OAuth step, what happens if we try to use a redirect\_uri that hasn’t been previously whitelisted on Yelp’s end? 
A: The request will fail with a 400.

## 

Webhooks

Q: Do we receive webhook events for reviews beyond the most recent 200 reviews? Specifically the REVIEW\_REMOVED\_EVENT 
A: No, the webhooks fire on any new events, not necessarily tied to the 200 review threshold.

Q: Do we receive a webhook event if a review moves from recommended to non-recommended? 
A: No, we suggest refreshing the most recent 200 reviews on a regular cadence to ensure you’re showing only recommended reviews (which is what we give you via API).

Q: What are the webhook time zones? 
A: Examples: 
Webhook payload: "time": "2021-08-31T18:07:42.116792", 
Time in PST the webhook was received: 2021-08-31 11:07am PT

Q: Is there a way to retrieve details about a single review, given that we have the review\_id? 
A: No, you’d need to query the biz\_id to get the most recent 200 reviews then capture the review\_id you’re expecting in that responses. There’s no endpoint that receives a review\_id and responds with relevant details.

Q: The API docs states the Private Reviews APi only returns the 200 most recent reviews. What would happen if we have a valid review\_id, but it’s the 201st review in the list? 
A: You wouldn’t see that returned in the response.

## 

Review Behavior

Q: What’s the difference between editing and updating a review? 
A: Check out this [page](https://www.yelp-support.com/article/How-do-I-edit-one-of-my-reviews?l=en_US) and this [page](https://www.yelp-support.com/article/How-do-I-post-an-update-to-one-of-my-reviews?l=en_US).

Q: How could we make sense of updated vs. edited reviews? 
A: Updates to reviews come in as a separate review with a different review\_id from the same user\_id, this update effectively replaces the previous review's rating and review\_count for the business i.e it gets removed from the reviews endpoint too. Quickly highlighting behavior below with an example:

- Consumer leaves a review in 2020 review\_id: 1
- Biz owner responds in 2020
- In 2021 user updates their review, you get a new\_review\_event webhook with the same biz id and user id as before but with review\_id: 10.
- When you query the Private Reviews API for this biz id, you see the new review and user's review text but the public\_response field is already populated with the previous owner's previous reply. If the user instead edited the review rather than updating it, you'd see that come in on the same review\_id with a review\_edited webhook event. Note a user can only edit a review within 30 days of posting the original review.

Q: What does the API response look like if a review response gets removed by the user natively? 
A: Deleted review won’t show up in the API response, but you do get a webhook for it.

Q: Are the reactions to reviews: “Useful”, “Funny”, “Cool” available via API? 
A: No, not today.

Q: Does Yelp API support deleting existing reviews? 
A: We don’t support any deletion of reviews left by consumers, except if the consumer deletes it themselves. Business owners' responses to reviews can be removed but they have to do so via logging into biz.yelp.com. This isn’t supported by an API today.

## 

Fusion API and Related Data

Q: I see this note in the ‘business details’ endpoint “Note: at this time, the API does not return businesses without any reviews.” Can we get an exception to this behavior? 
A: Request this via [partner-support@yelp.com](mailto:partner-support@yelp.com).

Q: The “Get Businesses Associated with Access Token” endpoint returns business ids. Do we need to use the Fusion API and request business details for each one? Is there a way to make a single request for a batch of business ids? 
A: Via the Fusion API: you’d use the business details endpoint to query more info about each returned id. These requests are done 1 biz id at a time. We can set a rate limit that allows you to process these requests in bulk. OR we can set you up with access to the GraphQL endpoint.

Q: We have noticed that the images url on Fusion API end with “o.png”, we may need other sizes, is this supported? 
A: Yes, you can change that “o”, other accepted options are l,ls,m,s,xs,ls,ms,ss, & xss

Q: Can we have access to page rankings on Yelp? 
A: Not exactly, via the Reporting API we give raw metrics like clicks/views, but we don’t expose the equivalent % rank for the location’s cat/geo.

Updated 5 months ago

---

Did this page help you?

Yes

No

Copy Page