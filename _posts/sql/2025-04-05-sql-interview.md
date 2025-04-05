---
layout: post
title:  "SQL Interview"
date:   2025-04-05 08:00:00 +0700
categories: [sql, coding, interview]
---

1. Identify Top Performing Ad Sets by ROAS
  - 2 tables:
    - `ad_clicks(ad_id, user_id, click_time, cost)`
    - `purchases(user_id, purchase_time, purchase_value)`
  - Calculate ROAS for each `ad_id`, defined as total `purchase_value` / total `cost`.
~~~sql
SELECT 
  ac.ad_id,
  SUM(p.purchase_value) / SUM(ac.cost) AS roas
FROM 
  ad_clicks ac
JOIN 
  purchases p
  ON ac.user_id = p.user_id
WHERE 
  p.purchase_time > ac.click_time
GROUP BY 
  ac.ad_id
ORDER BY 
  roas DESC;

~~~
2. Count Unique Converters Attributed to Each Campaign
   - `campaign_clicks(campaign_id, user_id, click_time)`
   - `conversions(user_id, conversion_time)`
   - Return the number of **unique users** who converted **after** clicking on each campaign.
~~~sql
select
  c.campaign_id,
  count(distinct c.user_id) as unique_converters
from
  campaign_clicks c
join
  conversions co
  on c.user_id = co.user_id
where
  c.click_time < co.conversion_time
group by
  c.campaign_id

~~~
4. 

