# Source: https://docs.developer.yelp.com/docs/conversions-api-zapier

> ## 🚧
> 
> Yelp Conversions API Availability
> 
> **Yelp Conversions is currently meant for larger businesses with 10+ locations**. If you do not meet this criteria, you may not receive attribution reporting at this time. If you’d like to tell us more about your interest in this integration, [please fill out this form](https://docs.google.com/forms/d/e/1FAIpQLSdWOpA1CnkrhqYNX21BsWFvaFKvwG8M99R7hY3EQGaTbFc3LA/viewform).

## 

Overview

This guide outlines the steps for implementing the Yelp Conversions API (CAPI) integration using Zapier. Leveraging Zapier provides a straightforward, plug-and-play approach to bridge your data sources with Yelp CAPI for streamlined attribution reporting.

### 

Table of Contents

1. [Prerequisites](https://docs.developer.yelp.com/docs/conversions-api-zapier#prerequisites)
2. [Setup Guide](https://docs.developer.yelp.com/docs/conversions-api-zapier#setup-guide)
 1. [Step 1: Create a New Zap](https://docs.developer.yelp.com/docs/conversions-api-zapier#step-1-create-a-new-zap)
 2. [Step 2: Review CAPI Requirements](https://docs.developer.yelp.com/docs/conversions-api-zapier#step-2-review-capi-requirements)
 3. [Step 3: Map the Fields to Complete the Zap](https://docs.developer.yelp.com/docs/conversions-api-zapier#step-3-map-the-fields-to-complete-the-zap)
 4. [Step 4: Send a Test Zap](https://docs.developer.yelp.com/docs/conversions-api-zapier#step-4-send-a-test-zap)
 5. [Step 5: Publish the Zap](https://docs.developer.yelp.com/docs/conversions-api-zapier#step-5-publish-the-zap)
3. [Hybrid Integration: Zapier Webhooks + CRM API](https://docs.developer.yelp.com/docs/conversions-api-zapier#hybrid-integration-zapier-webhooks--crm-api)

### 

Prerequisites

- You have reviewed our [Conversions API documentation.](https://docs.developer.yelp.com/docs/conversions-api)
- You have been assigned a Yelp Sales Engineer
- You have a Zapier account
- You have a Yelp Business account
- Confirmation that your CRM has a Zapier application with the necessary action to send transaction data
 - Alternatively, access to your CRM's APIs

### 

Setup Guide

#### 

Step 1: Create a New Zap

- Select your CRM for the trigger step.
 - You will need to identify the correct action provided by your CRM's Zapier app. This action will need to surface purchase data.
 - If your CRM does not have a Zapier application but does have an API, see [this section](https://docs.developer.yelp.com/docs/conversions-api-zapier#hybrid-integration-zapier-webhooks--crm-api) below.
- Select **Yelp CAPI** as the following action.
 - When prompted, authenticate with a Yelp Business account.
 - Depending on your CRM, you may need more than one action for this integration.

![A basic one-step Yelp CAPI integration in Zapier](https://files.readme.io/a448dc4573dddc844229d4a80c52658be4ab05e0848fe6868fd1f14a483c9d36-image.png)

A basic one-step Yelp CAPI integration in Zapier

![In the example above, additional steps are required to retrieve contact information associated with a deal in Hubspot.](https://files.readme.io/3a81c6cd0f13c66a18e8a4a60e18e6057bfe9615e7494ff9c2e2fd0d3ffd5b44-image.png)

In the example above, additional steps are required to retrieve contact information associated with a deal in Hubspot.

 

#### 

Step 2: Review CAPI requirements

- Refer to [Yelp Conversions API schema](https://docs.developer.yelp.com/docs/conversions-api#conversion-data-format) to understand the type of data you'll be sharing.

> ## 📘
> 
> Normalizing and Hashing Data
> 
> You don’t need to normalize or hash data for CAPI integrations when using the Yelp CAPI Zapier app—data formatting is handled automatically by the application.

#### 

Step 3: Map the Fields to Complete the Zap

- Select fields from your CRM trigger step and map them over to the required fields in the Yelp CAPI configuration step.

![](https://files.readme.io/cc07aa31f9af368b0071f2fbb304fa18bb073372597c750162ca4efb2e362095-image.png)

#### 

Step 4: Send a Test Zap

- Mark "Test Event" at the top of the **Configure** page in your **Yelp Conversions -> Send Single Events** step.

![](https://files.readme.io/88ab73f1b20b7fd3fe530e00544db77eadd35fa0ea25593db89a2d41d7b2e3f2-image.png)

- Click _Continue_ at the bottom of the page and then _Test_ on the next page.

![](https://files.readme.io/4b95a3270b2343d6e1267f783b69ad8bb7e36cf75a1dee1abf6b8bea251e7c33-image.png)

- If the test was **successful**, you will see the message "A Event was sent to Yelp Conversions (1.0.0) about 0 seconds ago". If the test was **not successful**, there may be an issue with your account. Please reach out to your Yelp Sales Engineer or email [zapier-capi-support@yelp.com](mailto:zapier-capi-support@yelp.com)

![A successful test run for Yelp CAPI on Zapier](https://files.readme.io/b5f0ada857309fe4c56c46e867b078bc8fb8119efc7456a527aca0027f9b59aa-image.png)

A successful test run for Yelp CAPI on Zapier

 

#### 

Step 5: Publish the Zap

- Once you have successfully tested the Zap and have double-checked your field mappings, go ahead and click "Publish" at the bottom of the page.

![](https://files.readme.io/1d0d34e001aec3546570dba611c304dbafaf66bfff3d49ac9b95c836b7e39d25-image.png) 

- Upon publishing your Zap, inform your account representative. As Yelp aggregates your conversions events, we will eventually be able to report on your ROAS.

 

### 

Hybrid Integration: Zapier Webhooks + CRM API

If your CRM does not have a Zapier app, or if its Zapier integration does not provide access to the data you need, check whether your CRM offers an accessible API. While this approach requires a bit more setup, you can still complete the integration by using the Zapier Webhooks trigger to connect directly to your CRM’s API and retrieve the necessary information.

If you need assistance with setting up this type of integration, please contact your Yelp Sales Engineer or email [zapier-capi-support@yelp.com](mailto:zapier-capi-support@yelp.com)

![](https://files.readme.io/dc861af8cb43997279467770d03ce2e66bf3cf79aaae6a6d86718c7cbb8ff051-image.png)

Updated 8 months ago

---

Did this page help you?

Yes

No

Copy Page