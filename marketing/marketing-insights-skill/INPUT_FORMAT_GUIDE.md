# Marketing Insights Skill - Input Format Guide

## Quick Reference: Data Types Required

| Analysis Type       | Required Data                     | Optional Data          |
|---------------------|-----------------------------------|------------------------|
| Basic Metrics       | CAC, CPL, or ROAS                 | LTV, CTR, CVR          |
| Efficiency Analysis | CAC + LTV                         | Spend, Revenue         |
| Channel Analysis    | Channel-wise spend & conversions  | Channel-wise revenue   |
| Funnel Analysis     | Stage counts (Leads → Won)        | Stage-wise breakdown   |
| Geographic Analysis | Location-wise funnel data         | Location-wise spend    |
| Cohort Analysis     | Cohort retention over time        | Cohort revenue, LTV    |

---

## Data Validation Rules

**IMPORTANT:** Your data must follow these rules for accurate analysis:

### Funnel Progression
Each funnel stage must be ≤ the previous stage:
```
Leads ≥ MQL ≥ SQL ≥ Won
```
**Invalid:** Won: 180, SQL: 108 (Won cannot exceed SQL)
**Valid:** Won: 90, SQL: 180 (90 ≤ 180)

### Segment Totals
Segment breakdowns must sum to the total:
```
Leads: 100 (Mumbai-50, Delhi-30, Bangalore-20) ✓ (50+30+20=100)
Leads: 100 (Mumbai-50, Delhi-30, Bangalore-25) ✗ (50+30+25=105≠100)
```

### Percentages
All rates must be 0-100%:
- Win Rate = Won ÷ SQL × 100
- If your Win Rate exceeds 100%, check your funnel counts

---

## RECOMMENDED: Complete Combined Input Format

For the most comprehensive analysis, provide all data types together. This enables full diagnostic analysis, cohort insights, segment breakdowns, and actionable recommendations.

### Full Combined Input Template (Copy & Customize)

```
[Month Year] Marketing Data:

=== CORE METRICS ===
- Total Spend: ₹[X]L
- Conversions: [#]
- Revenue: ₹[X]L
- CAC: ₹[X]
- CPL: ₹[X]
- LTV: ₹[X]
- ROAS: [X]x
- CTR: [X]%
- CVR: [X]%

=== CHANNEL BREAKDOWN ===
- Google: Spend ₹[X]L, Leads [#], Conversions [#], Revenue ₹[X]L
- Meta: Spend ₹[X]L, Leads [#], Conversions [#], Revenue ₹[X]L
- LinkedIn: Spend ₹[X]L, Leads [#], Conversions [#], Revenue ₹[X]L

=== FUNNEL BY GEOGRAPHY ===
Leads: [Total] (City1-[#], City2-[#], City3-[#])
MQL: [Total] (City1-[#], City2-[#], City3-[#])
SQL: [Total] (City1-[#], City2-[#], City3-[#])
Won: [Total] (City1-[#], City2-[#], City3-[#])

=== FUNNEL BY CHANNEL ===
Leads: [Total] (Google-[#], Meta-[#], LinkedIn-[#])
MQL: [Total] (Google-[#], Meta-[#], LinkedIn-[#])
SQL: [Total] (Google-[#], Meta-[#], LinkedIn-[#])
Won: [Total] (Google-[#], Meta-[#], LinkedIn-[#])

=== COHORT RETENTION ===
Jan cohort: [#] customers, M1 [X]%, M2 [X]%, M3 [X]%, M4 [X]%
Feb cohort: [#] customers, M1 [X]%, M2 [X]%, M3 [X]%
Mar cohort: [#] customers, M1 [X]%, M2 [X]%

=== COHORT REVENUE ===
Jan cohort: M1 ₹[X]L, M2 ₹[X]L, M3 ₹[X]L, M4 ₹[X]L
Feb cohort: M1 ₹[X]L, M2 ₹[X]L, M3 ₹[X]L
Mar cohort: M1 ₹[X]L, M2 ₹[X]L

=== COHORT BY CHANNEL ===
Google cohort: [#] customers, CAC ₹[X], M3 retention [X]%, LTV ₹[X]
Meta cohort: [#] customers, CAC ₹[X], M3 retention [X]%, LTV ₹[X]
LinkedIn cohort: [#] customers, CAC ₹[X], M3 retention [X]%, LTV ₹[X]

=== COMPARISON PERIOD ===
Previous Month:
- CAC: ₹[X]
- CPL: ₹[X]
- LTV: ₹[X]
- ROAS: [X]x
```

### Full Combined Input Example (Ready to Use)

```
Feb 2025 Marketing Data:

=== CORE METRICS ===
- Total Spend: ₹15L
- Conversions: 180
- Revenue: ₹72L
- CAC: ₹8,333
- CPL: ₹1,250
- LTV: ₹40,000
- ROAS: 4.8x
- CTR: 2.1%
- CVR: 15%

=== CHANNEL BREAKDOWN ===
- Google: Spend ₹6L, Leads 480, Conversions 90, Revenue ₹33L
- Meta: Spend ₹5L, Leads 400, Conversions 60, Revenue ₹21L
- LinkedIn: Spend ₹4L, Leads 320, Conversions 30, Revenue ₹12L

=== FUNNEL BY GEOGRAPHY ===
Leads: 1200 (Mumbai-540, Delhi-360, Bangalore-300)
MQL: 360 (Mumbai-180, Delhi-100, Bangalore-80)
SQL: 180 (Mumbai-90, Delhi-50, Bangalore-40)
Won: 90 (Mumbai-50, Delhi-25, Bangalore-15)

=== FUNNEL BY CHANNEL ===
Leads: 1200 (Google-480, Meta-400, LinkedIn-320)
MQL: 360 (Google-160, Meta-120, LinkedIn-80)
SQL: 180 (Google-80, Meta-60, LinkedIn-40)
Won: 90 (Google-45, Meta-30, LinkedIn-15)

=== COHORT RETENTION ===
Jan cohort: 50 customers, M1 90%, M2 78%, M3 68%, M4 62%
Feb cohort: 55 customers, M1 88%, M2 75%, M3 65%
Mar cohort: 45 customers, M1 82%, M2 68%

=== COHORT REVENUE ===
Jan cohort: M1 ₹5L, M2 ₹4.5L, M3 ₹4L, M4 ₹3.8L
Feb cohort: M1 ₹5.5L, M2 ₹4.8L, M3 ₹4.2L
Mar cohort: M1 ₹4.5L, M2 ₹3.8L

=== COHORT BY CHANNEL ===
Google cohort: 60 customers, CAC ₹16,000, M3 retention 72%, LTV ₹65,000
Meta cohort: 50 customers, CAC ₹22,000, M3 retention 58%, LTV ₹48,000
LinkedIn cohort: 40 customers, CAC ₹25,000, M3 retention 75%, LTV ₹72,000

=== COMPARISON PERIOD ===
Jan 2025:
- CAC: ₹7,500
- CPL: ₹1,100
- LTV: ₹38,000
- ROAS: 5.2x
```

### What Each Section Enables

| Section             | Analysis Enabled                                       |
|---------------------|--------------------------------------------------------|
| Core Metrics        | Health score, benchmark comparison, executive summary  |
| Channel Breakdown   | Channel performance analysis, budget reallocation      |
| Funnel by Geography | Geographic segment analysis, regional efficiency       |
| Funnel by Channel   | Channel funnel analysis, source quality                |
| Cohort Retention    | Retention curves, cohort health, churn patterns        |
| Cohort Revenue      | LTV projection, revenue decay analysis                 |
| Cohort by Channel   | Channel quality scoring, acquisition source ROI        |
| Comparison Period   | Trend analysis, MoM/YoY changes                        |

### Compact Shorthand Version

For quick input, use this compact syntax:

```
Metrics: CAC=8333 CPL=1250 LTV=40000 ROAS=4.8 CTR=2.1 CVR=15
Channels: G=6L/90conv/33Lrev | M=5L/60conv/21Lrev | L=4L/30conv/12Lrev
Funnel: Imp=500K→Click=15K→Lead=1200→MQL=360→SQL=180→Won=90
Geo: Leads(Mum-540,Del-360,Blr-300) MQL(Mum-180,Del-100,Blr-80) SQL(Mum-90,Del-50,Blr-40) Won(Mum-50,Del-25,Blr-15)
Cohorts: Jan(50,90/78/68/62%) Feb(55,88/75/65%) Mar(45,82/68%)
ChanCohort: G(60,16K,72%,65K) M(50,22K,58%,48K) L(40,25K,75%,72K)
vs: CAC=7500 CPL=1100 LTV=38000 ROAS=5.2
```

---

## Individual Input Formats

Below are individual formats if you don't have all data types available.

---

## INPUT FORMAT 1: Basic Marketing Metrics

### Minimum Required
```
CAC: ₹8,000
CPL: ₹1,200
```

### Recommended
```
CAC: ₹8,000
CPL: ₹1,200
LTV: ₹40,000
ROAS: 4.5x
CTR: 2.5%
CVR: 12%
```

### Full Metrics Input
```
Feb 2025 Marketing Metrics:

Acquisition Metrics:
- CAC (Customer Acquisition Cost): ₹8,000
- CPL (Cost Per Lead): ₹1,200
- CPA (Cost Per Acquisition): ₹8,000
- CPC (Cost Per Click): ₹25

Revenue Metrics:
- LTV (Lifetime Value): ₹40,000
- ARPU (Avg Revenue Per User): ₹3,500/month
- AOV (Average Order Value): ₹2,500

Efficiency Metrics:
- ROAS: 4.5x
- LTV:CAC Ratio: 5:1
- CAC Payback: 2.3 months

Engagement Metrics:
- CTR: 2.5%
- CVR: 12%
- Bounce Rate: 45%

Totals:
- Total Spend: ₹15L
- Total Revenue: ₹72L
- Total Conversions: 180
- Total Leads: 1,200
```

---

## INPUT FORMAT 2: Period Comparison (MoM / YoY)

### Simple Comparison
```
Feb vs Jan 2025:
- CAC: ₹8,000 vs ₹7,200
- CPL: ₹1,200 vs ₹1,100
- LTV: ₹40,000 vs ₹38,000
- ROAS: 4.5x vs 5.0x
```

### Detailed Comparison
```
Current Period: Feb 2025
Previous Period: Jan 2025

| Metric      | Feb 2025  | Jan 2025  |
|-------------|-----------|-----------|
| Spend       | ₹15L      | ₹12L      |
| Leads       | 1,200     | 1,000     |
| Conversions | 180       | 160       |
| Revenue     | ₹72L      | ₹60L      |
| CAC         | ₹8,333    | ₹7,500    |
| CPL         | ₹1,250    | ₹1,200    |
| LTV         | ₹40,000   | ₹38,000   |
| ROAS        | 4.8x      | 5.0x      |
```

---

## INPUT FORMAT 3: Channel Breakdown

### Simple Channel Format
```
Channel Performance:
- Google Ads: Spend ₹6L, Conversions 90, Revenue ₹33L
- Meta Ads: Spend ₹5L, Conversions 60, Revenue ₹21L
- LinkedIn: Spend ₹4L, Conversions 30, Revenue ₹12L
```

### Detailed Channel Format
```
Channel Performance - Feb 2025:

| Channel    | Spend   | Impressions | Clicks | Leads | Conversions | Revenue |
|------------|---------|-------------|--------|-------|-------------|---------|
| Google Ads | ₹6L     | 250,000     | 7,500  | 480   | 90          | ₹33L    |
| Meta Ads   | ₹5L     | 400,000     | 5,000  | 420   | 60          | ₹21L    |
| LinkedIn   | ₹4L     | 80,000      | 400    | 200   | 30          | ₹12L    |
| Email      | ₹0.5L   | -           | 2,000  | 100   | 15          | ₹6L     |
| Total      | ₹15.5L  | 730,000     | 14,900 | 1,200 | 195         | ₹72L    |
```

### Channel with Calculated Metrics
```
Channel Metrics - Feb 2025:

| Channel    | Spend | Conv | CAC     | CPL    | ROAS | CTR   | CVR |
|------------|-------|------|---------|--------|------|-------|-----|
| Google Ads | ₹6L   | 90   | ₹6,667  | ₹1,250 | 5.5x | 3.0%  | 18% |
| Meta Ads   | ₹5L   | 60   | ₹8,333  | ₹1,190 | 4.2x | 1.25% | 14% |
| LinkedIn   | ₹4L   | 30   | ₹13,333 | ₹2,000 | 3.0x | 0.5%  | 10% |
```

---

## INPUT FORMAT 4: Funnel Data

### Simple Funnel
```
Funnel - Feb 2025:
Impressions: 500K → Clicks: 15K → Leads: 1,200 → MQL: 360 → SQL: 108 → Won: 36
```

### Detailed Funnel
```
Sales Funnel - Feb 2025:

| Stage         | Count   | Conversion Rate |
|---------------|---------|-----------------|
| Impressions   | 500,000 | -               |
| Clicks        | 15,000  | 3.0% CTR        |
| Visitors      | 14,000  | 93.3%           |
| Leads         | 1,200   | 8.6%            |
| MQL           | 360     | 30%             |
| SQL           | 108     | 30%             |
| Opportunities | 65      | 60%             |
| Won           | 36      | 55%             |

Overall Conversion: 0.24% (Impression to Won)
Lead to Won: 3.0%
```

---

## INPUT FORMAT 5: Funnel with Segment Breakdown

### Geographic Breakdown
```
Funnel by City - Feb 2025:

| Stage       | Total | Mumbai | Goa | Bangalore | Delhi |
|-------------|-------|--------|-----|-----------|-------|
| Leads       | 100   | 45     | 30  | 15        | 10    |
| Site Visits | 40    | 20     | 12  | 5         | 3     |
| MQL         | 25    | 12     | 8   | 3         | 2     |
| SQL         | 15    | 8      | 5   | 1         | 1     |
| Won         | 10    | 6      | 3   | 1         | 0     |
```

### Shorthand Format
```
Leads: 100 (Mumbai-45, Goa-30, Bangalore-15, Delhi-10)
Site Visits: 40 (Mumbai-20, Goa-12, Bangalore-5, Delhi-3)
MQL: 25 (Mumbai-12, Goa-8, Bangalore-3, Delhi-2)
SQL: 15 (Mumbai-8, Goa-5, Bangalore-1, Delhi-1)
Won: 10 (Mumbai-6, Goa-3, Bangalore-1, Delhi-0)
```

### Channel-wise Funnel Breakdown
```
Funnel by Channel - Feb 2025:

| Stage | Total | Google | Meta  | LinkedIn | Organic |
|-------|-------|--------|-------|----------|---------|
| Leads | 200   | 80     | 70    | 30       | 20      |
| MQL   | 60    | 28     | 18    | 10       | 4       |
| SQL   | 24    | 12     | 6     | 4        | 2       |
| Won   | 12    | 6      | 3     | 2        | 1       |
| Spend | ₹10L  | ₹4L    | ₹3.5L | ₹2.5L    | ₹0      |
```

---

## INPUT FORMAT 6: Geographic Performance

### Simple Format
```
Performance by City:
- Mumbai: 50 leads, 6 conversions, Spend ₹4L
- Delhi: 30 leads, 3 conversions, Spend ₹2.5L
- Bangalore: 20 leads, 1 conversion, Spend ₹2L
```

### Detailed Format
```
Geographic Performance - Feb 2025:

| City      | Leads | Conv | CVR   | Spend  | CPL     | CAC       | Revenue | ROAS |
|-----------|-------|------|-------|--------|---------|-----------|---------|------|
| Mumbai    | 50    | 6    | 12%   | ₹4L    | ₹8,000  | ₹66,667   | ₹24L    | 6.0x |
| Delhi     | 30    | 3    | 10%   | ₹2.5L  | ₹8,333  | ₹83,333   | ₹12L    | 4.8x |
| Bangalore | 20    | 1    | 5%    | ₹2L    | ₹10,000 | ₹2,00,000 | ₹4L     | 2.0x |
| Goa       | 15    | 2    | 13%   | ₹1L    | ₹6,667  | ₹50,000   | ₹8L     | 8.0x |
| Total     | 115   | 12   | 10.4% | ₹9.5L  | ₹8,261  | ₹79,167   | ₹48L    | 5.1x |
```

---

## INPUT FORMAT 7: Cohort Analysis

### Retention by Acquisition Month
```
Cohort Retention Analysis - Q1 2025:

| Cohort   | Customers | CAC     | M1  | M2  | M3  | M4  | M5  | M6  |
|----------|-----------|---------|-----|-----|-----|-----|-----|-----|
| Jan 2025 | 100       | ₹15,000 | 92% | 80% | 70% | 62% | 55% | 50% |
| Feb 2025 | 120       | ₹18,000 | 88% | 75% | 65% | 58% | -   | -   |
| Mar 2025 | 90        | ₹22,000 | 82% | 68% | 60% | -   | -   | -   |
| Apr 2025 | 110       | ₹20,000 | 85% | 72% | -   | -   | -   | -   |
```

### Cohort Revenue Progression
```
Cohort Revenue - Q1 2025:

| Cohort   | M1   | M2    | M3    | M4    | M5    | M6    | Total  |
|----------|------|-------|-------|-------|-------|-------|--------|
| Jan 2025 | ₹10L | ₹8.5L | ₹7.2L | ₹6.5L | ₹5.8L | ₹5.2L | ₹43.2L |
| Feb 2025 | ₹12L | ₹9.8L | ₹8.1L | ₹7.0L | -     | -     | ₹36.9L |
| Mar 2025 | ₹9L  | ₹7.2L | ₹5.8L | -     | -     | -     | ₹22L   |
```

### Cohort by Acquisition Channel
```
Channel Cohort Analysis:

| Channel  | Customers | CAC     | M1 Ret | M3 Ret | M6 Ret | LTV     | LTV:CAC |
|----------|-----------|---------|--------|--------|--------|---------|---------|
| Google   | 150       | ₹12,000 | 90%    | 72%    | 58%    | ₹65,000 | 5.4:1   |
| Meta     | 120       | ₹18,000 | 85%    | 62%    | 45%    | ₹48,000 | 2.7:1   |
| LinkedIn | 80        | ₹25,000 | 92%    | 78%    | 68%    | ₹85,000 | 3.4:1   |
| Organic  | 60        | ₹5,000  | 95%    | 82%    | 72%    | ₹92,000 | 18.4:1  |
```

### Cohort by Customer Segment
```
Segment Cohort Analysis:

| Segment    | Customers | CAC     | M3 Ret | LTV       | Payback  |
|------------|-----------|---------|--------|-----------|----------|
| Enterprise | 30        | ₹80,000 | 90%    | ₹5,00,000 | 2 months |
| Mid-Market | 80        | ₹35,000 | 75%    | ₹1,50,000 | 3 months |
| SMB        | 150       | ₹12,000 | 60%    | ₹45,000   | 4 months |
| Startup    | 50        | ₹8,000  | 50%    | ₹25,000   | 5 months |
```

---

## INPUT FORMAT 8: Combined Full Analysis

### Complete Input Example
```
MARKETING PERFORMANCE REPORT - Feb 2025

=== SUMMARY METRICS ===
Total Spend: ₹15L
Total Leads: 1,200
Total Conversions: 180
Total Revenue: ₹72L
CAC: ₹8,333
CPL: ₹1,250
LTV: ₹40,000
ROAS: 4.8x
LTV:CAC: 4.8:1

=== CHANNEL BREAKDOWN ===
| Channel  | Spend | Leads | Conv | Revenue |
|----------|-------|-------|------|---------|
| Google   | ₹6L   | 480   | 90   | ₹33L    |
| Meta     | ₹5L   | 420   | 60   | ₹21L    |
| LinkedIn | ₹4L   | 200   | 30   | ₹12L    |
| Organic  | -     | 100   | 15   | ₹6L     |

=== FUNNEL BY GEOGRAPHY ===
| Stage       | Total | Mumbai | Goa | Bangalore |
|-------------|-------|--------|-----|-----------|
| Leads       | 100   | 45     | 30  | 25        |
| Site Visits | 40    | 20     | 12  | 8         |
| MQL         | 25    | 12     | 8   | 5         |
| SQL         | 15    | 8      | 5   | 2         |
| Won         | 10    | 6      | 3   | 1         |

=== COHORT DATA ===
Retention by Month:
- Jan 2025: 50 customers | M1: 90% | M2: 78% | M3: 68%
- Feb 2025: 55 customers | M1: 88% | M2: 75% | M3: 65%
- Mar 2025: 45 customers | M1: 82% | M2: 68%

Channel Cohort LTV:
- Google: LTV ₹65,000, M3 retention 72%
- Meta: LTV ₹48,000, M3 retention 58%
- LinkedIn: LTV ₹72,000, M3 retention 75%

=== COMPARISON (vs Jan 2025) ===
| Metric | Feb    | Jan    | Change |
|--------|--------|--------|--------|
| CAC    | ₹8,333 | ₹7,500 | +11%   |
| CPL    | ₹1,250 | ₹1,100 | +14%   |
| ROAS   | 4.8x   | 5.2x   | -8%    |
| Conv   | 180    | 160    | +12.5% |
```

---

## QUICK INPUT TEMPLATES

### Template 1: Minimum Viable Input
```
CAC: ₹[X]
LTV: ₹[X]
Spend: ₹[X]
Conversions: [X]
```

### Template 2: Channel Analysis
```
[Channel 1]: Spend ₹[X], Conversions [X], Revenue ₹[X]
[Channel 2]: Spend ₹[X], Conversions [X], Revenue ₹[X]
[Channel 3]: Spend ₹[X], Conversions [X], Revenue ₹[X]
```

### Template 3: Funnel with Breakdown
```
Leads: [Total] ([Segment1]-[X], [Segment2]-[X], [Segment3]-[X])
MQL: [Total] ([Segment1]-[X], [Segment2]-[X], [Segment3]-[X])
SQL: [Total] ([Segment1]-[X], [Segment2]-[X], [Segment3]-[X])
Won: [Total] ([Segment1]-[X], [Segment2]-[X], [Segment3]-[X])
```

### Template 4: Cohort Retention
```
[Month] Cohort: [X] customers
- M1 retention: [X]%
- M2 retention: [X]%
- M3 retention: [X]%
- LTV: ₹[X]
```

---

## METRIC DEFINITIONS (What to Provide)

| Metric        | Definition                 | How to Calculate                            |
|---------------|----------------------------|---------------------------------------------|
| **CAC**       | Customer Acquisition Cost  | Total Marketing Spend ÷ New Customers       |
| **CPL**       | Cost Per Lead              | Total Marketing Spend ÷ Total Leads         |
| **LTV**       | Lifetime Value             | Avg Revenue per Customer × Avg Lifespan     |
| **ROAS**      | Return on Ad Spend         | Revenue ÷ Ad Spend                          |
| **CTR**       | Click-Through Rate         | Clicks ÷ Impressions × 100                  |
| **CVR**       | Conversion Rate            | Conversions ÷ Clicks (or Visitors) × 100    |
| **MQL**       | Marketing Qualified Lead   | Leads meeting marketing criteria            |
| **SQL**       | Sales Qualified Lead       | Leads meeting sales criteria                |
| **Retention** | % customers still active   | Active Customers ÷ Starting Customers × 100 |

---

## TIPS FOR BEST RESULTS

1. **Include comparison data** - MoM or YoY data enables trend analysis
2. **Provide channel breakdown** - Enables optimization recommendations
3. **Include segment data** - Geographic or channel funnel breakdown reveals opportunities
4. **Add cohort data** - Shows customer quality over time
5. **Use consistent currency** - Stick to ₹ or $ throughout
6. **Specify time period** - Always mention the date range
7. **Include both spend AND revenue** - Enables ROI calculations

---

## EXAMPLE: COPY-PASTE READY

```
Feb 2025 Marketing Data:

Metrics:
- Total Spend: ₹15L
- CAC: ₹8,333
- CPL: ₹1,250
- LTV: ₹40,000
- ROAS: 4.8x

Channel Breakdown:
- Google: Spend ₹6L, Conversions 90, Revenue ₹33L
- Meta: Spend ₹5L, Conversions 60, Revenue ₹21L
- LinkedIn: Spend ₹4L, Conversions 30, Revenue ₹12L

Funnel by City:
- Leads: 100 (Mumbai-45, Goa-30, Bangalore-25)
- MQL: 25 (Mumbai-12, Goa-8, Bangalore-5)
- SQL: 15 (Mumbai-8, Goa-5, Bangalore-2)
- Won: 10 (Mumbai-6, Goa-3, Bangalore-1)

Cohort Retention:
- Jan 2025: 50 customers, M1: 90%, M2: 78%, M3: 68%
- Feb 2025: 55 customers, M1: 88%, M2: 75%, M3: 65%

vs Jan 2025:
- CAC: ₹7,500 → ₹8,333 (+11%)
- ROAS: 5.2x → 4.8x (-8%)
```
