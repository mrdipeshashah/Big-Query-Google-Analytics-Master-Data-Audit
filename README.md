# OVERVIEW
This repository contains Big Query code using Google Analytics raw data tracking the health of events via Google Tag Manager. Tags are critical in the GTM set-up but the common domoino for all platforms is the event/trigger which is used by Google Ads, Meta, Google Analytics etc. The focus is on event performance that any of the different teams working with the different platforms would want assurance on the health of the events.  

(I use event & trigger interchangeably - The best set-up are when the event name + trigger are the same, i.e. event name = purchase, trigger = purchase)

If Google Analytics stops tracking e-commerce sales it means the purchase event/trigger has failed meaning it would also fail for Google Ads, Meta etc. It also means if there are 100 purchase events reported on a given day it means Google Ads, Meta etc cannot be reporting more than 100 purchase events. 

I have developed a looker studio dashboard (https://lookerstudio.google.com/reporting/b3d4ac15-0583-4b5a-a083-32bdbd41d6ca) that brings the insights to life. 

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

  
