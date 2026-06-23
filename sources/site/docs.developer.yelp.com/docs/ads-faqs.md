# Source: https://docs.developer.yelp.com/docs/ads-faqs

## 

Ad creation

### 

What are the requirements to launch a CPC ad program on Yelp?

- Location needs a category
- Category needs to be eligible for search ads

Note: Yelp CPC ads will either use review text OR the about the business specialties field (free text info about the biz). In cases where there is neither - the ad will be accepted and will run only for “mobile search ads” which are served to mobile devices.

### 

What fields should we populate to ensure the biz has the best content?

We suggest adding the below information via the data ingestion api for businesses where available:

- Photos - helps with consumer experience/appeal
- Phone
- URL
- About the business specialties
- Ensure the business has claimed their Yelp page. Direct the business to this page to claim their page if they haven't do so already, you'll need to append their biz\_id into this url structure: [https://biz.yelp.com/signup/\[\*\*business\_id\*\*\]/account](https://biz.yelp.com/signup/%5B**business_id**%5D/account)?

### 

How is ad text created for businesses who want to advertise with Yelp but have an unclaimed and/or unreviewed business page?

We’ll use the text in the about the business specialities field as the ad text, this can be updated via the data ingestion api. Custom ad text is not supported via API today.

### 

When specifying CTAs for enhanced profiles - is the same CTA used for mobile and desktop?

No, there are different CTAs for mobile vs. desktop. See our data ingestion documentation

### 

Can multiple campaigns/programs with overlapping budget cycles be enabled?

Yes, a business can have multiple CPC programs running at the same time.

### 

Does Yelp ever go over the target budget?

No, we could over deliver impressions but they won't be charged. The budget is the max we’d charge for that month.

### 

How are CPC budgets pro-rated?

Please request CPC pro-ration behavior via [partner-support@yelp.com](mailto:partner-support@yelp.com).

## 

Ad Management

### 

Can we terminate campaigns before the begin date?

Yes, doing so will invalidate the program\_id though if the campaign never started, meaning if you’re using the partner support API after this termination you won’t get this program\_id in any responses, and if you use that program\_id as an input, that request will fail.

### 

Can we get the info for terminated campaigns? I.e. If we want to create a concept of “favorite campaign settings”, will Yelp store the old campaign info in a way that we can query via api?

Yes, so long as the campaign actually started (same behavior as the above question).

### 

Can we change the monthly budget of an existing program?

Yes, you can change it to be effective immediately or at some future date.

### 

What is future\_budget\_date and how does it differ from start and end date?

Use this to change the budget at some date in the future. If you don't apply future\_budget\_date it updates budget immediately.

### 

Can we change the budget in a 30 day cycle?

Yes, you can change it whenever you want.

### 

If the start and end date are not at the beginning and end of a month does Yelp prorate the budget by the number of days?

Generally yes, exact proration behavior has some nuances. Request more details via [partner-support@yelp.com](mailto:partner-support@yelp.com).

### 

Does unused Yelp budget get rolled over to next month?

No.

### 

Can we apply some kind of name to Yelp campaigns?

There’s no field that Yelp accepts to do this, the program\_id represents that unique campaign on Yelp.

### 

Where should we go for troubleshooting, performance or optimization questions?

[partner-support@yelp.com](mailto:partner-support@yelp.com) should be used by partners, partner’s should handle escalations from their own customer directly.

### 

What happens when I change the fee period from CALENDAR\_MONTH to ROLLING\_MONTH?

You can’t change this once the program has started.

## 

Enhanced Profiles and CTAs

### 

What features come with Enhanced Profiles?

No competitor ads, sequencing of photos on the Yelp page, & call to action.

### 

Where can we find if a business has an enhanced profile?

There’s no explicit {Enhanced Profile: True/False} data point that we expose, but you can look for other signs to see if a location likely has a EP already.

- Purchases will fail if a program already exists, we'd suggest trying to purchase the profile as the first step, then if if fails you know a profile already exists.
- Enhanced Profiles come with Call to Action, look for CTA [here](https://docs.developer.yelp.com/docs/partner-support-api#business-info-api).
- This [request](https://docs.developer.yelp.com/docs/partner-support-api#program-list-api) will tell if the location is a current advertiser. If they're currently advertising it's more likely than not that they have an active EP.

### 

Is the enhanced profile independent of the CPC program?

Yes, via API they’re created and managed as 2 distinct programs aka not formally bundled.

### 

Do the enhanced profiles follow the same life cycle as PPC programs? Either calendar month or 30 day cycles?

No, once a profile is purchased it’s always on until it’s ended. The profile’s features will apply to all traffic (organic or paid). There’s no prorated billing for profile products.

### 

Do CTAs get automatically removed by Yelp?

Yes, via a nightly job, if the profile product is ended the CTA, which is a feature of that program, will also be removed.

## 

Billing & Account setup

### 

Is there a limit to how many times a location can add/remove an enhanced profile?

No, but only 1 profile can be active at a time.

### 

Will merchants be charged every time they upgrade to an enhanced profile within the same month? Ie. add, remove, add in the same month.

No, the location will only be billed for 1 profile in the month. Profile purchases are not prorated.

### 

Can credentials be shared for reporting purposes?

No, there’s distinct program ownership by parties. If the requesting party didn’t create the program, they won’t be able to view that program data.

### 

Can we set up api access such that Yelp bills the advertiser directly, but the advertiser can manage their Yelp ads from a third party advertising platform? i.e. customer inputs their own credentials into our platform so we can make the api requests on their behalf, but the customer is billed directly for the activity.

Yes, this use-case is supported.

## 

UTM Tracking parameters

### 

How can we include UTM parameters in URLs that are associated with the advertiser's CPC program?

Use LINK\_TRACKING via the program feature api 
Sending this request payload: {"LINK\_TRACKING": {"website": "source=yelpweb"}} 
results in “?source=yelpweb” appending to the end of the existing URL.

### 

How does link\_tracking in the program feature api compare to the URL set in the data ingestion api?

Setting the link tracking via the program feature api referenced above applies the specific link tracking parameters to traffic generated by your CPC program, the URL set via data ingestion API is the organic traffic URL.

### 

Can traffic be directed immediately to the merchant’s website within search? or do they need to navigate to the Yelp profile page first, then click through to the non-Yelp website?

The consumer can click through to the external website directly from the cpc ad in search. Setting the program feature api’s AD\_GOAL to WEBSITE\_CLICKS which will surface a cta that prompts consumers to visit the website.

### 

What URL will be used when specifying ad goal:website\_clicks?

If tracking parameters have been set by link\_tracking, we’ll use those, else we’ll use the default external url for the location

### 

Is there anywhere else we can apply tracking parameters?

Yes, tracking can be applied to website, menu\_url, or the CTA.

Q:Does link\_tracking capture organic and paid traffic or can we differentiate between paid traffic coming from the ad? 
The link\_traking feature would only apply the tracking parameters to consumer traffic attributed to a CPC program.

## 

Call Tracking

### 

What are the options to set call tracking numbers?

There are 2 different places to add a call tracking #:

- Location level- Applies to all traffic that reaches the Yelp page (paid and organic). Set via metered\_phone\_number in the data ingestion api
- Program level- applies to traffic that’s interacted with the specific cpc program. Set via program feature api call\_tracking.

## 

General targeting

### 

What do ad\_goals do?

Setting this will dictate the call to action that’s displayed:

- Get more phone calls - “Call business”
- Get more website clicks - “Visit website”
- Let yelp optimize- mix of both.

### 

Can ad\_ goals be changed mid-program?

Yes

### 

Can we serve ads only when the business is open?

Yes, this is done via the program feature API AD\_SCHEDULING. Make this API request to get current hours for a location.

## 

Geotargeting

### 

Are there cases where Yelp could target something different than the exact city/neighborhood input for the CLT program feature?

Yes we’ll normalize some of the inputs so we suggest logging our response to see where we’re targeting after your request. Some county/city names are ambiguous so this could have slight impacts to how we target your campaigns.

### 

How should we handle the following error: “One or more locations can not be geocoded. {list of geocodes provided}”

Remove the failing values and retry, postal-codes are the easiest to manage since that’s a finite list of exact expected values, where some towns/neighborhoods are a bit more ambiguous.

### 

Are there rules/restrictions for custom location targets? Ie. radius limit, business physical location, boundaries, etc

Yes: “List of up to 25 locations. These locations can be zip codes, cities, neighborhoods, counties or state names but must be within the US.”

### 

Can we set a custom radius?

Yes, via CUSTOM\_RADIUS\_TARGETING in program feature api.

### 

Can a CPC Program switch back to standard/default radius targeting after specifying custom location targets? By deleting the custom location targeting feature, or removing custom location targets, or both?

Yes, but can't have both active at the same time, setting one will delete the other.

### 

Does CLT specify additional locations to target? OR is it specifying the only locations to target?

Anything set via CLT will replace the default targeting. There are two options for geotargeting 1) service area 2) physical location (default). Default radius is based on category and density.

## 

Reporting

### 

Are ad driven page views tracked?

Not explicitly, billed clicks is the best proxy for this, though not an exact match.

### 

How can we distinguish between a bad input and data not available yet?

- If it’s misformatted, we’ll fail it
- If the dates fall out of supported range, we’ll fail it
- If still processing we’ll give you a “job not complete” message

### 

Where does the new day start for campaigns?

Midnight PST

### 

What’s the difference between delivered vs billed clicks?

Some Yelp campaigns overdeliver but we don’t bill for the overage: 
Billed clicks X cpc = ad spend

### 

When does a campaign incur billed\_clicks?

Any action attributed to the ad will result in a click.

### 

Does ad driven total call to action include request a quote?

No this only tracks CTAs for locations with EPs. RAQ is captured in messages\_to\_the\_business.

### 

What is an appearance vs impression? Is this a component of impressions?

Appearance is the number of times it showed in organic search.

Q:What are we calling an impression and what are we calling a click? 
Paid Search + appearance on competitor page = impressions. Click encapsulates all actions done by a consumer on Yelp against an ad.

### 

What time is yesterday’s reporting data available?

Business metrics 1pm, Ad Driven 10am (Usually)

## 

Partner Support API

### 

If you enter business ID’s will you get all campaigns back for that business?

Yes, all campaigns you created will be returned. Campaigns belonging to other parties won’t be exposed.

## 

Promos

### 

Who’s eligible for promo campaigns?

Only new advertisers are eligible to use promo codes.

### 

How do we identify promo campaigns?

A promo campaign and primary campaign should have the same start date. You should be able to identify the promo program off the input promo code too. I.e ABC6M150B creates a $150 promo budget & ABC6M200B creates a $200 budget.

### 

What happens if the promo code provided is not valid?

The primary campaign will be rejected if the promo code isn't applicable.

### 

Can users be given the chance to correct the promo code (or other issue Ie. budget amount) and re-submit after a failure?

Yes since we’ll fail the primary campaign, just retry immediately after with a different value for promotion\_code and make other applicable changes like budget etc.

### 

Will all errors/failures surface at the initial point of program creation? Are validity checks done post creation? For example, what happens if the budget is lowered below the minimum spend threshold for the promo campaigns.

Yes a promo campaign could end if the qualifying program loses eligibility, this is processed nightly on Yelp’s end.

### 

How are these program terminations communicated?

There’s no explicit errors since these actions are done by an automated job on our end, in these cases you’d see the campaign move into "program\_status": "INACTIVE" and the value of the promos "end\_date": would change from {start date + 6 months} to whatever date our automed job ended it.

### 

What other possible changes could happen to the campaigns post creation?

If the qualifying campaign’s budget is changed to below the promo threshold, the promo campaign is terminated. Increasing the budget does not generate a new higher promo budget campaign.

### 

Is the promo campaign automatically deleted when the primary campaign is deleted?

Yes, this happens via a nightly job that runs. The end date of the promo campaign will be updated to the same as the primary campaign.

### 

How should we recognize the promo campaign?

We suggest pulling unrecognized campaigns with the same start date as the primary campaign. If you see an active program come back with the same start date that you didn't explicitly create, its safe to assume that is the promo campaign.

### 

Any other indicators of the promo program?

The promo campaign will have the same start date as the qualifying/parent campaign but the end date will be 6 months later and end on the last day of the month. For example a promo campaign would have these dates, so you’d look for a program where the month of the end date is 6 later than the start: "start\_date": "2021-05-07" "end\_date": "2021-11-30" -> “11” is used as end\_month in the following bullet.

### 

Would we notice any other providers programs running on a location and cause us to misidentify the promo program?

No, credentials are tied to a payment account, therefore they will only pull campaigns created under your payment account.

### 

How to handle cases where different accounts on our end all use our same parent payment account. I.e. What if 2 different agencies on our end are buying advertising programs for the same location?

Identifying the promo program based on the same start date, knowing what budget to look for based on the input promo code, and that {start\_month + 6 = end\_month for the promo} will reliably identify only the promo campaign. Any program with a start date that’s later the parent/qualifying campaign wouldn’t be a promo campaign. Then if there was a previous campaign in the program list endpoint it would have to be 6 months or more prior. Promos are only available to those who haven’t advertised in the last 6 months.

### 

Will campaigns that are not active appear? Ie. past promo campaigns?

Only 1 promo program would be active on a listing at a time. So if you’re pulling programs via the program list endpoint, you could see older campaigns but they’d be inactive and you could differentiate based on their start and end date.

### 

What are the error messages Yelp will show when promo codes are invalid?

Here are the errors and reasons a promo code might fail:

- Promo code is invalid or doesn't exist: "message": "The promotion is unavailable. This promotional code is invalid.","code": "PROMOTION\_UNAVAILABLE"
- Business does not qualify - needs to be a new advertiser (hasn’t advertised with Yelp in the past 6 months). "message": "The promotion is unavailable. This promotion is restricted to businesses that are not advertising with Yelp.","code": "PROMOTION\_UNAVAILABLE"
- Budget was too small:"message": "Could not add program for businesses.","code": "COULD\_NOT\_ADD\_PROGRAM"

### 

Can advertisers change the promo code during the 6 months the promo campaign runs? Ie. Can an advertiser “downgrade or upgrade” their promo?

No. promo code must be chosen at the time of campaign creation.

### 

How are promo codes provisioned?

It’s a list of static codes on Yelps end, these can be hard coded on the partner’s end.

### 

How are promo campaigns reported on? Are these separate or aggregate data with the qualifying program?

Separate, identified with a unique program ID.

### 

What are examples of promo codes?

get $100 bonus CPC (First 6 months) with $300 monthly CPC purchase.

### 

Can you edit promo programs like any other?

Changing budget is not advised, but targeting parameters can be updated.

## 

API vs. Yelp UI

### 

If we launched ad programs via API, can we see and manage those in the biz.yelp.com UI?

Not necessarily, there’s additional steps that need to be taken so that any biz you launch advertising for shows up your biz.yelp.com account. We suggest only managing campaigns via one channel.

### 

Will the ability to view campaigns in the Yelp UI be based on credential privileges or will we be able to see all programs created via the API in the Yelp UI?

This is based on credentials. We need to purposefully grant access for each biz owner account (email address used to login to biz.yelp.com) to your account on Yelp's end. Generally speaking if you purchase an ad program via API, you probably won’t be able to see that via Yelp.com unless you’ve already claimed said location in your Yelp for business account.

Updated 11 months ago

---

Did this page help you?

Yes

No

Copy Page