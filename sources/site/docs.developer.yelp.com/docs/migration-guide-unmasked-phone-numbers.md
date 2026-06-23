# Source: https://docs.developer.yelp.com/docs/migration-guide-unmasked-phone-numbers

## 

Table of Contents

1. [Overview](https://docs.developer.yelp.com/docs/migration-guide-unmasked-phone-numbers#overview)
2. [Detailed Changes](https://docs.developer.yelp.com/docs/migration-guide-unmasked-phone-numbers#detailed-changes)
3. [Immediate Action Items](https://docs.developer.yelp.com/docs/migration-guide-unmasked-phone-numbers#immediate-action-items)
4. [Long-Term Recommendations](https://docs.developer.yelp.com/docs/migration-guide-unmasked-phone-numbers#long-term-recommendations)
5. [What's Not Changing](https://docs.developer.yelp.com/docs/migration-guide-unmasked-phone-numbers#whats-not-changing)
6. [Next Steps for Your Team](https://docs.developer.yelp.com/docs/migration-guide-unmasked-phone-numbers#next-steps-for-your-team)
7. [FAQ](https://docs.developer.yelp.com/docs/migration-guide-unmasked-phone-numbers#faq)
8. [Example Response](https://docs.developer.yelp.com/docs/migration-guide-unmasked-phone-numbers#example-response)

 

## 

Overview

**What is changing?**

- Starting **April 16, 2026**, new leads in the Yelp Leads API will provide the consumer’s real, unmasked phone number when available.
- For leads generated **after April 16, 2026**, a new `phone_number` field will appear for eligible consumers: specifically, if the consumer opted in to be contacted by phone **on or after August 1, 2025**, their real phone number will be provided in this new field. Leads that did not opt-in to sharing their number will still not populate this field.
- Beginning April 16, 2026, the `temporary_phone_number` field will contain the real, unmasked phone number for all new leads, and its expiry will be set far in the future. For leads generated prior to April 16, 2026, the `temporary_phone_number` field will continue to contain the previously assigned temporary (masked) number, which will expire as originally scheduled.

---

## 

Detailed Changes

| Lead Creation Date | `phone_number` field | `temporary_phone_number` field | `temporary_phone_number_expiry` |
| --- | --- | --- | --- |
| Before April 16, 2026 | _Not present_ | Masked number (expires in 30 days) | Expiry 30 days after lead creation |
| On or after April 16, 2026 | Real, unmasked number (no expiry) | Real, unmasked number (for backward compatibility) | Expiry date far in the future |

 

> ## 🚧
> 
> Availability of Real Phone Numbers
> 
> For leads generated before April 16, 2026, real phone numbers will be available **as long as the consumer opted in to be contacted by phone on or after August 1, 2025.**
> 
> As a reminder, consumers can opt out of sharing phone number at any time. If this happens, you will receive a webhook notification of type "CONSUMER\_PHONE\_NUMBER\_OPT\_OUT\_EVENT". See [documentation](https://docs.developer.yelp.com/docs/leads-webhooks#masked-phone-number-opt-in-status-event-webhooks) for more details.

---

## 

Immediate Action Items

There is **no urgent work required**, but we advise teams to:

1. **Identify Usage**
 
 - Check if your application or validation layers are using or enforcing logic on the `temporary_phone_number_expiry` field.
 - If you are using this field for any workflow, **flag** this for review.
 - If not, no integration updates are required.
2. **Validate Your Integration**
 
 - Ensure your systems can accept and process `temporary_phone_number_expiry` values set in the far future (e.g., year 2099).
 - Confirm that your integration logic does not fail or throw errors for very distant expiry dates.

---

## 

Long-Term Recommendations

- **Plan for Migration to `phone_number`:**
 
 - Change your integration to reference the new `phone_number` field (unmasked, persistent) for leads created on or after April 16, 2026.
 - Remove usage of `temporary_phone_number`. Plan for possible future deprecation (no date has been set).
- **Remove Dependence on `temporary_phone_number_expiry`:**
 
 - Review any business logic tied to lead phone number expiration.
 - If you use expiry for any workflows, transition to using the new `phone_number` field where relevant.

---

## 

What’s Not Changing

- **No Data Loss:** No fields are being removed at this time.
- **Backward Compatibility:** The `temporary_phone_number` field will remain populated with the real number for all new leads, so integrations relying solely on this field will continue to work.
- **No Immediate Required Changes:**
 - The only risk is if your system rejects or mishandles expiry dates set far in the future.

---

## 

Next Steps for Your Team

1. Confirm your systems allow far future dates in `temporary_phone_number_expiry`.
2. Identify any processes relying on the expiry field and form a migration plan to use `phone_number` over `temporary_phone_number`.
3. Communicate to technical stakeholders that:
 - **No urgent migration is needed**
 - New leads starting April 16, 2026, will have unmasked phone numbers in the payload.

---

## 

FAQs

**Q: Do I need to update my integration immediately?** 
A: _No. Just check your system doesn’t fail or throw errors with far future expiry dates. Logic changes can be planned for a later release._

**Q: Will the `temporary_phone_number` or `temporary_phone_number_expiry` fields be removed soon?** 
A: _No plans to remove these fields yet, but migrating to `phone_number` is best practice._

**Q: What might go wrong if I do nothing?** 
A: _If your integration strictly enforces expiry date ranges, you may see validation errors or rejected data. Double-check your logic._

**Q: Does Yelp still require One-Time-Password (OTP) verification for phone sharing opt-in?** 
A: Yes. Newly opted-in customers will need to complete OTP opt-in. Please listen for `CONSUMER_PHONE_NUMBER_OPT_IN_EVENT` webhook notifications and re-pull the lead if the consumer opts in after they submit their project.

**Q: What if I use Zapier to integrate with Yelp Leads?** 
A: The `phone_number` field will not be available until the next Yelp Leads version release on Zapier. In the meantime, `temporary_phone_number` will contain the consumer phone number for leads generated after April 16, 2026.

 

---

## 

Example Response

JSON

`{   "business_id": "SNa1ugk6DNIuvIPu8-AiGA",   "id": "xKgWk-XoFWBQucET-xr-hw",   "conversation_id": "49-Acxgj7-0C5SAMG_J7Dg",   "temporary_email_address": "gbtUf6u0X36pKPqRzg7iXV@messaging.yelp.com",   "temporary_email_address_expiry": "2022-01-02T03:04:05+00:00",   "phone_number": "+14165551234", <--- new field   "temporary_phone_number": "+14165551234",   "temporary_phone_number_expiry": "2099-12-31T00:00:00+00:00",   "time_created": "2024-08-23T20:56:27+00:00",   "last_event_time": "2024-08-26T18:17:20+00:00",   "user": {     "display_name": "Austin D."   },   "project": {     "survey_answers": [       {         "question_text": "How many bathtubs need repairs?",         "answer_text": [           "1"         ]       }       // ...additional survey answers     ]   } }`

 

---

## 

Need Additional Help?

Contact your Yelp technical representative or support team with questions, or for assistance reviewing your integration.

---

Updated 2 months ago

---

Did this page help you?

Yes

No

Copy Page