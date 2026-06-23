# Source: https://docs.developer.yelp.com/docs/leads-api-zapier-integration

> ## 📘
> 
> Looking for guidance from our team?
> 
> You can request support on your Yelp Leads API Zapier integration [here](https://forms.clickup.com/9017360855/f/8cqm0eq-6337/MRK5WOLTJMNA5GW5FV).

> ## ☝️
> 
> Curious about unmasked phone numbers?
> 
> Check out our migration guide [here](https://docs.developer.yelp.com/docs/migration-guide-unmasked-phone-numbers).
> 
> The `phone_number` field will not be available until the next Yelp Leads version release on Zapier. In the meantime, `temporary_phone_number` will contain the consumer phone number for leads generated after April 16, 2026.

[Zapier](https://zapier.com/apps/yelp-leads/integrations) lets you connect different apps and automate tasks between them—**no coding needed**. For local businesses using Yelp Leads, Zapier can automatically send new leads from Yelp to your email, CRM, or other tools, helping you follow up faster and stay organized. This means easy setup, less manual work, and a smoother lead generation workflow.

### 

Table of Contents

- [How it Works](https://docs.developer.yelp.com/docs/leads-api-zapier-integration#how-it-works)
- [Setup Guide](https://docs.developer.yelp.com/docs/leads-api-zapier-integration#setup-guide)
 - [Getting Started](https://docs.developer.yelp.com/docs/leads-api-zapier-integration#getting-started)
 - [Authentication](https://docs.developer.yelp.com/docs/leads-api-zapier-integration#authentication)
 - [Lead Data](https://docs.developer.yelp.com/docs/leads-api-zapier-integration#lead-data)
 - [Contact Data](https://docs.developer.yelp.com/docs/leads-api-zapier-integration#contact-data)
 - [Project Information](https://docs.developer.yelp.com/docs/leads-api-zapier-integration#project-information)
 - [Two-Way Communication](https://docs.developer.yelp.com/docs/leads-api-zapier-integration#two-way-communication)
- [Example Zap Workflows](https://docs.developer.yelp.com/docs/leads-api-zapier-integration#example-zap-workflows)
- [FAQ](https://docs.developer.yelp.com/docs/leads-api-zapier-integration#faq)

### 

Prerequisites

- You have a [Yelp Business Account](https://biz.yelp.com/support-center/Yelp_Business_Page/Getting_Started/How-do-I-log-in-to-my-Yelp-Business-Account/en-US).
- You have [Yelp RAQ (Request-a-Quote)](https://business.yelp.com/brands/ad-solutions/request-a-quote/) enabled.
- You have a [Zapier](https://zapier.com/apps/yelp-leads/integrations) account.
- You have an idea of an app that you want to connect the Yelp Leads Zapier app to.
 - e.g. ServiceTitan, Google Sheets, Salesforce, Hubspot, Slack, Discord

### 

Key Terms

- **Zap**: _A Zapier workflow. A Zap consists of one Trigger and one or more subsequent Actions._
 - e.g. _When a new Yelp Lead is generated (Trigger), a new row is created in Google Sheets (Action)._
- **Trigger**: _The starting point for a Zap. A Trigger is typically some sort of listener that waits on a specific event in your target app._
 - e.g. _When a new message is received on a Yelp Lead._
- **Action**: _A middle or final step in a Zap. An Action is a step that occurs after a Trigger or after another Action._
 - e.g. _Send the Yelp Lead data to Salesforce._

![The anatomy of a Zap](https://files.readme.io/a84955f67733dc4397a2f90d56f1759b0d29bab9bb8db8af1983e57eaf685e3f-image.png)

The anatomy of a Zap

 

---

## 

How it Works

Zapier supports integrations with over 7,000 apps, so no matter how your lead generation pipeline is set up, the [Yelp Leads Zapier app](https://zapier.com/apps/yelp-leads/integrations) offers nearly unlimited automation options.

With a Yelp Leads Zapier **trigger**, you can automatically start your lead conversion workflow as soon as a new lead comes in via the Yelp Leads API.

With a Yelp Leads Zapier **action**, you can automatically update or reply to a Yelp Lead thread in response to events from any other connected app.

### 

Yelp Leads Triggers and Actions

#### 

Triggers

| Trigger | Description |
| --- | --- |
| New Lead | Triggers when a new lead is created. Includes all lead details. |
| New Consumer Message | Triggers when a new message is received from the consumer. Includes message text, consumer name, business ID, etc. |
| New Business Message | Triggers when a new message is sent from the business. |
| Phone Availability | Triggers when a phone number is available. |

#### 

Actions

| Action | Description |
| --- | --- |
| Create Message | Creates a new message for a lead (e.g., responding to a lead or message with a text response). |
| Mark Lead as Replied | Marks a lead as replied (by phone or email). Useful if you have already followed up with the lead outside of Yelp. |
| Mark Lead Message as Read | Marks an existing lead message and all messages before that as read. |
| Get Business Details | Retrieves business details. Input a business ID and get details like business name, address, URL etc |
| Get Lead Details | Retrieve information such as name and temporary email from the lead. |

 

---

## 

Setup Guide

### 

Getting Started

Create a new Zap in Zapier. Click on the **Trigger** step.

![](https://files.readme.io/e95e35ffd7ca0b7a72eed12949251e608edd780f042aed708f60b60b52c95bd4-image.png)

Search for "Yelp" in the application gallery and select **Yelp Leads**.

![](https://files.readme.io/4384b75b2ba551ef694884dc024381c051a0035e101d876ebdcd1eca445ced5e-image.png)

In the input field **Trigger event**, select **New Lead**. This is the trigger type we will be using for the sake of demonstration. Once you are familiar with the Zapier workflow, feel free to experiment with the others!

By selecting **New Lead** as the trigger step, we are setting up a Zap to listen for a new lead on your Yelp business account. Upon notification of a new lead, the Zap will trigger a subsequent action.

![](https://files.readme.io/a8ac3dacde7663dfbf309542a13bb39b9bc62156961fc35e677f13fd3f851fa2-image.png) 

### 

Authentication

You’ll need to sign in to your Yelp Business Account when setting up Yelp Leads triggers and actions in Zapier. Once authenticated, your Zapier account will remain connected to your Yelp Business Account. It's worth noting that you can have multiple Yelp Business Accounts associated with your Zapier account.

![Step 1: Adding your Yelp Business Owner Account to your Zap](https://files.readme.io/823785f71a7b54cebe9e27d3a4497fe59a150f844d88b092b7af959a15a0c18d-image.png)

Step 1: Adding your Yelp Business Owner Account to your Zap

![Step 2: Authorizing the connection between Yelp and Zapier](https://files.readme.io/43f4ffc08ca8588ef66c43b771f881e893a4e3c150f79ebbf98d8e428a737036-image.png)

Step 2: Authorizing the connection between Yelp and Zapier

 

### 

Lead Data

To complete setting up the trigger, click through the rest of the setup workflow. Upon testing this step, you will see a test record populate. This test record should represent an existing lead on your Yelp business account.

**Please note that certain triggers like New Consumer Message and New Business Message return dummy data and may not represent the data you would like to test with**. If you would like to test with lead data specific to your business, refer to the callout at the end of this section.

Go ahead and complete this step by selecting the test data and clicking "continue" at the bottom of the panel.

![](https://files.readme.io/81eb8b489143a94e4bf29248d28911fe322e7a7bc2c9dadd0d38c2c1e74c56ac-image.png)

Now that you've set up a trigger and authorized access to your Yelp business account, you are ready to start pulling lead data from Yelp and preparing the data to be sent to a downstream application. When prompted, select your downstream app of choice. See the section titled [Example Zap Workflows](https://docs.developer.yelp.com/docs/leads-api-zapier-integration#example-zap-workflows) further down in this article to get an idea of your options.

As a basic example, we will explore what it looks like to take Yelp Lead data and automatically send it into a Google Sheet. After configuring your Google Sheets action step, you'll be able to map Yelp Lead fields from the previous step into your Google sheet. This means that when a new lead comes in, this Zap will automatically collect the lead data and input it into a new row on your spreadsheet.

![](https://files.readme.io/2e72ff434852ac67e9da7618ae5f58183bf63ff653c1770150016bff8acc156e-image.png) 

> ## 🚧
> 
> Testing With Non-Dummy Data
> 
> If you want to test out this workflow with your own test data, see [this article](https://docs.developer.yelp.com/docs/leads-zapier-integration-access-error-when-testing). Read this article if you're seeing a **“You don’t have access to this business.”** error.

### 

Contact Data

If you are planning on leveraging contact data from your Lead Submitters in your Zapier integration, please be sure to read [this article](https://docs.developer.yelp.com/docs/lead-interaction). Additionally, be sure to set up a [**Phone Availability**](https://docs.developer.yelp.com/docs/leads-api-zapier-integration#lead-submitter-phone-verification) Zap trigger if you are planning on using phone numbers.

In summary:

- Yelp provides consumer contact information through the Leads API. Starting April 16, 2026, real (unmasked) phone numbers are available via the phone\_number field with no expiration. The temporary\_phone\_number and expiry fields remain populated for backward compatibility.
- Email will always be provided for a lead. Phone numbers are available for leads where the consumer opted in as long as they opted in on or after August 2025.
- Lead Submitters must opt in and verify their phone number. The Lead Submitter may not provide a phone number at all. Without the opt-in, the lead will not include a phone number. The opt-in process takes at least a couple minutes. As such, the initial lead may not include a phone number. That's why you will need the **Phone Availability** trigger to notify you when one is available.
- If a Lead Submitter has already opted in via another RAQ flow, then the phone number will appear in the initial new lead payload. Note that they also have the ability to opt out retroactively.
- On your end, the masked email functions much like a regular email address and can be used with any email client. On the consumer’s end, any message you send to the masked email will be routed to their Yelp Inbox, triggering email, push, and SMS notifications that share the content of your message.
- Messages can be sent directly via email, through the API, or through the Yelp Inbox.

If available, you will be able to access these contact fields as well as their expiration dates through the Yelp Leads payloads in Zapier.

![](https://files.readme.io/ffea4b662796161fc70bcaecbe96055ce279ad42e4506622651584ae6a9fca31-image.png)

#### 

Enabling Masked Phone Numbers

> ## ❗️
> 
> Masked Phone Numbers Deprecated April 16, 2026
> 
> The information below related to masked phone numbers is no longer relevant for phone number access in leads generated after April 16, 2026. This documentation is retained for reference only and is no longer applicable to current or future integrations.

Phone masking configuration (inbound/outbound registration) is only required for legacy masked phone numbers from before April 16, 2026. Unmasked phone numbers are provided directly and do not require phone masking setup. The below steps are deprecated as of April 16, 2026:

Before using a Yelp masked phone number, you must first register the phone number(s) you plan to use for outbound communication. This security measure ensures that all communication sent to customers via Yelp originates from a verified number associated with your business.

To enable masked phone numbers on your account, you will need to submit [this form](https://docs.google.com/forms/d/e/1FAIpQLSdxLoxhvz4pJK-Hyn4KBJjH9WkWGG9PNf9_XE_ds85LVz4WqA/viewform). In it, you will provide the following:

1. An centralized phone number that can receive inbound calls.
2. At least one phone number that will be used to make outbound calls. These will need to be allowlisted.

Starting April 16, 2026, unmasked phone numbers are enabled for all Leads API clients. The phone\_number field will appear in your Zapier payloads for eligible leads. No account-level enablement is required for unmasked numbers. Please reach out to [zapier-support@yelp.com](mailto:zapier-support@yelp.com) if you have questions.

> ## 🚧
> 
> Note to Channel Partners
> 
> Because you may be managing multiple clients leveraging multiple outbound call-lines, it may not be feasible for you to maintain an updated list of all of your clients’ outbound phone numbers and therefore **access to this field may not be available**.

#### 

Lead Submitter Phone Verification

When a Lead Submitter opts in to allow phone contact, they first need to verify their phone number. This process can take a few minutes so it's very possible the lead will appear as though the consumer didn't provide a phone number. To catch delayed available phone numbers, you can rely on the **Phone Availability** trigger.

![](https://files.readme.io/ccf3a1c1e56721205a5ede1c219a2456059ef90a0b8dbfcc416b793fc39e10e7-image.png) 

### 

Project Information

Project details from the RAQ survey will be populated in the Yelp Leads payloads on Zapier. Project survey questions and answers can be found as individual fields.

![](https://files.readme.io/4aec6fe8278a65aca28ba23d20ff4b3d00856ee9fc15bcce9b0c46742aaa8b27-image.png)

You'll also find project survey questions and answers aggregated and formatted into one field. Additionally, attachments will be included and accessible via URL.

![](https://files.readme.io/736f03ef5cb9aa19c3b5d75c5540973cdcf5113368fcad21784dd000edd8141e-image.png) 

### 

Two-Way Communication

The Yelp Inbox in your Business Account is an excellent way to connect directly with Lead Submitters, allowing you to have one-on-one conversations with potential customers right from the platform. However, the Yelp Leads Zapier app takes things a step further by letting you automate and manage these communications without needing to manually use the Yelp Inbox UI.

With the Zapier integration, you can trigger actions based on Yelp Leads messaging events—giving you a seamless entry point into conversations with your prospects. You can easily connect Yelp Leads messaging to your favorite messaging platform, or chatbot (as long as it supports Zapier), allowing you to plug Yelp Lead messaging directly into your existing workflows.

Establishing two-way communication through your Yelp Leads Zapier integration can meaningfully enhance your automated lead generation and nurturing process. With the right setup, your team—or your chatbot—can respond quickly and efficiently to Yelp Leads, improving response time and increasing your chances of converting prospects into customers.

We're going to explore two basic Yelp Leads Zapier workflows that will allow for two-way communication.

#### 

Starting a Conversation With a New Lead

Upon receipt of a lead, you can generate a follow-up automated message or you can send it to your preferred communication channel to be handled by the business manually. You can do so using a combination of the **New Lead** trigger and the **Create Message** action. The high level workflow is described in further detail below:

1. _Notification of a new lead_: The **New Lead** trigger will kick off once a new lead comes in for your business.
2. _Passing lead qualification/project information to your preferred messaging channel_: You can pass the lead information into a chatbot or a preferred communication platform.
3. _Sending a first response_: If using a chatbot, an auto-response can be generated and sent back to the Lead Submitter using the **Create Message** action.

![Left: A chatbot processes a lead and provides an auto-reponse to the Lead Submitter. 
Right: A new lead is sent directly to Discord, a messaging platform.](https://files.readme.io/18d3100f7a41effcafa4faa1a3dfe69c6c285244cebff857e14630c08fdadb0a-image.png)

Left: A chatbot processes a lead and provides an auto-response to the Lead Submitter. 
Right: A new lead is sent directly to Discord, a messaging platform.

#### 

Continuing the Conversation

If you're looking to facilitate two-way communication with your prospects and customers through the Zapier integration, you can leverage the **New Consumer Message** trigger and the **New Business Message** trigger alongside the **Create Message** action to do so. This can get a bit more complicated, but some example workflows are described below:

##### 

Listening for New Messages from the Lead Submitter (Consumer)

> ## 🚧
> 
> Choosing the Correct Message Trigger
> 
> Yelp's Zapier application offers two message triggers: **New Consumer Message** for incoming messages from leads, and **New Business Message** for your business’s responses.
> 
> Use **New Consumer Message** to automate actions or replies when a lead contacts you. 
> Use **New Business Message** to track your business’s replies.

1. _Notification of a new message_: The **New Consumer Message** trigger will kick off once a new message event from the Lead Submitter occurs on the Lead.
2. _Pass the message to a communication channel_: You can send the Lead Submitter's message directly to your messaging platform (Slack, Discord, Google Chat, etc.).
3. _Store the conversation ID and Yelp Lead ID_ In order to successfully tie the messaging conversation and the Yelp Lead together, you will need to store these identifiers somewhere that can be referenced later.

![](https://files.readme.io/2017a9921437a44a9e8b4e185ebba3f51640fba2b720784d88a52fb99b39d3e0-image.png) 

##### 

Listening for New Messages from the Business on your Messaging Platform

1. _Business sends an outbound message_: Set up a trigger for your messaging platform (Slack, Discord, Google Chat, etc.). It will listen for updates to a message thread and kick off once you send a message.
2. _Filter out inbound messages_: You want this Zap to run only when a new message are sent by you, the business. As such, you will need to introduce a **Filter** step into your workflow. In this step, you will filter out messages that aren't sent from the business.
3. _Retrieve the Yelp Lead ID from your data storage_: Using the conversation ID from your trigger, grab the associated Yelp Lead ID.
4. _Create a new Yelp Leads message_: The message from the messaging platform is then sent straight to the Yelp Lead through the **Create Message** action. By providing the Yelp Lead ID from the previous step, you ensure that the message is being sent to the correct thread.

![](https://files.readme.io/ce70b918bbdc8aeba1047ae37be92d83961b73ced4f26f91dd7903fb0c917f1a-image.png) 

##### 

Tracking Outbound Messages from the Business

1. _Business sends an outbound message_: Set up a **New Business Message** trigger for your Yelp Leads conversation. It will listen for outbound messages from the business to the customer.
2. _Look up the Yelp Lead ID in your data storage_: Using the Yelp Lead ID, find where the conversation is being stored.
3. _Update records of conversation_: Append the most recent outbound message for record-keeping purposes.

![](https://files.readme.io/3537da0e80be3792f45bed168ecfac643949e8d4e9dd1eb700858c58453a3d81-image.png) 

---

 

## 

Example Zap Workflows

#### 

When a new lead is created via Yelp Leads, create a new row in a Google Sheets spreadsheet.

This is a basic example of how you can leverage the Yelp Leads Zapier app to automatically move Yelp Lead information into a Google Sheets spreadsheet.

[Get a head start by using this Zapier template!](https://zapier.com/shared/aa6cd433d8655a1fda74f4662e3edf51e2a7e75d)

![New Lead -> Create Spreadsheet Row Zap workflow](https://files.readme.io/e972f301dec637236d0fec384627253abb29d36a15978a3760fee3ea2b28a2de-image.png)

New Lead -> Create Spreadsheet Row Zap workflow

![Example configuration of passing Yelp Lead fields into Google Sheet columns](https://files.readme.io/03bea6f067529ec26d43889f6b9f6a516aeff0bbf3f07a1723ed66058d9ee2a8-image.png)

Example configuration of passing Yelp Lead fields into Google Sheet columns

![Example output in a basic spreadsheet](https://files.readme.io/3be711dda4ab27b85543409b06a256d2ecfb69f84c455c9f4518e6c0ffadf417-image.png)

Example output in a basic spreadsheet

#### 

When a Lead Submitter opts in to being contacted by phone, update your existing Lead record with the new phone number in Google Sheets.

[Get a head start by using this Zapier template!](https://zapier.com/shared/c5a6745ab565b7ce87ae28c3ac984676d8ea2a38)

This is a basic example of how you can leverage the Yelp Leads Zapier app to automatically update existing Leads with a phone number once a Lead Submitter opts in.

![Phone Availability -> Lookup row for Lead ID in Google Sheet -> Update record with new phone number](https://files.readme.io/e913f64836a3180381f571ffb067684f42aeec5e0ba82a08f6cc21fa11771802-image.png)

Phone Availability -> Lookup row for Lead ID in Google Sheet -> Update record with new phone number

![Example configuration of looking up a spreadsheet row based on Yelp Lead ID](https://files.readme.io/db235933e1744d976cfddac4c8b3c2f3f7842584cd1ce8da5d77a83ad42ca3b1-image.png)

Example configuration of looking up a spreadsheet row based on Yelp Lead ID

![Example configuration of updating the Google Sheet row](https://files.readme.io/eb49a12d332355121d7892dd4952a2a465ece10b4f8afbbc848b6a4ef28c9e27-image.png)

Example configuration of updating the Google Sheet row

![Example updated spreadsheet with new phone number](https://files.readme.io/d0d7df8cee3b8d068c6276adb724e76328d53949d2b6365c72ed8ce269722a88-image.png)

Example updated spreadsheet with new phone number

 
 
 
 
 

---

## 

FAQ

**How can I get help with my Zapier integration?**

If you need assistance or have questions about your Zapier integration, reach out at [zapier-support@yelp.com](mailto:zapier-support@yelp.com) or fill out this [form](https://docs.google.com/forms/d/e/1FAIpQLSdxLoxhvz4pJK-Hyn4KBJjH9WkWGG9PNf9_XE_ds85LVz4WqA/viewform?usp=sharing&ouid=100848218112025059765).

**Why can’t I get the real phone number and email address?**

As of April 16, 2026, you can receive the real phone number through this integration. At the time of writing, it is only available through the `Temporary Phone Number` field.

We mask email addresses to limit the exposure of PII between users, businesses, and third-party systems.

**How can we get the real phone number and email address?**

There is no option or plans to expose these.

**Can we ask the consumer for their real contact info?**

Yes, feel free to ask the consumer directly for more info, it is up to them if they want to share more information.

**Where can I find pricing information for Zapier?**

For any pricing related questions, please contact Zapier directly.

**What if my CRM/Lead Gen software is not supported by Zapier?**

Zapier allows you to leverage webhooks if a native app is not present for your tool of choice.

**How long will the integration take to build?**

It depends on your engineering bandwidth and priorities, but others have completed in a few days to 1 month.

Updated 2 months ago

---

Did this page help you?

Yes

No

Copy Page