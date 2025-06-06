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
3. Meta Ads Ads SQL Scenario
   - Table: `meta_ads(ad_id, campaign_id, date, impressions, clicks, spend, conversions)`
   - Write a query to:
     - Compute CTR, CVR, and CPC per campaign. Be careful how we define these.
     - Return only campaigns with CTR > 2% and CPC < $1.
~~~sql
select
  campaign_id,
  SUM(clicks)*1.0 / SUM(impressions) as ctr,
  SUM(conversions)*1.0 / SUM(clicks) as cvr,
  SUM(spend)*1.0 / SUM(clicks) as cpc
from
  meta_ads
group by
  campaign_id
having
  SUM(clicks)*1.0 / SUM(impressions) > 0.02
  and SUM(spend)*1.0 / SUM(clicks) < 1.0
~~~

4. Find the distribution of posts made by users (i.e., 1000 users posted 1 time, 500 users posted 2 times, etc.)
  - `users(user_id, active_status, join_time)`
  - `posts(post_id, user_id, post_time)`
~~~sql
with cte as
  (
  select
    u.user_id,
    count(distinct post_id) as num_posts
  from users u
  left join posts p on u.user_id = p.user_id
  group by u.user_id
  )
select
  num_posts,
  count(*) as num_users
from
  cte
group by num_posts
~~~
5. 
6.   

