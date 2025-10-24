Dear [stakeholder name],

Here are the key Insights regarding your questions:

1️⃣ How much data does a subscription typically consume?

Typical Data Consumption depends on the granularity, here is at a global view:

- Median usage: ~298 MB per subscription period ( more insights about this in the next questions)
- High spread on usage across customers (many low-usage + some power users)
- 80% of subscriptions consume less than ~1,000 MB (see the **zoomed** graph below, the median )

![Cumulative Usage Distribution](./img/cumulative_dist.png)

**NB : Please note that the picture is zoomed due to the outliers. More on outliers later**

2️⃣ How does usage look like at different plan data allowances?

The Usage by Plan Type is significantly different among plans; Unlimited/Ultra Unlimited plans drive significantly higher consumption.
There is a clear correlation between plan allowances and actual usage.
In the other side, if you wonder if our Network provider have any impact on the usage, the answer is no; It has no measurable effect on usage patterns.

![Usage by Plan Type](./img/usage_by_plan.png)

_>>More in depth investigations can be done in this subject.<<_

3️⃣ Do subscriptions typically consume consistent amounts of data throughout their lifetime?

The usage consistency is can be measured by a consistency metric: coefficient of variation (CV).
I found that the CV is Moderately consistent overall (CV = 0.98) (better view on the graph bellow)
Furthermore, 43% of subscriptions show consistent usage patterns (CV ≤ 1)
![Consistency usage](./img/consistency_usage.png)

Here is a better graph through time:

![Consistency usage](./img/consistency_through_time.png)

Notice how the majority of the subscriptions become more consistent over time (excluding the outliers, the points outside the boxes - roight graph -).

4️⃣ ⚠️ Compare the retention pattern for the most recently launched project versus the two older ones.

Retention in the other side is well defined by
ACME Phone (newest project) shows significantly lower retention vs older projects
People Mobile & SmartDevices Inc. maintain 50%+ retention at period 16
ACME Phone drops faster, suggesting underlying issues

![Retention Red Flag](./img/retention.png)

Acme is the only project that shows high retention, while the others loose an increible amount ofclients in the first period.

🚨 Recommended Actions:

1. Its HIGHLY advisable to study the monetary side, ACME project could have higher retention but if the money side is close to zero then it addresses another niche.
1. Investigate if users churn due internal issues or due to influence from outside the company (also due to promotions, adversaries etc.).
1. Investigate why ACME Phone retention drop on 14th period- conduct user surveys, review pricing/features vs competitors
1. Check for technical issues (service quality, outages, speed, payment, etc)
1. Analyze customer support metrics and complaint trends
1. Consider promotional strategies that worked for older projects
1. Consider adding the financial perspective of promotions in long term.

Let me know if you would like me to dig deeper into any specific area.
