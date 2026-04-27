# Test Cases for Marketing Metrics Insights Skill

## Activation Trigger Tests

### Test T1: Metric Keywords Trigger
**Input:** "Our CAC is ₹8,000 and CPL is ₹1,200"
**Expected:** Skill activates, analyzes CAC and CPL against benchmarks

### Test T2: ROAS Trigger
**Input:** "What does ROAS of 3.5x mean for our Meta campaigns?"
**Expected:** Skill activates, provides ROAS analysis with benchmark context

### Test T3: LTV:CAC Trigger
**Input:** "LTV:CAC ratio is 2.5:1, is this healthy?"
**Expected:** Skill activates, provides LTV:CAC efficiency analysis

### Test T4: Channel Performance Trigger
**Input:** "Google Ads: Spend ₹5L, 100 conversions, ₹20L revenue"
**Expected:** Skill activates, calculates ROAS (4x), CAC (₹5,000), provides insights

### Test T5: Funnel Data Trigger
**Input:** "500K impressions → 10K clicks → 500 leads → 50 customers"
**Expected:** Skill activates, calculates conversion rates at each stage

### Test T6: Marketing ROI Trigger
**Input:** "Help me understand our marketing ROI from last month's data"
**Expected:** Skill activates, requests metrics if not provided

---

## Calculation Accuracy Tests

### Test C1: LTV:CAC Ratio
**Input:**
- LTV: ₹40,000
- CAC: ₹8,000
**Expected Output:**
- LTV:CAC = 5:1
- Status: Excellent
- Interpretation: Strong unit economics

### Test C2: ROAS Calculation
**Input:**
- Spend: ₹5,00,000
- Revenue: ₹22,00,000
**Expected Output:**
- ROAS = 4.4x
- Status: Strong (vs 4x benchmark)

### Test C3: CAC Payback
**Input:**
- CAC: ₹20,000
- Monthly ARPU: ₹5,000
- Gross Margin: 80%
**Expected Output:**
- Payback = 20,000 / (5,000 × 0.80) = 5 months
- Status: Excellent

### Test C4: Funnel Conversion Rates
**Input:**
- Leads: 1,000
- MQL: 300
- SQL: 90
- Customers: 18
**Expected Output:**
- Lead→MQL: 30%
- MQL→SQL: 30%
- SQL→Customer: 20%
- Overall: 1.8%

### Test C5: Period Change Calculation
**Input:**
- Current CAC: ₹8,333
- Previous CAC: ₹7,500
**Expected Output:**
- Change: +₹833
- % Change: +11.1%
- Trend: ↑

---

## Benchmark Comparison Tests

### Test B1: B2B SaaS CAC
**Input:** "SaaS company, CAC ₹45,000"
**Expected:**
- Benchmark: ₹15,000-₹1,50,000
- Status: Strong (within range)

### Test B2: E-commerce CAC
**Input:** "E-commerce, CAC ₹6,000"
**Expected:**
- Benchmark: ₹500-₹5,000
- Status: Needs Attention (above range)

### Test B3: Google Search CTR
**Input:** "Search campaign CTR 4.5%"
**Expected:**
- Benchmark: 3-5% good
- Status: Strong

### Test B4: Low LTV:CAC
**Input:** "LTV ₹10,000, CAC ₹8,000"
**Expected:**
- Ratio: 1.25:1
- Status: Critical
- Alert: "Unsustainable unit economics"

---

## Diagnostic Rule Tests

### Test D1: CAC Escalation Detection
**Input:**
- Current CAC: ₹10,000
- Previous CAC: ₹7,500
- Change: +33%
**Expected:**
- Trigger R1: CAC Escalation
- Recommended: D1 Playbook (CAC Reduction Sprint)
- Urgency: Immediate

### Test D2: Lead Quality Issue
**Input:**
- CPL: ₹500 (down 20%)
- Lead→Customer: 2% (down from 5%)
**Expected:**
- Trigger R2: Lead Quality Degradation
- Diagnosis: Cheaper leads but lower quality
- Action: Tighten targeting

### Test D3: Channel Efficiency Collapse
**Input:**
- Meta ROAS previous: 5.0x
- Meta ROAS current: 3.0x
- Change: -40%
**Expected:**
- Trigger R3: Channel Efficiency Collapse
- Alert: Major efficiency drop
- Checks: Creative fatigue, tracking, algorithm

### Test D4: Funnel Bottleneck
**Input:**
- Leads: ↑ 20%
- MQL: ↑ 15%
- SQL: → flat
- Customers: ↓ 10%
**Expected:**
- Trigger R11: Middle Funnel Bottleneck
- Diagnosis: Sales qualification or follow-up issue

---

## Pattern Recognition Tests

### Test P1: Spend Up, Conversions Flat
**Input:**
- Spend: ₹15L (up from ₹12L)
- Conversions: 100 (was 98)
**Expected:**
- Pattern P1 detected
- Interpretation: Diminishing returns
- Action: Optimize before scaling further

### Test P2: CTR Down, CVR Stable
**Input:**
- CTR: 1.8% (was 2.5%)
- CVR: 3.2% (was 3.1%)
**Expected:**
- Pattern P10 detected
- Interpretation: Ad fatigue
- Action: Creative refresh needed

### Test P3: Channel Divergence
**Input:**
- Google ROAS: 6x (up)
- Meta ROAS: 3x (down)
**Expected:**
- Pattern P7 detected
- Interpretation: Reallocation opportunity
- Action: Shift budget to Google

---

## Edge Case Tests

### Test E1: Minimal Input
**Input:** "CAC ₹5,000"
**Expected:**
- Basic analysis against benchmark
- Note: "LTV data required for full efficiency analysis"
- Provide benchmark context only

### Test E2: Zero Denominator
**Input:** "0 conversions, ₹5L spend"
**Expected:**
- Cannot calculate CAC (divide by zero)
- Alert: "Zero conversions detected"
- Focus on diagnosing why

### Test E3: Missing Comparison Period
**Input:** "Current CAC ₹8,000"
**Expected:**
- Benchmark comparison only
- Note: "Trend analysis requires comparison period"
- No % change calculations

### Test E4: Incomplete Channel Data
**Input:** "Google: 50 conversions | Meta: ₹3L spend"
**Expected:**
- Partial analysis where possible
- Note which metrics missing for complete analysis

### Test E5: Very High Values (Luxury/Enterprise)
**Input:** "CAC ₹5,00,000, LTV ₹50,00,000"
**Expected:**
- Recognize high-ticket context
- Apply appropriate benchmarks
- LTV:CAC = 10:1 (Excellent)

---

## Multi-Channel Tests

### Test M1: Channel Mix Analysis
**Input:**
```
Google: ₹6L spend, 90 conv, ROAS 5.5x
Meta: ₹5L spend, 60 conv, ROAS 4.2x
LinkedIn: ₹4L spend, 30 conv, ROAS 3.0x
```
**Expected:**
- Identify Google as top performer
- Flag LinkedIn underperformance
- Recommend budget shift
- Calculate blended metrics

### Test M2: Single Channel Dependency
**Input:**
```
Google: 85% of conversions
All others: 15%
```
**Expected:**
- Flag concentration risk
- Trigger R16: Single Channel Dependency
- Recommend diversification

---

## Recommendation Quality Tests

### Test R1: Actionable Specificity
**Input:** "CAC ₹8,000 up 15%, ROAS 4x down 10%"
**Expected:**
- Specific actions, not vague suggestions
- ✅ "Reduce LinkedIn spend by 25%"
- ❌ "Consider optimizing channels"

### Test R2: Priority Assignment
**Input:** Multiple issues identified
**Expected:**
- Clear priority ranking
- Immediate vs This Month vs Strategic
- Impact-effort assessment

### Test R3: Projected Impact
**Input:** Recommendations provided
**Expected:**
- Quantified expected improvement
- Confidence level stated
- Timeline for results

---

## Format Compliance Tests

### Test F1: Table Structure
**Expected:** All tables properly formatted with:
- Headers
- Aligned columns
- Consistent units
- Proper symbols (₹, %, x)

### Test F2: Section Order
**Expected:** Sections appear in order per output_contract.md

### Test F3: Status Language
**Expected:** Uses exactly: Excellent/Strong/Moderate/Needs Attention/Critical

### Test F4: Trend Arrows
**Expected:** Uses exactly: ↑/↓/→

---

## Industry-Specific Tests

### Test I1: SaaS B2B
**Input:** "SaaS: MRR ₹10L, CAC ₹50K, 12-month contracts"
**Expected:**
- Apply SaaS benchmarks
- Calculate LTV from MRR × contract length
- Analyze payback period

### Test I2: E-commerce
**Input:** "E-commerce: AOV ₹2,000, CAC ₹400, ROAS 5x"
**Expected:**
- Apply e-commerce benchmarks
- Focus on AOV and repeat rate
- Cart abandonment if provided

### Test I3: Real Estate
**Input:** "Luxury real estate: CPL ₹15,000, 85 leads, 2 sales"
**Expected:**
- Apply real estate benchmarks
- Long cycle context
- High-ticket analysis
