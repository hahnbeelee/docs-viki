# Source: https://docs.developer.yelp.com/docs/leads-zapier-integration-access-error-when-testing

When testing a Zap workflow, you may want to test with actual leads on your Yelp business account. You'll find that the **New Lead** and **New Message** triggers only provide a dummy data set to test with. Additionally, if you try to access the dummy lead data in a downstream Yelp action, you will be presented with the following error message: “You don’t have access to this business.” This usually means the lead you’re trying to retrieve belongs to a Yelp test business you don’t manage.

![Screenshot: Common testing error when setting up Yelp Leads in Zapier](https://files.readme.io/3807b4cf1cce70b4d967e0853312cfdc1ab35b1db8ede68811ab8634d742fda9-image.png)

Screenshot: Common testing error when setting up Yelp Leads in Zapier

So how do you to perform end-to-end testing on this workflow with actual Yelp Leads data instead of dummy data? To successfully test your Zap before publishing, you will need to generate a new test lead and obtain its lead ID. Please follow these steps:

### 

Generating a Lead via Request-a-Quote

1. Access your Yelp Business Account at [biz.yelp.com](https://docs.developer.yelp.com/biz.yelp.com).
 
2. Navigate to your public business page by linking out via the external link icon next to your business name, as indicated by the red arrow below.
 
 ![](https://files.readme.io/8cafedc1bf29b60172723d3ef2478165e2594a27b67c280a28560b7e06798b45-image.png) 
 
3. Submit a a test lead. **Note:** Because this is an organic event, this test lead will not be charged from your CPC budget.
 
 ![](https://files.readme.io/7527f86eb9866e56bb00d0a5201c2ce65e331247e9675b8ec920b9c3084f6e4d-image.png) ![](https://files.readme.io/c19465d57a012d25e8ab5bbc4e655c7f350d28a3df7be1614db4be443205aef0-image.png) 
 1. Be sure to leave the "Get competitive pricing" box unchecked
 
 ![](https://files.readme.io/235cc776ce453c3e2642191839ef679ab49669ddd0d5874960612856c79243b4-image.png) 
 

### 

Grabbing Your Lead ID for Testing

1. Once the lead has been generated, you can find a new messaging thread for the lead in your Yelp Inbox
 
 ![](https://files.readme.io/0debd2a643dc2ec4f80bca9e21ced8dc7667ab761a9c50644ba0c500dbb7b8d6-image.png)

 

1. Navigate to your new test lead (it should be the newest thread at the top of your Yelp Inbox)
 
2. Collect the trailing alpha-numeric identifier in your browser URL. This represents your **test lead ID**.
 
 ![ ](https://files.readme.io/2a39467a10980eeae4078c677f0faa09c97dc3ae7d016086f2075ab957cb2e36-image.png) 
 

### 

Setting Up Your Zapier Test Workflow

In order to successfully test an end-to-end workflow beginning with a Yelp Leads trigger (**New Lead** or **New Message**) and ending in sending test lead data to a downstream application, we will temporarily introduce a **Get Lead Details** action step after the trigger. By doing so, we can manually input the **test lead ID** and proceed through the rest of the workflow using actual test data as opposed to the default dummy data provided in the trigger.

1. Input your **test lead ID** into the `Yelp Lead ID` field of the "Configure" substep.
 
 ![ ](https://files.readme.io/df0f500497176a16dbd26f43b4558d438fa16528f2def078081125cb9ad75845-image.png)
2. Click into the "Test" substep. You should receive a successful status on the test. You will now be able to grab actual test lead data in downstream Zap actions.
 
 ![ ](https://files.readme.io/187103a82067985d4699403fa6974474214f0483fbf7dcf83c880a601023c49e-image.png)

### 

Publishing Your Zap

Once you have completed testing and have confirmed that your Zap workflow is working as expected, you can remove the intermediary **Get Lead Details** action step and directly pass the `Yelp Lead ID` variable from the **New Lead** trigger directly into your downstream app. You will continue to receive the access error during the "Test" substep, but your integration will work as expected once it's published.

![](https://files.readme.io/480e9ea836cb8c3ff682b5eb535792eff124e43c493b2cf8fcd13fbe8486d1ea-image.png)

Copy Page