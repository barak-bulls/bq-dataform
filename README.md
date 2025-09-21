# bq-dataform

This project manages the dataform for P-Com Bigquery DWH

# Version 1 Tickets

1. https://meagensupport.freshdesk.com/a/tickets/69371 - magimix report
2. https://meagensupport.freshdesk.com/a/tickets/67319 - regression testing for existing reports
3. https://meagensupport.freshdesk.com/a/tickets/70825 - BQ Data dependencies view

# Version 1 Pre-prod test

## Dataset

1. In BQ, Copy dataset dwh_prod to dwh_pre and stg_prod to stg_pre
2. Copy table dim_campaigns from dwh_test to dwh_pre
3. Add integer column fact_daily_segments.campaign_id to dwh_pre 
4. same for fact_daily_segments_pre

## Data

5. Set fact_daily_segments.campaign_id to -1
-- Update column dim_offers.company_id test merging on vol_offer_id and jv_id
6. Truncate table mrr.segments_with_campaigns  
   - In Jupyter Notebook, run V1 Upgrade --> Initial load to segments_with_campaigns table
7. Check the earliest date in mrr.segments_with_campaigns and delete all records from dwh_pre.fact_daily_segments starting this date (except sc_jv_id=16)
    - truncate fact_daily_segments_pre and insert from fact_daily_segments

## Upgrade Dataform

8. Create a new dev workspace and name it pre-v1
9. Pull from main branch
10. Change yaml settings to "pre" (datasetSuffix, dwh_schema,stg_schema)
11. Run dataform

## PBI

12. Copy relevant reports to pre version and compare to test version and prod version
