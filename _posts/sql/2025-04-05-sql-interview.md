---
layout: post
title:  "SQL Interview"
date:   2025-04-05 08:00:00 +0700
categories: [sql, coding, interview]
---

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
