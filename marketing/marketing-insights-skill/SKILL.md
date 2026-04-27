---
name: marketing-insights-skill
description: Marketing metrics analyzer that transforms calculated KPIs (CAC, CPL, ROAS, LTV, etc.) into actionable business insights. Auto-triggers when users provide marketing metrics data. Applies industry benchmarks, identifies performance patterns, diagnoses issues, and generates prioritized recommendations for marketing optimization.
---

# Marketing Metrics Insights Analyzer - Production Skill

## ACTIVATION TRIGGERS

This skill **auto-activates** when the user provides:
- Marketing metrics: CAC, CPL, CPA, ROAS, LTV, CTR, CVR, MQL, SQL, etc.
- Advertising data: spend, impressions, clicks, conversions, revenue
- Channel performance data: paid search, social, email, display metrics
- Campaign performance metrics with conversion data
- Keywords: marketing ROI, customer acquisition, campaign performance, ad spend analysis, channel attribution
- File uploads containing marketing KPIs or advertising metrics

## BUSINESS CONTEXT

### Marketing Efficiency Framework
- **Customer Acquisition Cost (CAC):** Total cost to acquire one customer
- **Cost Per Lead (CPL):** Cost to generate one lead
- **Lifetime Value (LTV):** Total revenue from a customer over relationship
- **Return on Ad Spend (ROAS):** Revenue generated per rupee/dollar spent
- **Marketing Efficiency Ratio (MER):** Total revenue / Total marketing spend

### Business Rules Applied to Analysis

1. **LTV:CAC Ratio is King**
   - Healthy ratio: 3:1 or higher
   - Below 3:1 indicates acquisition inefficiency or poor retention
   - Above 5:1 may indicate underinvestment in growth

2. **Payback Period Matters**
   - CAC should be recovered within 12 months for most businesses
   - Longer payback = higher risk, requires stronger LTV confidence
   - SaaS typically: 12-18 months acceptable

3. **Channel Attribution Complexity**
   - First-touch vs last-touch vs multi-touch attribution
   - Assisted conversions often undervalued
   - Brand campaigns support performance campaigns

4. **Marginal Returns**
   - Each additional rupee spent has diminishing returns
   - Saturation curves differ by channel
   - Efficiency vs scale trade-off

5. **Quality vs Quantity Trade-off**
   - Lower CPL may mean lower quality leads
   - MQL-to-SQL conversion reveals true lead quality
   - Focus on cost per qualified opportunity, not just cost per lead

6. **Seasonality Considerations**
   - Industry-specific peaks and valleys
   - Year-over-year comparison more meaningful than MoM for seasonal businesses
   - Budget allocation should follow demand patterns

## INDUSTRY BENCHMARKS

### Acquisition Cost Benchmarks

| Industry | CAC Range | CPL Range | Notes |
|----------|-----------|-----------|-------|
| SaaS B2B | ₹15,000 - ₹1,50,000 | ₹2,000 - ₹15,000 | Varies by deal size |
| E-commerce | ₹500 - ₹5,000 | ₹50 - ₹500 | Category dependent |
| D2C Brands | ₹800 - ₹3,000 | ₹100 - ₹800 | Higher for premium |
| Real Estate | ₹50,000 - ₹5,00,000 | ₹5,000 - ₹50,000 | High ticket size |
| EdTech | ₹2,000 - ₹25,000 | ₹200 - ₹2,000 | Course value dependent |
| FinTech | ₹1,000 - ₹10,000 | ₹100 - ₹1,000 | Product complexity |

### Efficiency Ratio Benchmarks

| Metric | Healthy | Needs Attention | Critical |
|--------|---------|-----------------|----------|
| LTV:CAC | > 3:1 | 2:1 - 3:1 | < 2:1 |
| ROAS | > 4x | 2x - 4x | < 2x |
| MER | > 5x | 3x - 5x | < 3x |
| CAC Payback | < 12 months | 12-18 months | > 18 months |

### Channel Performance Benchmarks

| Channel | Avg CTR | Avg CVR | Avg CPC | Notes |
|---------|---------|---------|---------|-------|
| Google Search | 3-5% | 3-8% | ₹20-200 | Intent-driven |
| Google Display | 0.3-0.8% | 0.5-2% | ₹5-50 | Awareness |
| Facebook/Meta | 0.8-1.5% | 2-5% | ₹10-100 | Targeting-driven |
| LinkedIn | 0.3-0.7% | 2-5% | ₹100-500 | B2B focused |
| Email | 15-25% open | 2-5% click | N/A | Owned channel |
| Organic Search | N/A | 2-4% | N/A | Long-term investment |

### Funnel Stage Benchmarks

| Stage Transition | B2B SaaS | E-commerce | D2C | Real Estate |
|------------------|----------|------------|-----|-------------|
| Visitor → Lead | 2-5% | 1-3% | 3-8% | 1-3% |
| Lead → MQL | 15-30% | N/A | N/A | 10-20% |
| MQL → SQL | 30-50% | N/A | N/A | 20-35% |
| SQL → Opportunity | 50-70% | N/A | N/A | 40-60% |
| Opportunity → Close | 20-35% | N/A | N/A | 5-15% |
| Cart → Purchase | N/A | 65-80% | 60-75% | N/A |

### Performance Status Indicators

- **Excellent:** >20% above benchmark
- **Strong:** Within or above benchmark
- **Moderate:** 0-15% below benchmark
- **Needs Attention:** 15-30% below benchmark
- **Critical:** >30% below benchmark

## CORE FUNCTIONALITY

### Input Metrics Accepted

**Acquisition Metrics:**
- CAC (Customer Acquisition Cost)
- CPL (Cost Per Lead)
- CPA (Cost Per Acquisition/Action)
- CPC (Cost Per Click)
- CPM (Cost Per Mille/Thousand Impressions)

**Revenue Metrics:**
- LTV (Lifetime Value) / CLV (Customer Lifetime Value)
- ARPU (Average Revenue Per User)
- AOV (Average Order Value)
- Revenue, GMV

**Efficiency Metrics:**
- ROAS (Return on Ad Spend)
- ROI (Return on Investment)
- MER (Marketing Efficiency Ratio)
- LTV:CAC Ratio
- CAC Payback Period

**Engagement Metrics:**
- CTR (Click-Through Rate)
- CVR (Conversion Rate)
- Bounce Rate
- Session Duration
- Pages per Session

**Funnel Metrics:**
- Impressions, Clicks, Conversions
- MQL, SQL, Opportunities, Wins
- Lead-to-Customer Rate
- Pipeline Value, Win Rate

**Channel/Campaign Data:**
- By channel: Paid Search, Social, Display, Email, Affiliate, Organic
- By campaign: Brand, Performance, Retargeting, Awareness
- By geography, device, audience segment

**Segment Breakdown Data:**
- By Geography: City, State, Region, Country
- By Source: Organic, Paid, Referral, Direct
- By Channel: Google, Meta, LinkedIn, Email, etc.
- By Campaign: Brand, Performance, Retargeting
- By Device: Desktop, Mobile, Tablet
- By Time: Day, Week, Month, Quarter

**Cohort Analysis Data:**
- By Acquisition Month: Jan cohort, Feb cohort, etc.
- By Acquisition Channel: Google cohort, Meta cohort, etc.
- By Customer Segment: Enterprise, SMB, Startup, etc.
- By Product/Plan: Basic, Pro, Enterprise tier
- By Geography Cohort: Region-based customer groups
- Retention metrics by cohort over time
- Revenue/LTV progression by cohort
- Churn patterns by acquisition source

### Analysis Approach

1. **Metric Health Assessment** - Compare each metric against industry benchmarks
2. **Trend Analysis** - Identify improving/declining patterns
3. **Efficiency Analysis** - Evaluate spend effectiveness
4. **Channel Attribution** - Understand channel contribution and interplay
5. **Bottleneck Detection** - Find funnel weak points
6. **Opportunity Identification** - Highlight optimization opportunities
7. **Risk Assessment** - Flag concerning trends
8. **Action Prioritization** - Rank recommendations by impact

## INPUT HANDLING

### Accepted Formats

**Text Format:**
```
"CAC: ₹2,500, CPL: ₹350, LTV: ₹12,000, ROAS: 4.2x, CTR: 2.8%, CVR: 3.5%"
"Google Ads: Spend ₹5L, Clicks 15K, Conversions 450, Revenue ₹25L"
```

**Comparison Format:**
```
"Feb vs Jan: CAC ₹2,500 vs ₹2,200, CPL ₹350 vs ₹380, ROAS 4.2x vs 3.8x"
"Current: CAC=2500 LTV=12000 ROAS=4.2, Prior: CAC=2200 LTV=11500 ROAS=3.8"
```

**Channel Breakdown Format:**
```
"Paid Search: CAC ₹1,800 | Social: CAC ₹3,200 | Display: CAC ₹4,500"
"Channel performance - Google=ROAS 5.2x, Meta=ROAS 3.8x, LinkedIn=ROAS 2.1x"
```

**Funnel Format:**
```
"Impressions: 500K → Clicks: 15K → Leads: 2,000 → MQL: 600 → SQL: 180 → Won: 36"
```

**Funnel with Segment Breakdown Format:**
```
"Leads: 100 (Mumbai-45, Goa-30, Bangalore-25)"
"MQL: 50 (Mumbai-25, Goa-15, Bangalore-10)"
"Conversions: 10 (Mumbai-6, Goa-3, Bangalore-1)"
```

**Combined Metrics + Funnel Format:**
```
"Total Spend: ₹10L | Leads: 200 (Google-80, Meta-70, LinkedIn-50) | MQL: 60 | SQL: 18 | Won: 5
CAC: ₹2L | CPL: ₹5,000 | LTV: ₹8L | ROAS: 4x"
```

**Geographic Breakdown Format:**
```
"Leads by City: Mumbai=50 (CPL ₹400), Delhi=30 (CPL ₹550), Bangalore=20 (CPL ₹480)"
"Conversions by Region: North-40%, South-35%, West-20%, East-5%"
```

**Cohort Analysis Format:**
```
"Cohort by Acquisition Month:
- Jan 2025: 100 customers, Month 1 retention 85%, Month 2: 70%, Month 3: 60%
- Feb 2025: 120 customers, Month 1 retention 88%, Month 2: 72%
- Mar 2025: 90 customers, Month 1 retention 82%"

"Cohort by Channel:
- Google cohort: 50 customers, LTV ₹45,000, Retention M3: 65%
- Meta cohort: 40 customers, LTV ₹38,000, Retention M3: 55%
- LinkedIn cohort: 30 customers, LTV ₹52,000, Retention M3: 70%"

"Cohort Revenue Progression:
- Jan cohort: M1 ₹5L, M2 ₹4.2L, M3 ₹3.8L, M4 ₹3.5L
- Feb cohort: M1 ₹6L, M2 ₹5.1L, M3 ₹4.5L"
```

**File Formats:**
- CSV/Excel with columns: Channel, Spend, Impressions, Clicks, Conversions, Revenue
- JSON: `{"cac": 2500, "cpl": 350, "ltv": 12000, "roas": 4.2}`

### Missing Data Handling

- If LTV not provided: Skip LTV:CAC analysis, note "LTV data required for full efficiency analysis"
- If channel breakdown missing: Analyze aggregate metrics only
- If historical data missing: Provide benchmark comparison without trend analysis
- If funnel stages missing: Focus on provided conversion points
- If spend data missing: Skip ROI/ROAS calculations, note "Spend data needed for efficiency analysis"

### Data Validation Rules

**CRITICAL: Always validate input data before analysis. Flag errors clearly.**

**Funnel Progression Validation:**
- Each stage must be ≤ previous stage (Leads ≥ MQL ≥ SQL ≥ Won)
- If Won > SQL or SQL > MQL: Flag as "⚠️ DATA ERROR: Funnel counts invalid - [Stage X] cannot exceed [Stage Y]"
- Do NOT proceed with conversion rate calculations on invalid data

**Percentage Validation:**
- All rates (CVR, CTR, retention) must be 0-100%
- Win Rate = Won ÷ SQL × 100 (must be ≤ 100%)
- If calculated rate > 100%: Flag as "⚠️ DATA ERROR: [Rate] exceeds 100% - verify input counts"

**Segment Sum Validation:**
- Segment breakdowns must sum to total
- If Mumbai + Delhi + Bangalore ≠ Total Leads: Flag as "⚠️ DATA WARNING: Segment sum ([X]) ≠ Total ([Y])"

**Cross-Reference Validation:**
- Conversions across all channels should equal total conversions
- Spend across all channels should equal total spend
- If mismatch > 5%: Flag as "⚠️ DATA WARNING: Channel totals don't match aggregate"

**When Data Errors Found:**
1. List all errors at the top of the report under "DATA QUALITY ISSUES"
2. Skip calculations that would produce invalid results
3. Provide analysis only on validated data
4. Recommend data correction before full analysis

## OUTPUT FORMAT

### Text Output
The skill generates a comprehensive insights report in the exact format shown below.

## EXACT OUTPUT FORMAT (NEVER DEVIATE)

```
[Date Range] Marketing Metrics Insights Report

BUSINESS CONTEXT: [Industry/Business Type]
ANALYSIS PERIOD: [Current Period] vs [Comparison Period]

EXECUTIVE SUMMARY

| Metric    | Value     | Benchmark       | Status           | Trend   |
|-----------|-----------|-----------------|------------------|---------|
| CAC       | ₹[X]      | ₹[benchmark]    | [Status]         | [↑/↓/→] |
| CPL       | ₹[X]      | ₹[benchmark]    | [Status]         | [↑/↓/→] |
| LTV       | ₹[X]      | ₹[benchmark]    | [Status]         | [↑/↓/→] |
| ROAS      | [X]x      | [benchmark]x    | [Status]         | [↑/↓/→] |
| LTV:CAC   | [X]:1     | 3:1             | [Status]         | [↑/↓/→] |

HEALTH SCORE: [X]/100
[One-line summary of overall marketing health]

Score Breakdown:
| Component         | Weight   | Score   | Calculation                                    |
|-------------------|----------|---------|------------------------------------------------|
| LTV:CAC Ratio     | 30 pts   | [X]/30  | >5:1=30, 4-5:1=25, 3-4:1=20, 2-3:1=10, <2:1=0  |
| ROAS              | 20 pts   | [X]/20  | >5x=20, 4-5x=16, 3-4x=12, 2-3x=8, <2x=0       |
| CAC vs Benchmark  | 20 pts   | [X]/20  | >20% below=20, at bench=15, 0-15% above=10    |
| Funnel Conversion | 15 pts   | [X]/15  | Above bench=15, at bench=12, 0-15% below=8    |
| Trend Direction   | 15 pts   | [X]/15  | Improving=15, Stable=10, Declining=5          |
| **Total**         | 100 pts  | [X]/100 | Sum of above                                   |

ACQUISITION EFFICIENCY ANALYSIS

| Metric   | Current   | Previous  | Change    | % Change  | Assessment  |
|----------|-----------|-----------|-----------|-----------|-------------|
| CAC      | ₹[X]      | ₹[X]      | [+/-₹X]   | [+/-X%]   | [Status]    |
| CPL      | ₹[X]      | ₹[X]      | [+/-₹X]   | [+/-X%]   | [Status]    |
| CPA      | ₹[X]      | ₹[X]      | [+/-₹X]   | [+/-X%]   | [Status]    |
| CPC      | ₹[X]      | ₹[X]      | [+/-₹X]   | [+/-X%]   | [Status]    |

Acquisition Insight: [Key finding about acquisition efficiency]

REVENUE & VALUE ANALYSIS

| Metric   | Current   | Previous  | Change    | % Change  | Assessment  |
|----------|-----------|-----------|-----------|-----------|-------------|
| LTV      | ₹[X]      | ₹[X]      | [+/-₹X]   | [+/-X%]   | [Status]    |
| ARPU     | ₹[X]      | ₹[X]      | [+/-₹X]   | [+/-X%]   | [Status]    |
| AOV      | ₹[X]      | ₹[X]      | [+/-₹X]   | [+/-X%]   | [Status]    |
| Revenue  | ₹[X]      | ₹[X]      | [+/-₹X]   | [+/-X%]   | [Status]    |

Value Insight: [Key finding about customer value]

LTV:CAC EFFICIENCY MATRIX

| Segment      | LTV       | CAC       | Ratio   | Payback   | Health     | Action     |
|--------------|-----------|-----------|---------|-----------|------------|------------|
| Overall      | ₹[X]      | ₹[X]      | [X]:1   | [X] mo    | [Status]   | [Action]   |
| [Channel 1]  | ₹[X]      | ₹[X]      | [X]:1   | [X] mo    | [Status]   | [Action]   |
| [Channel 2]  | ₹[X]      | ₹[X]      | [X]:1   | [X] mo    | [Status]   | [Action]   |
| [Channel 3]  | ₹[X]      | ₹[X]      | [X]:1   | [X] mo    | [Status]   | [Action]   |

Efficiency Insight: [Key finding about marketing efficiency]

CHANNEL PERFORMANCE ANALYSIS (if data provided)

| Channel      | Spend     | Conv  | CAC       | ROAS  | CVR   | Efficiency | Action     |
|--------------|-----------|-------|-----------|-------|-------|------------|------------|
| [Channel 1]  | ₹[X]      | [#]   | ₹[X]      | [X]x  | [X%]  | High/Med   | Scale      |
| [Channel 2]  | ₹[X]      | [#]   | ₹[X]      | [X]x  | [X%]  | High/Med   | Maintain   |
| [Channel 3]  | ₹[X]      | [#]   | ₹[X]      | [X]x  | [X%]  | High/Med   | Optimize   |
| **Total**    | ₹[X]      | [#]   | ₹[X]      | [X]x  | [X%]  | Overall    | -          |

Channel Insight: [Key finding about channel performance]

FUNNEL CONVERSION ANALYSIS (if funnel data provided)

| Stage            | Count   | CVR     | Benchmark | Gap       | Priority |
|------------------|---------|---------|-----------|-----------|----------|
| Leads            | [#]     | -       | -         | -         | -        |
| Leads → MQL      | [#]     | [X%]    | [X%]      | [+/-X%]   | High/Med |
| MQL → SQL        | [#]     | [X%]    | [X%]      | [+/-X%]   | High/Med |
| SQL → Won        | [#]     | [X%]    | [X%]      | [+/-X%]   | High/Med |
| **Overall**      | [#]     | [X%]    | [X%]      | [+/-X%]   | Focus    |

Funnel Insight: [Key finding about conversion funnel]

FUNNEL SEGMENT BREAKDOWN (if segment data provided)

| Segment      | Leads | Share | MQL  | MQL%  | SQL  | SQL%  | Won  | Win%  | Efficiency |
|--------------|-------|-------|------|-------|------|-------|------|-------|------------|
| [Segment 1]  | [#]   | [X%]  | [#]  | [X%]  | [#]  | [X%]  | [#]  | [X%]  | High       |
| [Segment 2]  | [#]   | [X%]  | [#]  | [X%]  | [#]  | [X%]  | [#]  | [X%]  | Medium     |
| [Segment 3]  | [#]   | [X%]  | [#]  | [X%]  | [#]  | [X%]  | [#]  | [X%]  | Low        |
| **Total**    | [#]   | 100%  | [#]  | [X%]  | [#]  | [X%]  | [#]  | [X%]  | Overall    |

Segment Performance Matrix:
| Segment      | Vol Rank | Eff Rank | Verdict       | Action   |
|--------------|----------|----------|---------------|----------|
| [Segment 1]  | 1        | 1        | Star          | Scale    |
| [Segment 2]  | 2        | 2        | Cash Cow      | Maintain |
| [Segment 3]  | 3        | 3        | Question Mark | Diagnose |

Segment Insight: [Key finding about segment performance]

GEOGRAPHIC PERFORMANCE (if geo data provided)

| Location     | Leads | Conv | CVR   | CPL     | CAC      | Revenue  | ROAS  | Action   |
|--------------|-------|------|-------|---------|----------|----------|-------|----------|
| [City 1]     | [#]   | [#]  | [X%]  | ₹[X]    | ₹[X]     | ₹[X]     | [X]x  | Scale    |
| [City 2]     | [#]   | [#]  | [X%]  | ₹[X]    | ₹[X]     | ₹[X]     | [X]x  | Maintain |
| [City 3]     | [#]   | [#]  | [X%]  | ₹[X]    | ₹[X]     | ₹[X]     | [X]x  | Optimize |
| **Total**    | [#]   | [#]  | [X%]  | ₹[X]    | ₹[X]     | ₹[X]     | [X]x  | -        |

Geographic Insight: [Key finding about geographic performance - best/worst performing regions]

COHORT ANALYSIS (if cohort data provided)

Retention by Acquisition Cohort:
| Cohort | Customers | M1 | M2 | M3 | M4 | M5 | M6 | Avg Retention | LTV | Status |
|--------|-----------|----|----|----|----|----|----|---------------|-----|--------|
| [Month 1] | [#] | [X%] | [X%] | [X%] | [X%] | [X%] | [X%] | [X%] | ₹[X] | [Healthy/Declining/Critical] |
| [Month 2] | [#] | [X%] | [X%] | [X%] | [X%] | [X%] | - | [X%] | ₹[X] | [Status] |
| [Month 3] | [#] | [X%] | [X%] | [X%] | [X%] | - | - | [X%] | ₹[X] | [Status] |
| [Month 4] | [#] | [X%] | [X%] | [X%] | - | - | - | [X%] | ₹[X] | [Status] |
| **Benchmark** | - | 85% | 70% | 60% | 55% | 50% | 45% | 60% | - | - |

Cohort Revenue Progression:
| Cohort | M1 Revenue | M2 Revenue | M3 Revenue | M4 Revenue | Cumulative | Monthly Decay | Status |
|--------|------------|------------|------------|------------|------------|---------------|--------|
| [Month 1] | ₹[X] | ₹[X] | ₹[X] | ₹[X] | ₹[X] | [X]%/mo | [Healthy/Warning/Critical] |
| [Month 2] | ₹[X] | ₹[X] | ₹[X] | - | ₹[X] | [X]%/mo | [Status] |
| [Month 3] | ₹[X] | ₹[X] | - | - | ₹[X] | [X]%/mo | [Status] |
| **Benchmark** | - | - | - | - | - | <10%/mo | Healthy |

Revenue Decay Benchmarks:
- **Healthy:** <10% monthly decay (revenue drops <10% each month)
- **Warning:** 10-15% monthly decay (moderate churn pressure)
- **Critical:** >15% monthly decay (urgent retention issue)

Monthly Decay Calculation: ((M1 - M2) / M1) × 100 = decay rate

Cohort by Acquisition Channel:
| Channel Cohort | Customers | CAC | M3 Retention | M6 Retention | LTV | LTV:CAC | Payback | Quality |
|----------------|-----------|-----|--------------|--------------|-----|---------|---------|---------|
| [Channel 1] | [#] | ₹[X] | [X%] | [X%] | ₹[X] | [X]:1 | [X] mo | [High/Medium/Low] |
| [Channel 2] | [#] | ₹[X] | [X%] | [X%] | ₹[X] | [X]:1 | [X] mo | [High/Medium/Low] |
| [Channel 3] | [#] | ₹[X] | [X%] | [X%] | ₹[X] | [X]:1 | [X] mo | [High/Medium/Low] |

Cohort Comparison Matrix:
| Dimension | Best Cohort | Worst Cohort | Gap | Insight |
|-----------|-------------|--------------|-----|---------|
| Retention (M3) | [Cohort] ([X%]) | [Cohort] ([X%]) | [X%] | [Observation] |
| LTV | [Cohort] (₹[X]) | [Cohort] (₹[X]) | [X]x | [Observation] |
| Payback | [Cohort] ([X] mo) | [Cohort] ([X] mo) | [X] mo | [Observation] |

Cohort Insight: [Key finding about cohort performance - which acquisition sources produce best long-term customers, retention trends, LTV patterns]

ENGAGEMENT METRICS (if data provided)

| Metric | Current | Previous | Benchmark | Status | Trend |
|--------|---------|----------|-----------|--------|-------|
| CTR | [X%] | [X%] | [X%] | [Status] | [↑/↓/→] |
| CVR | [X%] | [X%] | [X%] | [Status] | [↑/↓/→] |
| Bounce Rate | [X%] | [X%] | [X%] | [Status] | [↑/↓/→] |
| Avg Session | [X] min | [X] min | [X] min | [Status] | [↑/↓/→] |

Engagement Insight: [Key finding about user engagement]

DIAGNOSTIC ANALYSIS

Primary Issue Identified: [Issue Name]
├── Symptom: [What the data shows]
├── Root Cause: [Most likely cause]
├── Evidence: [Supporting data points]
├── Impact: [Business impact - High/Medium/Low]
└── Recommended Action: [Specific action to take]

Secondary Concern: [Issue Name]
├── Symptom: [What the data shows]
├── Root Cause: [Most likely cause]
├── Evidence: [Supporting data points]
├── Impact: [Business impact - High/Medium/Low]
└── Recommended Action: [Specific action to take]

PATTERN RECOGNITION

| Pattern Detected | Interpretation | Confidence | Action Required |
|------------------|----------------|------------|-----------------|
| [Pattern 1] | [What it means] | [High/Medium/Low] | [Action] |
| [Pattern 2] | [What it means] | [High/Medium/Low] | [Action] |
| [Pattern 3] | [What it means] | [High/Medium/Low] | [Action] |

OPPORTUNITY MATRIX

| Opportunity | Current State | Target State | Effort | Impact | Priority |
|-------------|---------------|--------------|--------|--------|----------|
| [Opportunity 1] | [Current metric] | [Target metric] | [Low/Medium/High] | [Low/Medium/High] | [1-5] |
| [Opportunity 2] | [Current metric] | [Target metric] | [Low/Medium/High] | [Low/Medium/High] | [1-5] |
| [Opportunity 3] | [Current metric] | [Target metric] | [Low/Medium/High] | [Low/Medium/High] | [1-5] |

RISK ASSESSMENT

| Risk | Current Indicator | Threshold | Severity | Mitigation |
|------|-------------------|-----------|----------|------------|
| [Risk 1] | [Current value] | [Warning threshold] | [High/Medium/Low] | [Mitigation action] |
| [Risk 2] | [Current value] | [Warning threshold] | [High/Medium/Low] | [Mitigation action] |

KEY INSIGHTS

STRENGTHS:
• [Strength 1 - what's working well with supporting data]
• [Strength 2 - competitive advantage identified]
• [Strength 3 - positive trend or above-benchmark performance]

AREAS NEEDING ATTENTION:
• [Area 1 - specific metric concern with benchmark context]
• [Area 2 - declining trend identified]
• [Area 3 - efficiency opportunity]

ACTIONABLE RECOMMENDATIONS

IMMEDIATE ACTIONS (This Week):
1. [Action 1] - [Expected Impact] - [Metric affected]
2. [Action 2] - [Expected Impact] - [Metric affected]

SHORT-TERM ACTIONS (This Month):
1. [Action 1] - [Expected Impact] - [Metric affected]
2. [Action 2] - [Expected Impact] - [Metric affected]

STRATEGIC INITIATIVES (This Quarter):
1. [Initiative 1] - [Expected Impact] - [Metrics affected]
2. [Initiative 2] - [Expected Impact] - [Metrics affected]

BUDGET REALLOCATION RECOMMENDATION (if channel data provided)

| Channel | Current Allocation | Recommended Allocation | Change | Rationale |
|---------|-------------------|------------------------|--------|-----------|
| [Channel 1] | [X%] | [X%] | [+/-X%] | [Reason] |
| [Channel 2] | [X%] | [X%] | [+/-X%] | [Reason] |
| [Channel 3] | [X%] | [X%] | [+/-X%] | [Reason] |

PROJECTED IMPACT OF RECOMMENDATIONS

| Metric | Current | Projected (30 days) | Projected (90 days) | Confidence | Methodology |
|--------|---------|---------------------|---------------------|------------|-------------|
| CAC | ₹[X] | ₹[X] | ₹[X] | [High/Medium/Low] | [Basis] |
| ROAS | [X]x | [X]x | [X]x | [High/Medium/Low] | [Basis] |
| Revenue | ₹[X] | ₹[X] | ₹[X] | [High/Medium/Low] | [Basis] |

Projection Methodology:
- **Budget Reallocation Impact:** Shifting [X]% budget from [Low ROAS channel] to [High ROAS channel] → Expected [X]% improvement in blended ROAS
- **Efficiency Gains:** Reducing spend on underperforming segments → CAC reduction of [X]%
- **Volume Impact:** Scaling high-performing channels by [X]% → [X] additional conversions at similar efficiency
- **Confidence Levels:**
  - High: Based on historical data from same channels/segments
  - Medium: Based on industry benchmarks and similar campaigns
  - Low: Requires testing to validate assumptions
```

## ANALYSIS GUIDELINES

### What to Look For

**Efficiency Patterns:**
- Rising CAC with flat revenue: Acquisition becoming expensive without value increase
- Declining LTV:CAC: Marketing efficiency deteriorating
- Channel CAC divergence: Some channels becoming inefficient
- ROAS declining while spend increasing: Diminishing returns

**Quality Indicators:**
- CPL vs conversion rate relationship: Low CPL + low conversion = poor quality leads
- MQL-to-SQL ratio: Lead quality indicator
- CAC vs LTV by channel: True channel profitability

**Growth Signals:**
- Improving unit economics with scale: Healthy growth
- Stable CAC while scaling: Efficient growth
- LTV increasing faster than CAC: Compounding efficiency

**Warning Signs:**
- CAC increasing faster than LTV: Unsustainable acquisition
- Payback period extending: Cash flow pressure
- Single channel dependency: Concentration risk
- Declining engagement metrics: Audience fatigue

### Interpretation Language

Use clear, actionable language:
- "Acquisition efficiency is declining" instead of "CAC increased"
- "Channel is reaching saturation" instead of "ROAS dropped"
- "Lead quality requires attention" instead of "conversion rate fell"
- "Strong unit economics supporting growth" instead of "good LTV:CAC"

### Diagnostic Framework

**Step 1: Identify the Symptom**
- Which metric is underperforming?
- Is it trending or sudden?
- Is it isolated or systemic?

**Step 2: Trace the Cause**
- Is it a volume issue (traffic, leads)?
- Is it a quality issue (conversion, engagement)?
- Is it a value issue (AOV, LTV)?
- Is it a cost issue (CPC, CPM)?

**Step 3: Assess Impact**
- Revenue impact: Direct effect on bottom line
- Cash flow impact: Payback period changes
- Growth impact: Ability to scale

**Step 4: Recommend Action**
- Specific, measurable actions
- Expected impact with timeline
- Risk considerations

### Recommendation Prioritization

**High Priority (Immediate):**
- Metrics >30% below benchmark
- Declining trends in efficiency metrics
- Cash flow threatening patterns

**Medium Priority (Short-term):**
- Metrics 15-30% below benchmark
- Optimization opportunities in performing channels
- Testing opportunities for new channels

**Low Priority (Strategic):**
- Above-benchmark areas for maintenance
- Long-term capability building
- Experimentation and innovation

## EXAMPLE

### Input:
```
"Feb 2025 Marketing Metrics:
- Total Spend: ₹15L
- Conversions: 180
- Revenue: ₹72L
- CAC: ₹8,333
- CPL: ₹1,250 (1,200 leads)
- LTV: ₹40,000
- CTR: 2.1%
- CVR: 15%

Channel breakdown:
- Google Ads: Spend ₹6L, Conversions 90, ROAS 5.5x
- Meta Ads: Spend ₹5L, Conversions 60, ROAS 4.2x
- LinkedIn: Spend ₹4L, Conversions 30, ROAS 3.0x

vs Jan 2025:
- CAC: ₹7,500
- CPL: ₹1,100
- LTV: ₹38,000
- ROAS: 5.2x (overall)"
```

### Output:
```
Feb 2025 Marketing Metrics Insights Report

BUSINESS CONTEXT: B2B SaaS (Inferred from metrics profile)
ANALYSIS PERIOD: Feb 2025 vs Jan 2025

EXECUTIVE SUMMARY

| Metric | Value | Benchmark | Status | Trend |
|--------|-------|-----------|--------|-------|
| CAC | ₹8,333 | ₹15,000-₹50,000 | Excellent | ↑ +11% |
| CPL | ₹1,250 | ₹2,000-₹15,000 | Excellent | ↑ +14% |
| LTV | ₹40,000 | Industry varies | Strong | ↑ +5% |
| ROAS | 4.8x | 4x | Strong | ↓ -8% |
| LTV:CAC | 4.8:1 | 3:1 | Excellent | ↓ |

HEALTH SCORE: 82/100
Strong marketing efficiency with minor acquisition cost pressure; LTV growth compensating for rising CAC.

ACQUISITION EFFICIENCY ANALYSIS

| Metric | Current | Previous | Change | % Change | Assessment |
|--------|---------|----------|--------|----------|------------|
| CAC | ₹8,333 | ₹7,500 | +₹833 | +11.1% | Slight Decline |
| CPL | ₹1,250 | ₹1,100 | +₹150 | +13.6% | Slight Decline |
| CPA | ₹8,333 | ₹7,500 | +₹833 | +11.1% | Slight Decline |
| Lead→Customer | 15% | 16.7% | -1.7% | -10% | Moderate Decline |

Acquisition Insight: CAC increased 11% MoM indicating rising competition or audience saturation. However, at ₹8,333 vs benchmark of ₹15K-50K for B2B SaaS, you're still highly efficient. Monitor closely for continued escalation.

REVENUE & VALUE ANALYSIS

| Metric | Current | Previous | Change | % Change | Assessment |
|--------|---------|----------|--------|----------|------------|
| LTV | ₹40,000 | ₹38,000 | +₹2,000 | +5.3% | Improving |
| Revenue | ₹72L | ₹65L | +₹7L | +10.8% | Strong Growth |
| ARPU | ₹40,000 | ₹38,000 | +₹2,000 | +5.3% | Improving |
| Conversions | 180 | 173 | +7 | +4% | Growing |

Value Insight: LTV growing faster than expected (+5.3%) partially offsetting the CAC increase. This suggests improving product-market fit or retention. Continue investing in customer success to maintain LTV trajectory.

LTV:CAC EFFICIENCY MATRIX

| Segment | LTV | CAC | Ratio | Payback | Health | Action |
|---------|-----|-----|-------|---------|--------|--------|
| Overall | ₹40,000 | ₹8,333 | 4.8:1 | 2.5 months | Excellent | Scale with caution |
| Google Ads | ₹40,000 | ₹6,667 | 6.0:1 | 2 months | Excellent | Scale aggressively |
| Meta Ads | ₹40,000 | ₹8,333 | 4.8:1 | 2.5 months | Strong | Maintain & optimize |
| LinkedIn | ₹40,000 | ₹13,333 | 3.0:1 | 4 months | Moderate | Optimize targeting |

Efficiency Insight: Google Ads delivering exceptional 6:1 LTV:CAC with fastest payback. LinkedIn at 3:1 is at threshold - consider whether the audience quality justifies the higher CAC for B2B.

CHANNEL PERFORMANCE ANALYSIS

| Channel | Spend | Conversions | CAC | ROAS | CVR | Efficiency | Recommendation |
|---------|-------|-------------|-----|------|-----|------------|----------------|
| Google Ads | ₹6L | 90 | ₹6,667 | 5.5x | 18% | High | Scale 20% |
| Meta Ads | ₹5L | 60 | ₹8,333 | 4.2x | 14% | Medium | Optimize creatives |
| LinkedIn | ₹4L | 30 | ₹13,333 | 3.0x | 10% | Low | Refine audience |
| Total | ₹15L | 180 | ₹8,333 | 4.8x | 15% | Strong | Rebalance mix |

Channel Insight: Google Ads contributing 50% of conversions at lowest CAC - clear winner. Meta performing adequately but losing efficiency vs benchmark. LinkedIn is the weak link with 2x the CAC of Google for same LTV customers.

FUNNEL CONVERSION ANALYSIS

| Stage | Count | Conversion Rate | Benchmark | Gap | Priority |
|-------|-------|-----------------|-----------|-----|----------|
| Impressions | ~714K | - | - | - | - |
| Clicks | ~15K | 2.1% CTR | 3-5% | -0.9% | Medium |
| Leads | 1,200 | 8% | 2-5% | +3% | - |
| Conversions | 180 | 15% | 15-30% | On target | Low |

Funnel Insight: CTR below benchmark suggests ad creative or targeting optimization needed. However, landing page performance is strong with 8% visitor-to-lead conversion and 15% lead-to-customer rate.

ENGAGEMENT METRICS

| Metric | Current | Previous | Benchmark | Status | Trend |
|--------|---------|----------|-----------|--------|-------|
| CTR | 2.1% | 2.3% | 3-5% | Below | ↓ |
| CVR (Lead) | 8% | 8.5% | 2-5% | Above | ↓ |
| CVR (Sale) | 15% | 16.7% | 15-30% | On Target | ↓ |

Engagement Insight: All engagement metrics showing slight decline from previous month. CTR decline suggests ad fatigue - creative refresh recommended.

DIAGNOSTIC ANALYSIS

Primary Issue Identified: Rising Acquisition Costs
├── Symptom: CAC up 11%, CPL up 14% MoM
├── Root Cause: Likely ad fatigue (CTR declining) + competitive pressure
├── Evidence: CTR down from 2.3% to 2.1%, spend flat but efficiency declining
├── Impact: Medium - still well within healthy range but trending wrong direction
└── Recommended Action: Refresh ad creatives, test new audiences, consider new channels

Secondary Concern: LinkedIn Channel Efficiency
├── Symptom: 3.0x ROAS vs 5.5x on Google Ads
├── Root Cause: Higher CPCs on LinkedIn + lower conversion rate (10% vs 18%)
├── Evidence: 2x the CAC of best-performing channel for equivalent LTV
├── Impact: Medium - dragging overall portfolio ROAS down
└── Recommended Action: Narrow LinkedIn targeting to highest-intent audiences, reduce spend 25%

PATTERN RECOGNITION

| Pattern Detected | Interpretation | Confidence | Action Required |
|------------------|----------------|------------|-----------------|
| CAC↑, LTV↑ | Healthy growth but efficiency pressure | High | Monitor ratio closely |
| CTR↓ across channels | Ad fatigue setting in | High | Creative refresh |
| Channel efficiency divergence | Google outperforming significantly | High | Rebalance budget |

OPPORTUNITY MATRIX

| Opportunity | Current State | Target State | Effort | Impact | Priority |
|-------------|---------------|--------------|--------|--------|----------|
| Scale Google Ads | ₹6L spend, 5.5x ROAS | ₹7.5L spend, 5x ROAS | Low | High | 1 |
| Refresh ad creatives | 2.1% CTR | 3.5% CTR | Medium | High | 2 |
| LinkedIn audience refinement | 3.0x ROAS, ₹4L | 4x ROAS, ₹3L | Medium | Medium | 3 |
| Retargeting campaigns | Not measured | 2x improvement | Medium | Medium | 4 |

RISK ASSESSMENT

| Risk | Current Indicator | Threshold | Severity | Mitigation |
|------|-------------------|-----------|----------|------------|
| CAC Escalation | +11% MoM | >15% MoM | Medium | Diversify channels, refresh creatives |
| Channel Concentration | 50% from Google | >60% | Low | Test new channels proactively |
| Ad Fatigue | CTR down 9% | >15% drop | Medium | Monthly creative rotation |

KEY INSIGHTS

STRENGTHS:
• Exceptional LTV:CAC ratio of 4.8:1 provides strong foundation for scaling
• Google Ads channel achieving 6:1 LTV:CAC with room to scale
• LTV growing +5.3% indicates improving product value or retention
• Fast payback period (2.5 months) enables aggressive reinvestment

AREAS NEEDING ATTENTION:
• Acquisition costs trending up (+11% CAC, +14% CPL) - early warning sign
• CTR declining across channels suggests creative refresh needed
• LinkedIn at 3:1 LTV:CAC is underperforming portfolio average significantly
• Lead-to-customer conversion dropped from 16.7% to 15%

ACTIONABLE RECOMMENDATIONS

IMMEDIATE ACTIONS (This Week):
1. Pause lowest-performing LinkedIn campaigns - Save ₹50K/week, minimal volume impact
2. Launch 3 new ad creative variants on Meta - Expected +15% CTR improvement

SHORT-TERM ACTIONS (This Month):
1. Increase Google Ads budget by 25% - Projected +22 conversions at similar CAC
2. Implement A/B testing framework for landing pages - Target +2% conversion improvement
3. Refine LinkedIn targeting to decision-makers only - Expected CAC reduction to ₹10K

STRATEGIC INITIATIVES (This Quarter):
1. Launch retargeting campaigns across channels - Typically 2x better ROAS than prospecting
2. Test new channels (YouTube, Programmatic) - Diversify from Google dependency
3. Implement LTV tracking by acquisition source - Enable true channel profitability analysis

BUDGET REALLOCATION RECOMMENDATION

| Channel | Current Allocation | Recommended Allocation | Change | Rationale |
|---------|-------------------|------------------------|--------|-----------|
| Google Ads | 40% (₹6L) | 50% (₹7.5L) | +10% | Best efficiency, room to scale |
| Meta Ads | 33% (₹5L) | 33% (₹5L) | 0% | Maintain while optimizing |
| LinkedIn | 27% (₹4L) | 17% (₹2.5L) | -10% | Underperforming, reduce exposure |

PROJECTED IMPACT OF RECOMMENDATIONS

| Metric | Current | Projected (30 days) | Projected (90 days) | Confidence |
|--------|---------|---------------------|---------------------|------------|
| CAC | ₹8,333 | ₹7,800 | ₹7,200 | Medium |
| ROAS | 4.8x | 5.2x | 5.5x | Medium |
| Conversions | 180 | 195 | 220 | High |
| Revenue | ₹72L | ₹78L | ₹88L | Medium |
```

## EXAMPLE 2: COMBINED METRICS + FUNNEL WITH SEGMENT BREAKDOWN

### Input:
```
"Feb 2025 Marketing Data:

Metrics:
- Total Spend: ₹12L
- CAC: ₹1,20,000
- CPL: ₹12,000
- LTV: ₹5,00,000
- ROAS: 4.2x

Funnel with Geographic Breakdown:
- Leads: 100 (Mumbai-45, Goa-30, Bangalore-25)
- Site Visits: 40 (Mumbai-20, Goa-12, Bangalore-8)
- MQL: 25 (Mumbai-12, Goa-8, Bangalore-5)
- SQL: 15 (Mumbai-8, Goa-5, Bangalore-2)
- Won: 10 (Mumbai-6, Goa-3, Bangalore-1)

Channel Breakdown:
- Google: Leads 40, Won 5, Spend ₹5L
- Meta: Leads 35, Won 3, Spend ₹4L
- LinkedIn: Leads 25, Won 2, Spend ₹3L"
```

### Output:
```
Feb 2025 Marketing Metrics & Funnel Insights Report

BUSINESS CONTEXT: B2B / High-Ticket Sales
ANALYSIS PERIOD: Feb 2025

EXECUTIVE SUMMARY

| Metric | Value | Benchmark | Status | Notes |
|--------|-------|-----------|--------|-------|
| CAC | ₹1,20,000 | ₹50K-₹2L | Strong | Within range |
| CPL | ₹12,000 | ₹5K-₹20K | Strong | Good quality focus |
| LTV | ₹5,00,000 | Industry varies | - | High-ticket |
| ROAS | 4.2x | 4x | Strong | Above threshold |
| LTV:CAC | 4.2:1 | 3:1 | Excellent | Healthy unit economics |

HEALTH SCORE: 78/100
Strong unit economics with excellent LTV:CAC. Geographic concentration in Mumbai presents both opportunity and risk.

FUNNEL OVERVIEW

| Stage | Total | CVR | Benchmark | Status |
|-------|-------|-----|-----------|--------|
| Leads | 100 | - | - | Entry point |
| Site Visits | 40 | 40.0% | 30-50% | On Track |
| MQL | 25 | 62.5% | 50-70% | Strong |
| SQL | 15 | 60.0% | 40-60% | Strong |
| Won | 10 | 66.7% | 50-70% | Strong |
| **Overall** | 10 | **10.0%** | 5-15% | **Strong** |

FUNNEL SEGMENT BREAKDOWN (Geographic)

| City | Leads | % Share | Site Visits | Visit Rate | MQL | MQL Rate | SQL | SQL Rate | Won | Win Rate | CPL | CAC | Efficiency |
|------|-------|---------|-------------|------------|-----|----------|-----|----------|-----|----------|-----|-----|------------|
| Mumbai | 45 | 45% | 20 | 44.4% | 12 | 60.0% | 8 | 66.7% | 6 | 75.0% | ₹10,000 | ₹75,000 | **High** |
| Goa | 30 | 30% | 12 | 40.0% | 8 | 66.7% | 5 | 62.5% | 3 | 60.0% | ₹12,000 | ₹1,20,000 | Medium |
| Bangalore | 25 | 25% | 8 | 32.0% | 5 | 62.5% | 2 | 40.0% | 1 | 50.0% | ₹14,400 | ₹3,60,000 | **Low** |
| **Total** | 100 | 100% | 40 | 40.0% | 25 | 62.5% | 15 | 60.0% | 10 | 66.7% | ₹12,000 | ₹1,20,000 | Strong |

Segment Performance Matrix:
| City | Volume Rank | Efficiency Rank | Lead→Won CVR | Verdict | Action |
|------|-------------|-----------------|--------------|---------|--------|
| Mumbai | 1 | 1 | 13.3% | ⭐ Star | Scale aggressively |
| Goa | 2 | 2 | 10.0% | Cash Cow | Maintain & optimize |
| Bangalore | 3 | 3 | 4.0% | ❓ Question Mark | Diagnose or reduce |

Segment Insight: Mumbai is the clear winner - highest volume (45%) AND best efficiency (13.3% conversion, lowest CAC at ₹75K). Bangalore needs attention - despite 25% of leads, only 1 conversion (4% rate) with 3x the CAC of Mumbai.

CHANNEL PERFORMANCE ANALYSIS

| Channel | Leads | Won | Lead→Won | Spend | CPL | CAC | ROAS | Efficiency | Action |
|---------|-------|-----|----------|-------|-----|-----|------|------------|--------|
| Google | 40 | 5 | 12.5% | ₹5L | ₹12,500 | ₹1,00,000 | 5.0x | **High** | Scale |
| Meta | 35 | 3 | 8.6% | ₹4L | ₹11,429 | ₹1,33,333 | 3.8x | Medium | Optimize |
| LinkedIn | 25 | 2 | 8.0% | ₹3L | ₹12,000 | ₹1,50,000 | 3.3x | Low | Review targeting |
| **Total** | 100 | 10 | 10.0% | ₹12L | ₹12,000 | ₹1,20,000 | 4.2x | Strong | - |

Channel Insight: Google delivering best efficiency (12.5% conversion, 5x ROAS). LinkedIn has lowest conversion despite similar CPL - lead quality issue suspected.

CROSS-SEGMENT ANALYSIS

| Dimension | Best Performer | Worst Performer | Gap | Recommendation |
|-----------|----------------|-----------------|-----|----------------|
| Geography | Mumbai (13.3% CVR) | Bangalore (4.0% CVR) | 3.3x | Shift budget to Mumbai |
| Channel | Google (12.5% CVR) | LinkedIn (8.0% CVR) | 1.6x | Reduce LinkedIn spend |
| CAC | Mumbai (₹75K) | Bangalore (₹3.6L) | 4.8x | Investigate Bangalore issues |

DIAGNOSTIC ANALYSIS

Primary Issue: Bangalore Underperformance
├── Symptom: 4.0% conversion vs 13.3% Mumbai, 4.8x higher CAC
├── Root Cause: Low site visit rate (32%) + poor SQL conversion (40%)
├── Evidence: 25 leads → only 8 visits → only 2 SQLs → 1 win
├── Impact: High - ₹3.6L spent for 1 customer vs ₹4.5L for 6 in Mumbai
└── Action: Either fix targeting/messaging for Bangalore OR reallocate budget to Mumbai

Secondary Issue: LinkedIn Lead Quality
├── Symptom: 8.0% conversion vs 12.5% on Google
├── Root Cause: Possibly targeting too broad, attracting non-decision makers
├── Evidence: Similar CPL but 36% lower conversion
├── Impact: Medium - ₹1.5L CAC vs ₹1L on Google
└── Action: Tighten targeting to senior decision-makers, test InMail

OPPORTUNITY MATRIX

| Opportunity | Current | Target | Effort | Impact | Priority |
|-------------|---------|--------|--------|--------|----------|
| Scale Mumbai spend +50% | 45 leads, 6 won | 68 leads, 9 won | Low | High | 1 |
| Shift Bangalore budget to Mumbai | 25% allocation | 10% allocation | Low | High | 2 |
| Improve Google budget +25% | 40 leads | 50 leads | Low | Medium | 3 |
| Fix Bangalore site visit rate | 32% | 45% | Medium | Medium | 4 |

BUDGET REALLOCATION RECOMMENDATION

By Geography:
| City | Current | Recommended | Change | Rationale |
|------|---------|-------------|--------|-----------|
| Mumbai | ~45% | 60% | +15% | Best performer, scale |
| Goa | ~30% | 30% | 0% | Maintain solid performer |
| Bangalore | ~25% | 10% | -15% | Fix efficiency first |

By Channel:
| Channel | Current | Recommended | Change | Rationale |
|---------|---------|-------------|--------|-----------|
| Google | 42% (₹5L) | 50% (₹6L) | +8% | Best ROAS |
| Meta | 33% (₹4L) | 33% (₹4L) | 0% | Maintain |
| LinkedIn | 25% (₹3L) | 17% (₹2L) | -8% | Lower efficiency |

ACTIONABLE RECOMMENDATIONS

IMMEDIATE ACTIONS (This Week):
1. Increase Mumbai geo-targeting by 30% on Google - Expected +2 conversions
2. Reduce Bangalore budget by 50% until diagnosed - Save ₹1.5L/month

SHORT-TERM ACTIONS (This Month):
1. A/B test Mumbai-specific landing page - Target +5% site visit rate
2. Audit LinkedIn targeting - Focus only on C-level/Director titles
3. Create Goa-specific campaign creative - Leverage local appeal

STRATEGIC INITIATIVES (This Quarter):
1. Build Mumbai lookalike audiences for other metros - Replicate success
2. Develop city-specific value propositions - Address local pain points
3. Implement lead scoring by source + geo - Prioritize high-quality leads

PROJECTED IMPACT

| Metric | Current | After Reallocation | Improvement |
|--------|---------|-------------------|-------------|
| Conversions | 10 | 13-14 | +30-40% |
| Blended CAC | ₹1,20,000 | ₹95,000 | -21% |
| ROAS | 4.2x | 5.2x | +24% |
| Revenue | ₹50L | ₹65-70L | +30-40% |
```

## EXAMPLE 3: COHORT ANALYSIS

### Input:
```
"Q1 2025 Cohort Analysis:

Acquisition Metrics:
- Total Spend: ₹30L
- Total Customers: 150
- Blended CAC: ₹20,000

Cohort by Acquisition Month:
- Jan 2025: 50 customers, CAC ₹18,000
  - M1 retention: 90%, M2: 78%, M3: 68%, M4: 62%
  - M1 revenue: ₹5L, M2: ₹4.5L, M3: ₹4L, M4: ₹3.8L

- Feb 2025: 55 customers, CAC ₹19,000
  - M1 retention: 88%, M2: 75%, M3: 65%
  - M1 revenue: ₹5.5L, M2: ₹4.8L, M3: ₹4.2L

- Mar 2025: 45 customers, CAC ₹24,000
  - M1 retention: 82%, M2: 68%
  - M1 revenue: ₹4.5L, M2: ₹3.8L

Cohort by Channel:
- Google: 60 customers, CAC ₹16,000, M3 retention 72%, LTV ₹65,000
- Meta: 50 customers, CAC ₹22,000, M3 retention 58%, LTV ₹48,000
- LinkedIn: 40 customers, CAC ₹25,000, M3 retention 75%, LTV ₹72,000"
```

### Output:
```
Q1 2025 Cohort Analysis Report

BUSINESS CONTEXT: SaaS / Subscription Business
ANALYSIS PERIOD: Jan - Mar 2025

EXECUTIVE SUMMARY

| Metric | Value | Benchmark | Status | Trend |
|--------|-------|-----------|--------|-------|
| Blended CAC | ₹20,000 | ₹15K-₹50K | Strong | ↑ +33% (Jan→Mar) |
| Avg M3 Retention | 66% | 60-70% | On Track | ↓ Declining |
| Projected LTV | ₹58,000 | Industry varies | - | Mixed |
| LTV:CAC | 2.9:1 | 3:1 | Needs Attention | ↓ |

HEALTH SCORE: 68/100
Retention trending down and CAC trending up - cohort quality declining over Q1. Urgent action needed.

COHORT RETENTION ANALYSIS (By Acquisition Month)

| Cohort | Customers | CAC | M1 | M2 | M3 | M4 | Avg Retention | Projected LTV | LTV:CAC | Status |
|--------|-----------|-----|----|----|----|----|---------------|---------------|---------|--------|
| Jan 2025 | 50 | ₹18,000 | 90% | 78% | 68% | 62% | 74.5% | ₹68,000 | 3.8:1 | **Healthy** |
| Feb 2025 | 55 | ₹19,000 | 88% | 75% | 65% | - | 76.0% | ₹58,000 | 3.1:1 | On Track |
| Mar 2025 | 45 | ₹24,000 | 82% | 68% | - | - | 75.0% | ₹48,000 | 2.0:1 | **Critical** |
| **Benchmark** | - | - | 85% | 70% | 60% | 55% | 67.5% | - | 3:1 | - |

Retention Trend Summary:
| Month | Jan Cohort | Feb Cohort | Mar Cohort | Trend |
|-------|------------|------------|------------|-------|
| M1 | 90% | 88% | 82% | ↓ Declining (-8% over Q1) |
| M2 | 78% | 75% | 68% | ↓ Declining (-10% over Q1) |
| M3 | 68% | 65% | - | ↓ Declining |

⚠️ **Retention Alert:** Each successive cohort showing worse retention - investigate acquisition quality.

COHORT REVENUE PROGRESSION

| Cohort | M1 Revenue | M2 Revenue | M3 Revenue | M4 Revenue | Cumulative | Monthly Decay | Status |
|--------|------------|------------|------------|------------|------------|---------------|--------|
| Jan 2025 | ₹5.0L | ₹4.5L | ₹4.0L | ₹3.8L | ₹17.3L | 8.3%/mo | Healthy (<10%) |
| Feb 2025 | ₹5.5L | ₹4.8L | ₹4.2L | - | ₹14.5L | 9.1%/mo | Healthy (<10%) |
| Mar 2025 | ₹4.5L | ₹3.8L | - | - | ₹8.3L | 15.6%/mo | **Critical (>15%)** |
| **Benchmark** | - | - | - | - | - | <10%/mo | Healthy |

⚠️ **Revenue Decay Alert:** Mar cohort showing 15.6% monthly decay vs 8.3% for Jan cohort - 1.9x worse. This indicates serious retention issues with recent acquisitions.

COHORT BY ACQUISITION CHANNEL

| Channel | Customers | CAC | M3 Retention | LTV | LTV:CAC | Payback | Quality Score | Action |
|---------|-----------|-----|--------------|-----|---------|---------|---------------|--------|
| Google | 60 | ₹16,000 | 72% | ₹65,000 | 4.1:1 | 3 mo | **High** | Scale |
| LinkedIn | 40 | ₹25,000 | 75% | ₹72,000 | 2.9:1 | 4 mo | **High** | Maintain |
| Meta | 50 | ₹22,000 | 58% | ₹48,000 | 2.2:1 | 5.5 mo | **Low** | Optimize/Reduce |

Channel Cohort Insight: LinkedIn has highest LTV (₹72K) and best retention (75%) despite highest CAC. Meta customers churning fastest (58% M3 retention) - worst quality despite mid-range CAC.

COHORT COMPARISON MATRIX

| Dimension | Best Cohort | Worst Cohort | Gap | Trend | Action |
|-----------|-------------|--------------|-----|-------|--------|
| Retention (M3) | Jan 2025 (68%) | Mar 2025 (projected ~60%) | 8% | ↓ Declining | Investigate Mar acquisition quality |
| LTV | LinkedIn (₹72K) | Meta (₹48K) | 1.5x | - | Shift budget to LinkedIn |
| LTV:CAC | Google (4.1:1) | Meta (2.2:1) | 1.9x | - | Reduce Meta spend |
| CAC | Google (₹16K) | LinkedIn (₹25K) | 1.6x | - | LinkedIn justified by LTV |
| Payback | Google (3 mo) | Meta (5.5 mo) | 2.5 mo | - | Google best cash efficiency |

COHORT HEALTH DIAGNOSTIC

Primary Issue: Declining Cohort Quality Over Time
├── Symptom: M1 retention dropped from 90% (Jan) to 82% (Mar)
├── Root Cause: Likely scaling too fast, acquiring lower-quality customers
├── Evidence: CAC up 33% (₹18K→₹24K), retention down 8%, revenue decay 2x worse
├── Impact: Critical - Mar cohort LTV:CAC at 2.0:1 (below sustainable threshold)
└── Action: Pause Mar-style campaigns, return to Jan acquisition approach

Secondary Issue: Meta Channel Cohort Underperformance
├── Symptom: 58% M3 retention vs 72-75% on other channels
├── Root Cause: Targeting likely too broad, attracting low-intent users
├── Evidence: Lowest LTV (₹48K), highest churn, mediocre CAC
├── Impact: High - dragging down blended metrics
└── Action: Tighten Meta targeting or reduce spend by 40%

COHORT-BASED RECOMMENDATIONS

IMMEDIATE ACTIONS (This Week):
1. Reduce Mar-style broad campaigns - Cap spend at Jan levels
2. Implement churn prediction for Mar cohort - Proactive retention outreach
3. Pause lowest-performing Meta ad sets - Focus on proven audiences

SHORT-TERM ACTIONS (This Month):
1. Increase Google budget by 30% - Best LTV:CAC and retention
2. A/B test onboarding improvements - Target +5% M1 retention
3. Create retention campaign for Feb/Mar cohorts - Reduce M3 drop-off

STRATEGIC INITIATIVES (This Quarter):
1. Build cohort-based LTV prediction model - Identify high-value customers early
2. Implement channel-specific onboarding - LinkedIn vs Meta vs Google tracks
3. Develop early warning system - Flag at-risk customers by cohort characteristics

PROJECTED IMPACT OF COHORT OPTIMIZATION

| Metric | Current | After Optimization | Improvement |
|--------|---------|-------------------|-------------|
| Blended M3 Retention | 66% | 72% | +6% |
| Blended LTV | ₹58,000 | ₹68,000 | +17% |
| LTV:CAC | 2.9:1 | 3.4:1 | +17% |
| Annual Revenue | ₹1.5Cr | ₹1.8Cr | +20% |
```

## QUALITY CHECKLIST

Before outputting report, verify:
- [ ] All provided metrics included in analysis
- [ ] Metrics compared against appropriate industry benchmarks
- [ ] Trend direction identified for each metric
- [ ] Health status assessed for key efficiency metrics
- [ ] LTV:CAC ratio calculated and interpreted
- [ ] Channel performance analyzed (if data provided)
- [ ] Funnel segment breakdown analyzed (if segment data provided)
- [ ] Geographic performance analyzed (if geo data provided)
- [ ] Cohort retention analysis completed (if cohort data provided)
- [ ] Cohort revenue progression tracked (if cohort data provided)
- [ ] Channel cohort quality compared (if channel cohort data provided)
- [ ] Cohort trends identified (improving/declining retention)
- [ ] Diagnostic analysis with root causes completed
- [ ] Pattern recognition applied to data
- [ ] Opportunities identified and prioritized
- [ ] Risks assessed with severity levels
- [ ] Strengths and weaknesses clearly articulated
- [ ] Recommendations are specific and actionable
- [ ] Recommendations prioritized by timeframe
- [ ] Budget reallocation suggested (if channel data provided)
- [ ] Projected impact of recommendations included
- [ ] All insights supported by data evidence
