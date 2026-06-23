# Source: https://docs.developer.yelp.com/docs/agentic_ai_api

## 

Introduction

This guide will take you through the process of building a powerful AI agent using a Large Language Model (LLM) integrated with Yelp AI API.

We'll leverage Langchain alongside an OpenAI LLM agent to interact with the Yelp AI API, enabling your agent to handle complex business queries with ease.

 

### 

What You'll Learn

- Setting up Yelp Places API integration
- Creating an LLM agent that handles business queries
- Managing conversation context
- Handling multi-turn dialogues

 

### 

What Can This Agent Do?

Your agent will be able to handle natural conversations like:

`User: "Find the best pizza places near me" Agent: [Provides list of top pizza places]  User: "What are their opening hours?" Agent: [Shows business hours for the entire week including special hours]`

 

## 

Prerequisites

Before we start, make sure you have:

1. **Yelp Developer Account**
 
 - Sign up at [Yelp's Developer Portal](https://business.yelp.com/data/products/fusion)
 - Get your API key
2. **API Authentication**
 
 Shell
 
 `# Your key should be stored securely YELP_API_KEY = "your_yelp_api_key_here"`
 
3. **LLM Environment**
 
 - Access to an LLM (like OpenAI's GPT models)
 
 Python
 
 `import os  os.environ["OPENAI_API_KEY"] = "your_openai_api_key"`
 
 - Python environment with required packages

 

## 

Setting Up the Basic Structure

1. **Let's define a sample function**

Let's look at the steps to allow a model to use a `yelp_ai_api` function defined below as a Langchain tool:

Python

`import requests from langchain_core.tools import tool from pydantic import BaseModel, Field  class YelpQueryInput(BaseModel):     query: str = Field(description="The user's query for local business information")     chat_id: str | None = Field(description="Unique chat ID for maintaining conversation history", default = None)  @tool(args_schema=YelpQueryInput) def yelp_ai_api(query: str, chat_id: str) -> dict:     """     Calls Yelp AI API to get local business information and comparisons from a natural language query.      Args:     - query: The user's query for local business information.     - chat_id: Unique chat ID for maintaining conversation history.      Returns:     - dict: JSON response from the Yelp AI API or an error message.     """     url = "https://api.yelp.com/ai/chat/v2"     headers = {       "Authorization": f"Bearer {YELP_API_KEY}",       "Content-Type": "application/json"     }     data = {       "query": query,       "chat_id": chat_id     }      try:       response = requests.post(url, headers=headers, json=data)       response.raise_for_status()       return response.json()     except requests.RequestException as e:       return {"error": f"API request failed: {str(e)}"}`

2. **Create LLM agent**

_The agent is initialized with the `OPENAI_API_KEY` we created earlier._

Python

`from langchain_openai import ChatOpenAI from langchain.prompts import ChatPromptTemplate from langchain.agents import AgentExecutor, create_tool_calling_agent  # Initialize OpenAI model llm = ChatOpenAI(model="gpt-4o")  # Define a system prompt for the agent prompt = ChatPromptTemplate.from_messages(   [     ("system", "You are a helpful assistant"),     ("human", "{input}"),     # Placeholders fill up a **list** of messages     ("placeholder", "{agent_scratchpad}"),   ] )  # Intialize the agent agent = create_tool_calling_agent(llm, tools=[yelp_ai_api], prompt=prompt) # Intialize AgentExecutor agent_executor = AgentExecutor(agent=agent, tools=[yelp_ai_api], verbose=True)`

Learn more about AgentExecutor in the [official documentation](https://python.langchain.com/api_reference/langchain/agents/langchain.agents.agent.AgentExecutor.html)

3. **Invoke the agent**

Python

`input_data = {   "query": "Find the best pizza places in SF",   "chat_id": None  # None for first message }  # Run the agent response = agent_executor.invoke({"input": input_data}) print(response)`

Here is the response:

Output

`{   "input": {     "query": "Find the best pizza places in SF",     "chat_id": null   },   "output": "Here are some of the best pizza places in San Francisco according to Yelp:\n\n1. **Tony's Pizza Napoletana**\n   - Address: 1570 Stockton St, San Francisco, CA 94133\n   - Rating: 4.2 (7813 reviews)\n   - Price: $$\n   - Known for its award-winning pizzas and wide variety of pizza styles, including Neapolitan, Detroit, St. Louis, and New York. It features a full bar and is located in a vibrant neighborhood.\n   - Visit: [Tony's Pizza Napoletana Yelp](https://www.yelp.com/biz/tonys-pizza-napoletana-san-francisco?adjust_creative=3aOVd6DAVkgZJsTctgMtSA&utm_campaign=yelp_api_v3&utm_medium=api_v3_public_ai_api_chat_v2&utm_source=3aOVd6DAVkgZJsTctgMtSA)\n\n2. **Golden Boy Pizza**\n   - Address: 542 Green St, San Francisco, CA 94133\n   - Rating: 4.3 (4616 reviews)\n   - Price: $\n   - Famous for its Sicilian-style squares with a thick, focaccia-like crust. Recommended for its clam and garlic pizza and casual atmosphere.\n   - Visit: [Golden Boy Pizza Yelp](https://www.yelp.com/biz/golden-boy-pizza-san-francisco?adjust_creative=3aOVd6DAVkgZJsTctgMtSA&utm_campaign=yelp_api_v3&utm_medium=api_v3_public_ai_api_chat_v2&utm_source=3aOVd6DAVkgZJsTctgMtSA)\n\n3. **That's Amore Woodfire Pizza**\n   - Address: 1901 Ocean Ave, San Francisco, CA 94127\n   - Rating: 4.5 (270 reviews)\n   - Price: $$\n   - Known for authentic wood-fired pizzas made with fresh ingredients. Features a Stefano Ferrera oven from Naples, Italy. Cozy ambiance with live music on Thursdays.\n   - Visit: [That's Amore Woodfire Pizza Yelp](https://www.yelp.com/biz/thats-amore-woodfire-pizza-san-francisco?adjust_creative=3aOVd6DAVkgZJsTctgMtSA&utm_campaign=yelp_api_v3&utm_medium=api_v3_public_ai_api_chat_v2&utm_source=3aOVd6DAVkgZJsTctgMtSA)\n\nEach of these pizza spots offers a unique dining experience with highly-rated pizzas and welcoming atmospheres." }`

 

## 

Handling Multi-Turn Conversations

You can store the `chat_id` from the response in `yelp_ai_api()` and pass it in subsequent calls to continue the conversation.

Here is a sample response from the Yelp AI endpoint. Copy the `chat_id`.

Sample output from Yelp AI API endpoint

`{   "response": {     "text": "Here are some places in San Francisco offering the best pizza with excellent reviews and a welcoming atmosphere."   },   "types": [     "business_search"   ],   "entities": [     {       "businesses": [         {           "id": "mSMZJj2pFvttWLpcDmgrEA",           "alias": "tonys-pizza-napoletana-san-francisco",           "name": "Tony's Pizza Napoletana",           "url": "https://www.yelp.com/biz/tonys-pizza-napoletana-san-francisco?adjust_creative=3aOVd6DAVkgZJsTctgMtSA&utm_campaign=yelp_api_v3&utm_medium=api_v3_public_ai_api_chat_v2&utm_source=3aOVd6DAVkgZJsTctgMtSA",           "location": {             "address1": "1570 Stockton St",             "address2": "",             "address3": "",             "city": "San Francisco",             "zip_code": null,             "state": "CA",             "country": "US",             "formatted_address": "1570 Stockton St\nSan Francisco, CA 94133"           },           "coordinates": {             "latitude": 37.8003893855776,             "longitude": -122.40903343231504           },           "review_count": 7815,           "price": "$$",           "rating": 4.2,           "categories": [             {               "alias": "pizza",               "title": "Pizza"             }           ],           "attributes": {             "BusinessAcceptsAndroidPay": false,             "BusinessAcceptsApplePay": false,             "WiFi": "no"           },           "phone": "+14158359888",           "summaries": {             "short": "Bustling pizzeria with award-winning pizzas and outdoor seating in North Beach.",             "medium": "Located in a vibrant neighborhood, this internationally recognized pizzeria is popular with visitors for its diverse range of pizza styles, including Neapolitan, Detroit, St. Louis, and New York, crafted with authentic Italian ingredients.",             "long": "Located in a vibrant neighborhood, this internationally recognized pizzeria is popular with visitors for its diverse range of pizza styles, including Neapolitan, Detroit, St. Louis, and New York, crafted with authentic Italian ingredients."           },           "contextual_info": {             "summary": "Known for its award-winning pizzas and outdoor seating, this bustling pizzeria in North Beach is a must-visit for pizza lovers.",             "review_snippets": [],             "business_hours": [               {                 "day_of_week": "Monday",                 "business_hours": [                   {                     "open_time": "2025-03-03 12:00:00",                     "close_time": "2025-03-03 21:30:00"                   }                 ],                 "special_hours_applied": false               }             ],             "photos": [               {                 "original_url": "https://s3-media0.fl.yelpcdn.com/bphoto/EEYTzxAAtuaHx7Vw2piKCQ/o.jpg"               }             ],             "review_snippet": "Tony's isn't just the [[HIGHLIGHT]]best pizza[[ENDHIGHLIGHT]] in the city, but it may be the best pizza I've ever had!"           }         }       ]     }   ],   "chat_id": "N1u996U6HInvhrCaedrb1Q" }`

 

Here's how to manage context and follow-up questions:

Python

`chat_id = "N1u996U6HInvhrCaedrb1Q"  # should be referred from previous API call query = "What are their opening hours?"  input_data = {     "query": query,     "chat_id": chat_id } response = agent_executor.invoke({"input": input_data}) print(response)`

Here is the response:

Output

`{   "input": {     "query": "What are their opening hours?",     "chat_id": "17nYOwqmFA3S3kjxXuJjIQ"   },   "output": "Here are the opening hours for the businesses mentioned:\n\n1. **Tony's Pizza Napoletana** \n   - Monday & Tuesday: 12:00 PM - 9:30 PM\n   - Wednesday & Thursday: 12:00 PM - 10:00 PM\n   - Friday & Saturday: 12:00 PM - 11:00 PM\n   - Sunday: 12:00 PM - 10:30 PM\n   - [Visit Tony's Pizza Napoletana on Yelp](https://www.yelp.com/biz/tonys-pizza-napoletana-san-francisco?adjust_creative=3aOVd6DAVkgZJsTctgMtSA&utm_campaign=yelp_api_v3&utm_medium=api_v3_public_ai_api_chat_v2&utm_source=3aOVd6DAVkgZJsTctgMtSA)\n\n2. **Golden Boy Pizza**\n   - Monday to Thursday: 11:30 AM - 9:00 PM\n   - Friday & Saturday: 11:30 AM - 11:00 PM\n   - Sunday: 11:30 AM - 9:00 PM\n   - [Visit Golden Boy Pizza on Yelp](https://www.yelp.com/biz/golden-boy-pizza-san-francisco?adjust_creative=3aOVd6DAVkgZJsTctgMtSA&utm_campaign=yelp_api_v3&utm_medium=api_v3_public_ai_api_chat_v2&utm_source=3aOVd6DAVkgZJsTctgMtSA)\n\n3. **That's Amore Woodfire Pizza**\n   - Open every day from 11:00 AM - 9:45 PM\n   - [Visit That's Amore Woodfire Pizza on Yelp](https://www.yelp.com/biz/thats-amore-woodfire-pizza-san-francisco?adjust_creative=3aOVd6DAVkgZJsTctgMtSA&utm_campaign=yelp_api_v3&utm_medium=api_v3_public_ai_api_chat_v2&utm_source=3aOVd6DAVkgZJsTctgMtSA)" }`

 

## 

Location based search results

By passing the user's location (latitude and longitude) to the Yelp AI endpoint, you can retrieve businesses around the user's current location.

### 

Steps to Implement Location-Based Search:

1. **Redefine the Tool to Include User Location** 
 Update your Tool to send the user's location in the API call. This allows the API to return results specific to the user's geographical area.

Python

`import requests from langchain_core.tools import tool from pydantic import BaseModel, Field  class UserContext(BaseModel):     latitude: float     longitude: float  class YelpQueryInput(BaseModel):     query: str = Field(description="The user's query for local business information")     chat_id: str | None = Field(description="Unique chat ID for maintaining conversation history", default = None)     user_context: UserContext = Field(description="Contains user's latitude and longitude for location-based search")  @tool(args_schema=YelpQueryInput) def yelp_ai_api(query: str, chat_id: str, user_context: UserContext) -> dict:     """     Calls Yelp AI API to get local business information and comparisons from a natural language query.          Parameters:     - query: The user's query for local business information.     - chat_id: Unique chat ID for maintaining conversation history.     - user_context: Contains user's latitude and longitude for location-based search.          Returns:     - dict: JSON response from the Yelp AI API or an error message.     """     url = "https://api.yelp.com/ai/chat/v2"     headers = {       "Authorization": f"Bearer {YELP_API_KEY}",       "Content-Type": "application/json"     }     data = {       "query": query,       "user_context": {         "latitude": user_context.latitude if user_context else None,         "longitude": user_context.longitude if user_context else None       },       "chat_id": chat_id     }      try:       response = requests.post(url, headers=headers, json=data)       response.raise_for_status()       return response.json()     except requests.RequestException as e:       return {"error": f"API request failed: {str(e)}"}`

2. **Invoke the agent**

Call the agent with the user's location data to get personalized search results.

Python

`input_data = {   "query": "Find the best pizza places near me",   "user_context": {     "latitude": 37.7749,     "longitude": -122.4194   },   "chat_id": None  # None for first message }  # Run the agent response = agent_executor.invoke({"input": input_data}) print(response)`

Here is the response:

Output

`{   "input": {     "query": "Find the best pizza places near me",     "user_context": {       "latitude": 37.7749,       "longitude": -122.4194     },     "chat_id": null   },   "output": "Here are some of the best pizza places near you in San Francisco:\n\n1. **[Tony's Pizza Napoletana](https://www.yelp.com/biz/tonys-pizza-napoletana-san-francisco?adjust_creative=3aOVd6DAVkgZJsTctgMtSA&utm_campaign=yelp_api_v3&utm_medium=api_v3_public_ai_api_chat_v2&utm_source=3aOVd6DAVkgZJsTctgMtSA)**\n   - **Rating:** 4.2\n   - **Review Count:** 7813\n   - **Price:** $$\n   - **Address:** 1570 Stockton St, San Francisco, CA 94133\n   - **Description:** Renowned pizzeria in North Beach with award-winning pizzas, including the celebrated Margherita. Offers a variety of pizza styles with a full bar.\n   - **Specialties:** Neapolitan, Classic American, Italian, Sicilian, and more.\n   - **Business Hours:** Open daily from 12 PM, with varying closing times throughout the week.\n\n   ![Tony's Pizza](https://s3-media0.fl.yelpcdn.com/bphoto/EEYTzxAAtuaHx7Vw2piKCQ/o.jpg)\n\n2. **[Outta Sight Pizza](https://www.yelp.com/biz/outta-sight-pizza-san-francisco?adjust_creative=3aOVd6DAVkgZJsTctgMtSA&utm_campaign=yelp_api_v3&utm_medium=api_v3_public_ai_api_chat_v2&utm_source=3aOVd6DAVkgZJsTctgMtSA)**\n   - **Rating:** 4.6\n   - **Review Count:** 317\n   - **Price:** $\n   - **Address:** 422 Larkin St, San Francisco, CA 94102\n   - **Description:** Cozy urban pizzeria known for its New York-style slices and unique toppings. \n   - **Specialties:** Thin, crispy crust with diverse slice options like Ruby Pie and BLT slice.\n   - **Business Hours:** Open daily 11 AM to 9 PM.\n\n   ![Outta Sight Pizza](https://s3-media0.fl.yelpcdn.com/bphoto/QmWNIf_B_OJk9WCJ1JFdMw/o.jpg)\n\n3. **[Golden Boy Pizza](https://www.yelp.com/biz/golden-boy-pizza-san-francisco?adjust_creative=3aOVd6DAVkgZJsTctgMtSA&utm_campaign=yelp_api_v3&utm_medium=api_v3_public_ai_api_chat_v2&utm_source=3aOVd6DAVkgZJsTctgMtSA)**\n   - **Rating:** 4.3\n   - **Review Count:** 4616\n   - **Price:** $\n   - **Address:** 542 Green St, San Francisco, CA 94133\n   - **Description:** Famous for its Sicilian-style pizza with a thick, focaccia-like crust, especially the clam and garlic pizza.\n   - **Specialties:** Square slices with quick service, perfect for takeout.\n   - **Business Hours:** Open daily 11:30 AM to 9 PM, with extended hours on weekends.\n\n   ![Golden Boy Pizza](https://s3-media0.fl.yelpcdn.com/bphoto/3HLUfXgYw2f7XgJwxPNnGQ/o.jpg)\n\nThese spots offer a variety of pizza styles, from classic Neapolitan to modern, innovative slices. Enjoy!" }`

 

## 

Next Steps

Explore the [Fusion AI API](https://docs.developer.yelp.com/reference/v2_ai_chat) to understand how to effectively call the endpoint and interpret detailed responses. This will help you leverage the full capabilities of Yelp AI API.

Updated 10 months ago

---

Did this page help you?

Yes

No

Copy Page