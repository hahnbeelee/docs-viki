# Source: https://docs.developer.yelp.com/docs/leads-webhooks

> ## 📘
> 
> Get started with webhooks here
> 
> This page described the details of the Leads API Webhooks. For the general webhook setup please see [Webhooks](https://docs.developer.yelp.com/docs/webhooks) first.

If you'd like to receive lead webhook notifications, you first need to subscribe to the business ids that you'd like notifications for [here](https://docs.developer.yelp.com/reference/create_business_subscriptions) using event `"subscription_types": ["WEBHOOK"]`. You will only receive webhooks for locations that you're subscribed to. **Syncing your business subscriptions is an ongoing process**: We recommend you do it at _least once every 24 hours_.

# 

Format of Webhook Messages

A Webhook POST request body is a JSON object with the following format:

## 

Full Webhook Payload

Webhooks will include a timestamp, a "business" object and data related to the lead. 
The payload may slightly differ depending on the event type we're dealing with.

### 

Lead Interaction Event Webhook Payload

You will receive this type of webhook if a new lead is created, or a new interaction is done in an existing lead.

JSON

`{   // Yelp processing time   "time": "2022-06-09T09:41:14+00:00",   // always business   "object": "business",   "data": {     // Yelp Business ID     "id": "SoVHhx7Hel_XX0DKCLp72Q",     // updates is an array of updates/webhook events.      // For Lead Interaction Event Webhooks this will always be 1 entry with the event_type NEW_EVENT.      // Other Yelp Webhooks may include a different number of updates with different event types.      "updates": [       {         // The event type.         // For Lead Interaction Event webhooks this will always be NEW_EVENT.         "event_type": "NEW_EVENT",         // The unique ID of this event         "event_id": "IsKxQAYZNqCjvRRmNoiCUw",         // The ID of the lead this event happened on         "lead_id": "TbvEUYEi02cmSBmqCjQbkg",         // The time this event was created by the user         "interaction_time": "2022-06-09T09:41:13+00:00"       }     ]   } }`

### 

Phone Number Opt-In Status Event Webhooks

> ## 🚧
> 
> Masked Phone Numbers
> 
> Masked phone numbers on Yelp Leads have been deprecated as of April 16, 2026. If you're looking for more information on this, please refer to the [migration guide](https://docs.developer.yelp.com/docs/migration-guide-unmasked-phone-numbers).

You will receive this type of webhook when the Lead Submitter opts into being contacted by phone and finished the verification process. If you receive an opt-in webhook, you should call the [Get Lead Endpoint](https://docs.developer.yelp.com/reference/get-lead) to read the consumer's phone number and update your lead record accordingly.

json

`{   // Yelp processing time   "time": "2022-06-09T09:41:14+00:00",   // always business   "object": "business",   "data": {     // Yelp Business ID     "id": "SoVHhx7Hel_XX0DKCLp72Q",     // updates is an array of updates/webhook events.     // Similar to Lead Interaction Event webhooks, this will only contain 1 entry.     "updates": [       {         // The event type.         // For Phone Number Opt-In Status Event webhooks, this will always be one of:         // CONSUMER_PHONE_NUMBER_OPT_IN_EVENT         // CONSUMER_PHONE_NUMBER_OPT_OUT_EVENT         "event_type": "CONSUMER_PHONE_NUMBER_OPT_IN_EVENT",         // The ID of the lead this event happened on         "lead_id": "TbvEUYEi02cmSBmqCjQbkg"             }     ]   } }`

# 

Webhook delivery

## 

What interactions on Yelp trigger a Webhook?

Once the webhook setup is completed, you'll be notified when:

- A new lead is created
- A new interaction is done in an existing lead, for example a new message is sent.
- \[If enabled for your account\] The submitting consumer user is opted into sharing phone number at the time of lead submission.
- \[If enabled for your account\] The submitting consumer user opts in or out of sharing phone number after lead submission.

## 

When are webhooks sent?

Webhooks are sent whenever an event starts showing on Yelp for Business. This can be significantly later than when the user interacted on Yelp in some cases, see below.

Most webhooks are sent out within a minute or less after showing up on Yelp. While we don't provide any guarantees, our aim is to deliver 99% of webhooks within 100 seconds.

The same applies to phone number opt-in status webhooks, if they are enabled for your account. We send these webhooks for up to 2 weeks old leads.

## 

Why is there a delay between interaction\_time and when the webhook is sent?

Some events are not eligible to be shown on Yelp immediately. The two most common case are:

**Spam:** Yelp may quarantine messages for some time (minutes, hours, days). Webhooks are sent whenever a message is also eligible to be shown on Yelp, which may differ significantly from the timestamps in a message.

**Events displayed delayed on Yelp:** Some kind of events may show a significant delay between when the user interacted with a Lead and when the interaction is shown on Yelp and you are notified. This is intentional.

One example for this are consumer hire resolution events where a Yelp User marks your or another business's Lead as hired, you'll receive a message text such as `"Automatic message:\\nUser U. has indicated they have booked another business for this job."`.

## 

If the business responds directly on Yelp, will I get notified?

Yelp Webhook notifies you of all interactions on a Lead no matter the source. This means you will get notified for interactions on Yelp and through the API from both consumer and business users (including events you create yourself).

## 

Why isn't the message text in the webhook?

Yelp Webhook currently does not return full events. You can obtain the lead\_id in the Webhook, and use the [Get Lead Events Endpoint](https://docs.developer.yelp.com/reference/get-lead-events) to get the full event content (message text, attachments or other).

## 

Can we add your IP addresses to an allow list to verify the requests are coming from Yelp?

Yes, we can share the list of IPs that will send webhook payloads.

# 

FAQs

Please see also the Leads API FAQs:

[![Leads API FAQs](https://files.readme.io/08035d8-small-yelp-dev-portal.png)\\ \\ ![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Leads API FAQs](https://docs.developer.yelp.com/docs/leads-api-faqs)

Updated 2 months ago

---

Did this page help you?

Yes

No

Copy Page