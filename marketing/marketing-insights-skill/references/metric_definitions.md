# Marketing Metric Definitions

## Acquisition Metrics

### CAC (Customer Acquisition Cost)
- **Formula:** Total Marketing & Sales Cost / Number of New Customers Acquired
- **Components:** Ad spend + Marketing salaries + Tools/Software + Agency fees + Sales costs
- **Interpretation:** Lower is better; should be recovered by LTV
- **Typical Range:** Varies by industry (₹500 - ₹5,00,000)

### CPL (Cost Per Lead)
- **Formula:** Total Marketing Spend / Number of Leads Generated
- **Interpretation:** Efficiency of lead generation; lower isn't always better if quality suffers
- **Quality Check:** Must evaluate alongside lead-to-customer conversion rate

### CPA (Cost Per Acquisition/Action)
- **Formula:** Total Campaign Cost / Number of Conversions
- **Interpretation:** Direct campaign efficiency measure
- **Use Case:** Campaign-level optimization

### CPC (Cost Per Click)
- **Formula:** Total Ad Spend / Total Clicks
- **Interpretation:** Traffic acquisition efficiency
- **Context:** Must evaluate with CTR and CVR for full picture

### CPM (Cost Per Mille)
- **Formula:** (Total Ad Spend / Total Impressions) × 1000
- **Interpretation:** Cost to reach 1,000 people
- **Use Case:** Brand awareness and reach campaigns

## Revenue & Value Metrics

### LTV (Lifetime Value) / CLV (Customer Lifetime Value)
- **Formula:** Average Purchase Value × Purchase Frequency × Average Customer Lifespan
- **Alternative:** Total Revenue from Customer Over Relationship
- **Interpretation:** Higher indicates better retention and monetization
- **Strategic Use:** Determines acceptable CAC ceiling

### ARPU (Average Revenue Per User)
- **Formula:** Total Revenue / Total Active Users
- **Interpretation:** Monetization efficiency per user
- **Time Period:** Typically monthly (Monthly ARPU)

### AOV (Average Order Value)
- **Formula:** Total Revenue / Total Orders
- **Interpretation:** Basket size/transaction value
- **Optimization Levers:** Upselling, cross-selling, bundling

### GMV (Gross Merchandise Value)
- **Formula:** Total Value of All Transactions (before deductions)
- **Use Case:** Marketplace and e-commerce total volume

## Efficiency Metrics

### ROAS (Return on Ad Spend)
- **Formula:** Revenue Attributed to Ads / Ad Spend
- **Interpretation:** >1x means revenue exceeds spend; >4x typically healthy
- **Expression:** Usually as Nx (e.g., 4.5x ROAS)

### ROI (Return on Investment)
- **Formula:** (Revenue - Total Marketing Cost) / Total Marketing Cost × 100
- **Interpretation:** Percentage return on marketing investment
- **Difference from ROAS:** Includes all marketing costs, not just ad spend

### MER (Marketing Efficiency Ratio)
- **Formula:** Total Revenue / Total Marketing Spend
- **Interpretation:** Holistic efficiency measure including organic
- **Also Known As:** Blended ROAS, Overall Marketing Efficiency

### LTV:CAC Ratio
- **Formula:** Lifetime Value / Customer Acquisition Cost
- **Healthy Range:** 3:1 to 5:1
- **Interpretation:**
  - <2:1 = Unsustainable (losing money)
  - 2:1-3:1 = Needs attention
  - 3:1-5:1 = Healthy
  - >5:1 = May be underinvesting in growth

### CAC Payback Period
- **Formula:** CAC / (ARPU × Gross Margin)
- **Interpretation:** Months to recover acquisition cost
- **Healthy Range:** <12 months for most businesses

## Engagement Metrics

### CTR (Click-Through Rate)
- **Formula:** (Clicks / Impressions) × 100
- **Interpretation:** Ad/content relevance and appeal
- **Benchmark:** Varies by channel (Search 3-5%, Display 0.3-0.8%)

### CVR (Conversion Rate)
- **Formula:** (Conversions / Visitors or Clicks) × 100
- **Interpretation:** Effectiveness at converting visitors to desired action
- **Types:** Site CVR, Landing Page CVR, Funnel Stage CVR

### Bounce Rate
- **Formula:** (Single-Page Sessions / Total Sessions) × 100
- **Interpretation:** Lower is generally better; indicates engagement
- **Context:** Depends on page purpose (blog vs landing page)

### Session Duration / Time on Site
- **Formula:** Total Time Spent / Number of Sessions
- **Interpretation:** Engagement depth
- **Consideration:** Quality of time matters more than raw duration

### Pages per Session
- **Formula:** Total Page Views / Total Sessions
- **Interpretation:** Content exploration depth

## Funnel Metrics

### Lead-to-MQL Rate
- **Formula:** (MQLs / Total Leads) × 100
- **Interpretation:** Lead qualification efficiency
- **Benchmark:** 15-30% for B2B

### MQL-to-SQL Rate
- **Formula:** (SQLs / MQLs) × 100
- **Interpretation:** Marketing-to-sales handoff quality
- **Benchmark:** 30-50% for B2B

### SQL-to-Opportunity Rate
- **Formula:** (Opportunities / SQLs) × 100
- **Interpretation:** Sales qualification effectiveness
- **Benchmark:** 50-70% for B2B

### Win Rate / Close Rate
- **Formula:** (Closed Won / Total Opportunities) × 100
- **Interpretation:** Sales effectiveness
- **Benchmark:** 20-35% for B2B

### Cart Abandonment Rate
- **Formula:** (Carts Created - Purchases) / Carts Created × 100
- **Interpretation:** Checkout friction indicator
- **Benchmark:** 60-80% is typical (lower is better)

## Comparison Computations

### Absolute Change
- **Formula:** Current Value - Previous Value
- **Expression:** +₹500 or -₹500

### Percentage Change
- **Formula:** (Current - Previous) / Previous × 100
- **Expression:** +15% or -8%
- **Guardrail:** If previous = 0, show absolute only

### Period-over-Period
- **MoM:** Month-over-Month
- **QoQ:** Quarter-over-Quarter
- **YoY:** Year-over-Year (most meaningful for seasonal businesses)

## Derived Insights

### Efficiency Trend
- **Calculation:** Compare current LTV:CAC vs previous
- **Interpretation:**
  - Improving: Current > Previous
  - Stable: Within 5% variance
  - Declining: Current < Previous by >5%

### Channel Efficiency Score
- **Calculation:** (ROAS × CVR) / (CAC / Industry Benchmark CAC)
- **Interpretation:** Normalized efficiency across channels

### Growth Efficiency
- **Calculation:** Revenue Growth Rate / CAC Growth Rate
- **Interpretation:** >1 = Efficient growth, <1 = Inefficient growth

## Guardrails

- If denominator is 0: Return null, note "insufficient data"
- If previous period is 0: Show absolute change only
- Negative values: Only valid for change calculations
- Percentage caps: CVR, CTR should not exceed 100%
- Ratio minimums: ROAS, LTV:CAC should be ≥ 0
