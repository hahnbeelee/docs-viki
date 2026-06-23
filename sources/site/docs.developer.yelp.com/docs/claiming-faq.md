# Source: https://docs.developer.yelp.com/docs/claiming-faq

##### 

Note: Yelp's SMB Claiming API is designed for our partner's small and medium-sized business (SMB) clients, and is not intended for enterprise business clients. Please contact [partner-support@yelp.com](mailto:partner-support@yelp.com) if you have questions about claiming listings.

### 

Can a new business created by the API be claimed immediately?

No - our User Operations team needs to review and approve the business before it can be claimed. The approval process typically takes 1-2 business days.

### 

Can the claim email be resent to the business owner?\*

Yes, you will have to revoke the business claim and submit a new claim request to the business owner's email address.

### 

A Partner customer has a listing that is not in Yelp, and they initiate the business creation process for Yelp in the Partner’s UI. While the listing is in the queue to be approved by Yelp staff, can the process be cancelled via API?

No, we currently don't have a way to cancel the business creation process and remove it from the queue.

### 

A Partner customer submits a misspelled or incorrect email address to Yelp. Can Partner cancel the current authorization request via the API, then submit a new email address?

Yes, you will have to revoke the business claim with the incorrect email address and submit a new claim request with the corrected email address.

### 

A Yelp listing can have more than one owner. Is there a limit to how many co-owners a Yelp listing can have?

No, there is not a limit. However, it’s rare to see more than 10 account owners on one listing for local businesses.

### 

When a Partner submits an email address for an already-claimed location, does the notification email go to all owners?

No, the notification email only goes to the submitted email address.

### 

A partner customer submits one email address for multiple listings at the same time to Yelp. How many notification emails from Yelp will they receive?

Currently, the partner may receive several notification emails for each location, however the business owner will receive one email notifying them how many locations have been claimed. We expect to resolve this issue for Partner’s employees by mid-March (partner employee will receive one daily “round-up” email of all locations claimed).

### 

A Partner’s customer moves one of their businesses to a new address and updates the NAP info, which then syncs to Yelp. Is that new address considered the same location in Yelp or a new location?

It's considered the same location on Yelp.

### 

A customer closes a location in the Yelp UI that is being synced with the Partner. How would that affect Partner’s ability to edit that listing?

Once a biz is closed, we don't allow further edits for the business.

### 

A Partner customer syncs their listings with Yelp, and one day they delete their BOA on the Yelp website. Would Partner still be authorized to make updates to those listings?

Technically, Partner account will still be authorized to make updates. However, this is very rare that a customer deletes their BOA account, and furthermore we’d expect Partner to send over a new email.

### 

If a business is created by Partner and then rejected, will there be a status provided as to why?

Not right now, although this is being worked on. If a business is rejected, it is likely due to it being ineligible for a Yelp listing (i.e. online only, B2B, or it’s matched to a closed listing).

### 

What happens if a business owner claimed their Yelp listing, but has not logged in for months or cannot remember password and Partner sends over a new, different email the same business owner?

If a business owner has not been active in over 90 days, Yelp will remove current biz owner and send an email. The new email and owner that were passed from Partner will gain access. The former claimee, will have ability to re-gain access after 90 days of inactivity from the new claimee. Alternatively, The new account [holder](https://www.yelp-support.com/article/How-do-I-set-up-additional-logins-for-my-Yelp-Business-Account?l=en_US) can also share access to the business account by inviting additional users. If none of the above has worked, please [contact](http://yelp.com/support/contact/business_claim?src_article_id=000005375) Yelp’s support team.

### 

What happens if the biz owner has been in active in last 90 days, and Partner sends over a new email and business owner to that listing?

No email goes to current biz owner if they have been active within 90 days. The requested email will just be added as a co-owner after they claim. If the current biz owner has been inactive for 90 days, they will be removed and get an email. We will monitor this and see how often this happens. Our Customer Ops team will be prepared to reinstate the current biz owner.

### 

Is there any way to create a business and claim it at the same time?

You can create _and_ claim a business in a single API call using our Data Ingestion API. Please reference our [Create and Claim](https://docs.developer.yelp.com/docs/claiming#claims_api_create) guide.

Updated over 2 years ago

---

Did this page help you?

Yes

No

Copy Page