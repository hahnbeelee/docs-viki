# Source: https://docs.developer.yelp.com/docs/lead-interaction

So you've received a lead through Yelp! What can you do with it?

Yelp Leads allow you to interact with a Lead Submitter in one of four ways inside the Yelp ecosystem:

- By messaging through the [Yelp Inbox](https://biz.yelp.com/support-center/Yelp_Business_Page/Messages_Notifications/How-do-I-respond-to-a-message-from-my-business-account/en-US), which is your Yelp Business Account messaging interface.
- By messaging through [Leads API Events](https://docs.developer.yelp.com/reference/write-lead-event).
- By messaging, using a Yelp-generated masked email address, received through the Leads API.
- By call/messaging, using a consumer's phone number, received through the Leads API

> ## 📘
> 
> Messaging through a Yelp Lead
> 
> Whether you're communicating with a customer via the Yelp user interface, the Leads API, or masked email, all messages are **part of the same unified chat thread**. Regardless of the channel, the conversation is consolidated into a single thread for consistency. As such, be sure to stick to one method of communication to avoid confusion.

You can find a consumer user's phone number and temporary (masked) email address by calling the [Get Lead](https://docs.developer.yelp.com/reference/get-lead) endpoint. See the example API response below:

JSON

`{   "business_id": "SNa1ugk6DNIuvIPu8-AiGA",   "id": "xKgWk-XoFWBQucET-xr-hw",   "conversation_id": "49-Acxgj7-0C5SAMG_J7Dg",   "temporary_email_address": "gbtUf6u0X36pKPqRzg7iXV@messaging.yelp.com",   "temporary_email_address_expiry": "2022-01-02T03:04:05+00:00",   "phone_number": "+14165551234",   "temporary_phone_number": "+14165551234",   "temporary_phone_number_expiry": "2099-12-31T00:00:00+00:00",   "time_created": "2024-08-23T20:56:27+00:00",   "last_event_time": "2024-08-26T18:17:20+00:00",   "user": {     "display_name": "Austin D."   },   "project": {     "survey_answers": [       {         "question_text": "How many bathtubs need repairs?",         "answer_text": [           "1"         ]       }       // ...additional survey answers     ]   } }`

 

> ## 📘
> 
> Consumer Phone Numbers
> 
> **Starting April 16, 2026**, unmasked consumer phone numbers are available via the new phone\_number field for all Leads API clients. The legacy `temporary_phone_number` field continues to be populated for backward compatibility.
> 
> **For leads created and fetched before April 16, 2026,**
> 
> - The temporary\_phone\_number field contains a masked number that expires after 30 days.
> 
> **For leads fetched after April 16, 2026**,
> 
> - `phone_number`contains contains the unmasked consumer number if available.
> - `temporary_phone_number` is populated with the same value for backward compatibility. This temporary phone number will expire after 30 days.
> - Clients should migrate to `phone_number`as soon as possible. The `temporary_phone_number` field **may be deprecated in a future release**.
> - Please refer to this [migration documentation](https://docs.developer.yelp.com/docs/migration-guide-unmasked-phone-numbers) for a comprehensive guide of next steps.

## 

How to Manage Phone Numbers

**Starting April 16, 2026, these phone numbers are provided unmasked via the new phone\_number field.**

The phone number of the Lead Submitter will only be passed via our [Get Lead](https://docs.developer.yelp.com/reference/get-lead) endpoint. It is only available **if the Lead Submitter opts-in to be communicated with via phone/SMS**.

If you plan to use this field, we recommend calling the [Get Lead](https://docs.developer.yelp.com/reference/get-lead) endpoint after receiving the [Phone Number Opt-In Status event webhook](https://docs.developer.yelp.com/docs/leads-webhooks#masked-phone-number-opt-in-status-event-webhooks) .

Due to the phone number verification process on the consumer side, phone numbers may not be immediately available upon your initial receipt of a lead. Look out for a webhook event with `"event_type":"CONSUMER_PHONE_NUMBER_OPT_IN_EVENT"` if you are looking to process leads that include a phone number.

Please note that at the time of writing, about 40% of Yelp Leads include a phone number. Keep this in mind as you design your integration.

> ## ❗️
> 
> Masked Phone Numbers Deprecated April 16, 2026
> 
> The information below related to masked phone numbers is no longer relevant for phone number access in leads generated after April 16, 2026. This documentation is retained for reference only and is no longer applicable to current or future integrations.

### 

Allow-Listing Outbound Phone Numbers

Before using a Yelp masked phone number, you must first register the phone number(s) you plan to use for outbound communication. This security measure ensures that all communication sent to customers via Yelp originates from a verified number associated with your business.

Then, you will need to provide **a comprehensive list of phone numbers you use to outbound dial** Yelp phone leads so Yelp can add them to your businesses' allowlist. Additionally, share **the best phone number where the Lead Submitter can contact you directly**. This step is a requirement of receiving and using masked phone numbers from a Yelp Lead. You can provide your phone number(s) to your Yelp account representative or by filling out this [form](https://docs.google.com/forms/d/e/1FAIpQLSdxLoxhvz4pJK-Hyn4KBJjH9WkWGG9PNf9_XE_ds85LVz4WqA/viewform?usp=sharing&ouid=100848218112025059765).

Allow-listing outbound phone numbers is only required for phone masking configurations created before April 16, 2026. Going forward, consumer phone numbers are provided directly and can be dialed without masking configuration.

> ## 🚧
> 
> Note to Channel Partners
> 
> Because you may be managing multiple clients leveraging multiple outbound call-lines, it may not be feasible for you to maintain an updated list of all of your clients’ outbound phone numbers and therefore **access to this field may not be available**.

### 

SMS Exchanges

You can send outbound SMS texts to the masked phone number, but **two-way SMS is not currently supported**. Any replies from the Lead Submitter are accessible in the Yelp Inbox of your Business Owner Account or via the Leads API Events feed.

---

## 

How to Manage Temporary/Masked Email Address

We mask email addresses to limit the exposure of PII between users, businesses, and third-party systems. While phone numbers are currently shared unmasked, emails use a proxy masked address so the real address is not revealed.

The Temporary/Masked Email Address of the Lead Submitter will always be passed via our [Get Lead](https://docs.developer.yelp.com/reference/get-lead) endpoint and can be used for multiple communications for up to 30 days until it expires.

### 

Best Practice

While you can engage with leads using the Yelp Inbox or the Leads API, you also have the option to contact them directly via email. Communicating with customers through their masked email address is relatively simple. If you choose to take this approach, please follow the best practices outlined below:

- Stick with plain text when formatting your email response. Including formatting or URLs in the email could affect our system's ability to correctly parse the email body. This means:
 - No HTML or rich text formatting
 - No embedded links or full URLs
 - If you would prefer to include a URL, we would recommend using a URL shortener such as Bitly, TinyURL, or Short URL. These types of URLs work well with the email parser.
 - No images or attachments

**Correct Usage:** Here is an example of an email body formatted correctly:

`Thank you for your interest in our services. We're excited to help you with your project! Please feel free to reach out if you have any more questions. To learn more about our team, check out https://bit.ly/3XyzAbC!   Best regards,  The Team` 

**Incorrect Usage:** The following example includes common mistakes that should be avoided:

`Thank you for your interest in our services. [Bold]We're excited to help you with your project![/Bold]   • Please feel free to reach out if you have any more questions.  • To learn more about our team, check out https://yelp.com!  Best regards,  The Team` 

- In the incorrect example, the email includes rich text formatting as well as a full URL.

 

## 

Yelp Inbox

If you're interested in managing Yelp Leads communication directly through your Business Account Yelp Inbox, you can construct a link to a lead-specific chat using the URL template below. The `business_id` and `lead_id` needed to construct this URL can be found in the GET Lead response of the API.

`https://biz.yelp.com/leads_center/{{business_ID}}/leads/{{leads_ID}}` 

Updated 2 months ago

---

Did this page help you?

Yes

No

Copy Page