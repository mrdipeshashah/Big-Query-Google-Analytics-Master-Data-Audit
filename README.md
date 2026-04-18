# OVERVIEW
This repository contains Big Query code using Google Analytics raw data that will provide a summary of the Google Analytics data. The data studio dashboard (https://datastudio.google.com/reporting/47aa8820-3e4b-4844-8084-093acf00a59b) that brings will bring many of the insights to life providing a summary helping to better understamd the business and the Google Analytics data. The dashboard covers: 

1. Channel performance
2. Landing page performance
3. Tech stack performance
4. Data quality performance
5. Location performance

The Google Analytics audit + dashboard is E-commerce focused but it can be tweaked for any business model i.e. lead generation 

# THE SET-UP
The steps required:

1. To be able to generate the data to build the dashboard it requires implementing this GTM container > https://github.com/GTMRecipeContainers/Google-Analytics-4-Enhanced-E-commerce it will require configuring the triggers + GA4 event tag that works best for the website
3. Google Analytics is connected to Big Query
4. The 101-GA-Audit Big Query code provided, create and save the view in Big Query
5. Make a copy of the data studio dashboard and connect it to the saved view

# THE WATCH-OUTS
The key Watch-Outs: 

1. The most critical step is having Google Analytics connected to Big Query, the 101-GA-Audit is using the default schema in Big Query + purchase event which will need to be setup in Google Tag Manager to provide the insights 
2. It's important to have the right architecture setup. The above shared GitHub GTM link helps with the architecture if a deeper aduit of events etc is needed  
3. The Big Query code - purchase-event-tracking is used on the 7 day and yesterday scorecards + transaction ID health table 
4. The Big Query code - all-events-tracking is used on the event health trend chart + purchase event health v baseline + event volume by journey stage + event audit log
5. The Trans ID Fill in the scorecard is SUM(is_id_populated)/SUM(is_purchase) and it needs to be using - purchase-event-tracking 
6. The Trans ID Status which is the dropdown for the Trans ID Health table using the below following which is created as a calculated file in purchase-event-tracking. Add Field > Add Calcularted Field 

  CASE 
  WHEN is_id_populated = 1 THEN "✅ ID Populated" 
  ELSE "❌ Missing ID (Red Rows)" 
  END

# FILTERING

One of the key outputs from the audit will be how to filter data to provide a better view of performance. The options would be to either filter in Biq Query (hard filter) or in Data Studio (soft filter). 

Exclude In Big Query: 

1. Spam & Bot Traffic: If you identify a surge of fake hits from a specific IP or Browser version
2. Hostname Errors: Traffic from test.shop.com or localhost
3. Ghost Transactions: Technical misfires with NULL IDs that have no business value
4. Internal Testing: Traffic from your dev team

Exclude in Data Studio: 

1. Regional Focus (e.g., Africa): If you want the option to see that data occasionally, but want the main dashboard to ignore it.
2. Product Categories: Switching between views for "Product A" vs "Product B."
3. Date Ranges: Allowing the user to toggle between Last 14 Days and Last 30 Days
4. Marketing Segments: Toggling between Organic and Paid traffic performance
