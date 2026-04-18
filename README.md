# OVERVIEW
This repository contains Big Query code using Google Analytics raw data that will provide a summary of the Google Analytics data. The data studio dashboard (https://datastudio.google.com/reporting/47aa8820-3e4b-4844-8084-093acf00a59b) that brings will bring many of the insights to life providing a summary helping to better understamd the business and the Google Analytics data. The dashboard covers: 

1. Channel performance
2. Landing page performance
3. Tech stack performance
4. Data quality performance
5. Location performance 

# THE SET-UP
The steps required:

1. To be able to generate the data to build the dashboard it requires implementing this GTM container > https://github.com/GTMRecipeContainers/Google-Analytics-4-Enhanced-E-commerce it will require configuring the triggers + GA4 event tag that works best for the website
2. Google Analytics is connected to Big Query
3. The 2 Big Query code provided, create and save the views in Big Query
4. Make a copy of the looker studio dashboard and connect it to the saved views

# THE WATCH-OUTS
The key Watch-Outs: 

1. It's important to have the right architecture setup. The above shared GitHub GTM link helps with the architecture which needs to be supported by a data layer architecture   
2. The Big Query code - purchase-event-tracking is used on the 7 day and yesterday scorecards + transaction ID health table 
3. The Big Query code - all-events-tracking is used on the event health trend chart + purchase event health v baseline + event volume by journey stage + event audit log
4. The Trans ID Fill in the scorecard is SUM(is_id_populated)/SUM(is_purchase) and it needs to be using - purchase-event-tracking 
5. The Trans ID Status which is the dropdown for the Trans ID Health table using the below following which is created as a calculated file in purchase-event-tracking. Add Field > Add Calcularted Field 

  CASE 
  WHEN is_id_populated = 1 THEN "✅ ID Populated" 
  ELSE "❌ Missing ID (Red Rows)" 
  END

  
