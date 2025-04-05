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
3. 

