# Output Contract

## Data Validation (MUST Check First)

Before generating any analysis, validate input data:

### Validation Rules
1. **Funnel Progression:** Each stage must be ≤ previous stage (Leads ≥ MQL ≥ SQL ≥ Won)
2. **Percentages:** All rates must be 0-100% (Win Rate = Won ÷ SQL × 100)
3. **Segment Totals:** Segment breakdowns must sum to total
4. **Channel Totals:** Channel spend/conversions must match aggregate

### When Errors Found
If validation fails, output this section FIRST:

```
⚠️ DATA QUALITY ISSUES

| Issue        | Found         | Expected      | Impact               |
|--------------|---------------|---------------|----------------------|
| [Error type] | [Value found] | [Valid range] | [Calculations skipped] |

Recommendation: Please correct the data above before requesting full analysis.
```

---

## Required Sections (Always Include)

These sections MUST appear in every analysis output:

### 1. Header Block
```
[Date Range] Marketing Metrics Insights Report

BUSINESS CONTEXT: [Industry/Business Type]
ANALYSIS PERIOD: [Current Period] vs [Comparison Period]
```

### 2. Executive Summary Table
Always include even with minimal data:
- Show available metrics
- Include benchmark comparison
- Show status (Excellent/Strong/Moderate/Needs Attention/Critical)
- Show trend if comparison data available

### 3. Health Score
```
HEALTH SCORE: [X]/100
[One-line summary]

Score Breakdown:
| Component         | Weight   | Score   | Calculation                                              |
|-------------------|----------|---------|----------------------------------------------------------|
| LTV:CAC Ratio     | 30 pts   | [X]/30  | >5:1=30, 4-5:1=25, 3-4:1=20, 2-3:1=10, <2:1=0            |
| ROAS              | 20 pts   | [X]/20  | >5x=20, 4-5x=16, 3-4x=12, 2-3x=8, <2x=0                  |
| CAC vs Benchmark  | 20 pts   | [X]/20  | >20% below=20, at bench=15, 0-15% above=10, >30% above=0 |
| Funnel Conversion | 15 pts   | [X]/15  | Above bench=15, at bench=12, 0-15% below=8, >15% below=0 |
| Trend Direction   | 15 pts   | [X]/15  | Improving=15, Stable=10, Declining=5, Rapidly declining=0|
| **Total**         | 100 pts  | [X]/100 | Sum of above                                             |
```

**IMPORTANT:** Always show the score breakdown table so users understand how the score was calculated.

### 4. Key Insights Section
Always include:
- STRENGTHS (minimum 2)
- AREAS NEEDING ATTENTION (minimum 2)

### 5. Actionable Recommendations
Always provide:
- IMMEDIATE ACTIONS (minimum 1)
- SHORT-TERM ACTIONS (minimum 1)

---

## Conditional Sections (Include When Data Available)

### If Period Comparison Data Provided:
- Acquisition Efficiency Analysis (with change columns)
- Revenue & Value Analysis (with change columns)
- Trend indicators (↑/↓/→)

### If Channel Breakdown Provided:
- Channel Performance Analysis table
- Channel Insight
- Budget Reallocation Recommendation

### If Funnel Data Provided:
- Funnel Conversion Analysis
- Funnel Insight
- Stage-by-stage recommendations

### If Engagement Metrics Provided:
- Engagement Metrics table
- Engagement Insight

### If LTV and CAC Both Provided:
- LTV:CAC Efficiency Matrix
- Payback period analysis
- Efficiency Insight

---

## Sections to Skip (With Notes)

When data is missing, include a brief note instead:

| Missing Data          | Note to Include                                        |
|-----------------------|--------------------------------------------------------|
| LTV                   | "LTV data required for full efficiency analysis"       |
| Channel breakdown     | "Channel-level analysis requires channel breakdown data"|
| Historical/comparison | "Trend analysis requires comparison period data"       |
| Funnel stages         | "Funnel analysis requires stage-level counts"          |
| Spend data            | "Spend data needed for ROI/ROAS calculations"          |

---

## Table Formatting Rules

### Numeric Formatting
- Currency: ₹X,XXX or ₹X.XL (lakhs) or ₹X.XCr (crores)
- Percentages: X.X%
- Ratios: X.Xx or X.X:1
- Change: +X% or -X% with sign always shown

### Status Indicators
Use exactly these terms:
- **Excellent:** >20% above benchmark
- **Strong:** At or above benchmark
- **Moderate:** 0-15% below benchmark
- **Needs Attention:** 15-30% below benchmark
- **Critical:** >30% below benchmark

### Trend Indicators
- ↑ Improving (positive change)
- ↓ Declining (negative change)
- → Stable (within ±5%)

### Priority Indicators
- **Immediate:** Action required this week
- **This Month:** Short-term priority
- **This Quarter:** Strategic initiative

### Revenue Decay Indicators (for Cohort Analysis)
- **Healthy:** <10% monthly decay
- **Warning:** 10-15% monthly decay
- **Critical:** >15% monthly decay

Calculation: Monthly Decay = ((M1 Revenue - M2 Revenue) / M1 Revenue) × 100

---

## Projection Methodology (Required for Projected Impact Section)

All projections MUST include methodology explanation:

```
Projection Methodology:
- **Budget Reallocation Impact:** Shifting [X]% budget from [Channel A] to [Channel B] → Expected [X]% improvement
- **Efficiency Gains:** [Specific action] → [X]% improvement based on [evidence]
- **Confidence Levels:**
  - High: Based on historical data from same channels/segments
  - Medium: Based on industry benchmarks
  - Low: Requires testing to validate
```

**NEVER** show projections without explaining the basis for the numbers.

---

## Section Order (Strict)

1. Header Block
2. Executive Summary
3. Health Score
4. Acquisition Efficiency Analysis
5. Revenue & Value Analysis
6. LTV:CAC Efficiency Matrix
7. Channel Performance Analysis
8. Funnel Conversion Analysis
9. Engagement Metrics
10. Diagnostic Analysis
11. Pattern Recognition
12. Opportunity Matrix
13. Risk Assessment
14. Key Insights (Strengths & Attention Areas)
15. Actionable Recommendations
16. Budget Reallocation Recommendation
17. Projected Impact

---

## Language Guidelines

### Use Action-Oriented Language
- ✅ "Scale Google Ads budget by 20%"
- ❌ "Consider increasing Google Ads"

### Be Specific with Numbers
- ✅ "CAC increased 11% from ₹7,500 to ₹8,333"
- ❌ "CAC went up"

### Provide Context
- ✅ "CAC of ₹8,333 is excellent vs benchmark of ₹15,000-₹50,000"
- ❌ "CAC is ₹8,333"

### Connect Insights to Actions
- ✅ "CTR declining (-9%) suggests ad fatigue; refresh creatives"
- ❌ "CTR is declining"

---

## Quality Checklist

Before output:
- [ ] All provided metrics analyzed
- [ ] Benchmarks cited for context
- [ ] Trends identified if comparison data available
- [ ] Health score calculated
- [ ] Diagnostic analysis included
- [ ] At least 3 actionable recommendations
- [ ] Strengths and attention areas balanced
- [ ] No speculation without data evidence
- [ ] Currency symbols consistent
- [ ] Percentages properly formatted
