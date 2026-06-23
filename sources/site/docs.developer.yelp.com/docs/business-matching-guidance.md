# Source: https://docs.developer.yelp.com/docs/business-matching-guidance

When trying to match to business page on Yelp, we suggest normalizing your data to best match how we represent the data on Yelp.com to increase the likelihood that we will find and return the desired match. This includes potentially reformatting the business name and the address to align with our [Data Quality Guidelines](https://docs.developer.yelp.com/docs/yelp-data-quality-guidelines).

Here are some specific items to consider:

1. Special characters (such as @, #, /, and parentheses) and excessive store information in the business name and address fields, such as location tags, dba, and store numbers. These are typically not allowed per our Yelp listing guidelines and our system cannot match them. Examples: 
 JACK IN THE BOX #7310 
 ACCENT FOOD SERVICES @ KYND CANNABIS 
 TACO BELL #31858 
 GRILL AT QUAIL CORNERS (THE) 
 EGG ROLL KING @ S. WELLS AVE
 
2. Legal entities in the business name field (we only list the DBA; businesses with Inc., LLC, Co, Group, etc. are probably causing the no matches). Examples: 
 UMCo LLC DBA THE URBAN MARKET 
 TACOS JALISCO CANTINA & GRILL LLC 
 BIBO COFFEE CO INC 
 MINDFUL CUPCAKES LLC 
 SFP DEVELOPMENT CO LLC/DBA MOD PIZZA
 
3. Remove irrelevant businesses (i.e. non-restaurants/food businesses) and businesses we don't list on Yelp, such as the employee cafeteria at an office. Examples: 
 HARRAHS RENO EMPLOYEES LOUNGE (not eligible for Yelp) 
 ACCENT FOOD SERVICES CASHMAN UPSTAIRS BREAKROOM (not eligible for Yelp) 
 CVS PHARMACY #3948 (not a restaurant/food biz) 
 GOLDEN GATE PETROLEUM OF NEVADA LLC (not a restaurant/food biz) 
 DOLLAR TREE #6733 (not a restaurant/food biz) 
 FOOD ACCENT FOOD SERVICES SUMMIT RACING CALL CENTER (not a restaurant/food biz and also not eligible for Yelp) 
 ACCENT FOOD SERVICES SHERWIN WILLIAMS (this sounds like food services for employees as Sherwin Williams is a paint store, so it wouldn't be eligible since it's not consumer-facing) 
 WASHOE LITTLE LEAGUE (not a restaurant/food biz) 
 ELDORADO HOTEL EMPLOYEE RESTAURANT (not eligible for Yelp)
 
4. Joint businesses (or businesses located inside another). We have separate Yelp listings for each entity, so these need to come through as separate businesses. Examples: 
 AFC SUSHI / HOT WOK @ RALEYS #105 
 HYATT REGENCY LAKE TAHOE/TAHOE PROVISIONS 
 TARGET STORE T1363/PIZZA HUT EXPRESS
 
5. Businesses with no clear identity - concession stands at stadiums, amusement parks, and convention centers usually do not have a clear identity or distinctive business name and therefore, we do not grant them listings. Examples: 
 PEPPERMILL 2ND FLR CONVENTION SERVICE BAR 
 NUGGET SPARKS GAME ON SMALL BAR 
 LEVY PREMIUM FOOD SERVICE LTD CONCESSION STAND TWO 
 LEVY PREMIUM FOOD SERVICE THEME CART 
 ELDORADO HOTEL ROOM SERV BAR 
 ST JAMES INFIRMARY UPSTAIRS OUTSIDE BAR
 

Copy Page