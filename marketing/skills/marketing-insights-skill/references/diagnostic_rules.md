# Marketing Diagnostic Rules

## Rule Format
- **Trigger:** Observable metric pattern
- **Checks:** What to investigate
- **Evidence Needed:** Data to confirm diagnosis
- **Likely Causes:** Ranked probable reasons
- **Recommended Playbook(s):** Action to take
- **Urgency:** Immediate / This Week / This Month

---

## Acquisition Diagnostics

### R1: CAC Escalation
**Trigger:** CAC ↑ >15% MoM or >25% vs benchmark

**Checks:**
- Which channels have CAC increases?
- Is spend up with flat conversions?
- Are CPCs rising?
- Is conversion rate declining?

**Evidence Needed:**
- Channel-level CAC breakdown
- CPC trends by platform
- CVR trends by landing page
- Competitive intelligence (auction insights)

**Likely Causes:**
1. Audience saturation / ad fatigue
2. Increased competition
3. Targeting drift
4. Landing page degradation
5. Seasonal demand shifts

**Recommended Playbook(s):** D1: CAC Reduction Sprint

**Urgency:** Immediate (if LTV:CAC <2.5:1) / This Week (otherwise)

---

### R2: Lead Quality Degradation
**Trigger:** CPL ↓ but Lead→Customer CVR ↓ significantly

**Checks:**
- Lead source mix changes
- Lead scoring distribution
- MQL rate by channel
- Sales feedback on lead quality

**Evidence Needed:**
- Lead-to-MQL rate trend
- MQL-to-SQL rate trend
- Source-level conversion rates
- Sales disposition data

**Likely Causes:**
1. Targeting broadened too much
2. Lead magnets attracting wrong audience
3. Channel mix shifted to high-volume/low-quality
4. Form qualification removed
5. Incentive structure misaligned

**Recommended Playbook(s):** D4: Funnel Conversion Recovery

**Urgency:** This Week

---

### R3: Channel Efficiency Collapse
**Trigger:** Single channel ROAS ↓ >30% or CAC ↑ >40%

**Checks:**
- Platform algorithm changes
- Tracking/attribution issues
- Creative fatigue
- Audience size changes
- Competitor activity

**Evidence Needed:**
- Impression share / reach data
- Frequency metrics
- Platform release notes
- Technical audit results

**Likely Causes:**
1. Platform algorithm change
2. Tracking breakage
3. Audience exhaustion
4. Competitor surge
5. Creative staleness

**Recommended Playbook(s):** D2: Channel Diversification, D6: Creative Refresh

**Urgency:** Immediate (if >50% of budget) / This Week (otherwise)

---

## Efficiency Diagnostics

### R4: LTV:CAC Ratio Decline
**Trigger:** LTV:CAC ↓ below 3:1 or dropped >20%

**Checks:**
- Is it LTV declining or CAC rising?
- Customer quality changes
- Retention curve shifts
- Revenue per customer changes

**Evidence Needed:**
- Cohort LTV analysis
- Churn rate trends
- ARPU trends
- CAC breakdown

**Likely Causes:**
1. CAC inflation outpacing LTV
2. Retention deteriorating
3. Customer quality declining
4. Pricing pressure
5. Competitive alternatives

**Recommended Playbook(s):** D1: CAC Reduction, D3: LTV Improvement

**Urgency:** Immediate

---

### R5: Payback Period Extension
**Trigger:** CAC Payback ↑ >3 months or exceeded 12 months

**Checks:**
- CAC trend
- ARPU trend
- Gross margin changes
- Time to first purchase

**Evidence Needed:**
- Monthly ARPU by cohort
- Gross margin trending
- First purchase timing
- Upsell rates

**Likely Causes:**
1. CAC rising without ARPU increase
2. Gross margin compression
3. Slower monetization velocity
4. Mix shift to lower-value customers

**Recommended Playbook(s):** D1: CAC Reduction, D3: LTV Improvement

**Urgency:** This Month (if <18 months) / Immediate (if >18 months)

---

### R6: ROAS Declining with Flat Spend
**Trigger:** ROAS ↓ >15%, Spend ~, Revenue ↓

**Checks:**
- Conversion rate changes
- AOV changes
- Traffic quality
- Attribution changes

**Evidence Needed:**
- CVR trend by channel
- AOV trend by segment
- Bounce rate trend
- Attribution comparison

**Likely Causes:**
1. CVR declining
2. AOV declining
3. Attribution model changes
4. Traffic quality degradation
5. Site experience issues

**Recommended Playbook(s):** D4: Funnel Conversion Recovery

**Urgency:** This Week

---

## Engagement Diagnostics

### R7: CTR Degradation
**Trigger:** CTR ↓ >20% from baseline or below benchmark

**Checks:**
- Creative age
- Frequency metrics
- Audience changes
- Competitive creative analysis

**Evidence Needed:**
- Creative performance by age
- Frequency distribution
- Audience overlap reports
- Ad preview in auction

**Likely Causes:**
1. Creative fatigue
2. Message staleness
3. Audience exhaustion
4. Competitive improvements
5. Relevance decline

**Recommended Playbook(s):** D6: Creative Refresh Sprint

**Urgency:** This Week

---

### R8: Landing Page Conversion Drop
**Trigger:** Landing page CVR ↓ >15% from baseline

**Checks:**
- Page load speed
- Device breakdown
- Traffic source changes
- Technical errors

**Evidence Needed:**
- Core Web Vitals
- Device-specific CVR
- Error logs
- Heat maps / session recordings

**Likely Causes:**
1. Page speed degradation
2. Mobile experience issues
3. Technical bugs
4. Traffic quality change
5. Message mismatch

**Recommended Playbook(s):** D4: Funnel Conversion Recovery

**Urgency:** Immediate (if main landing page) / This Week (otherwise)

---

### R9: Bounce Rate Spike
**Trigger:** Bounce rate ↑ >25% or exceeds 70%

**Checks:**
- Page load performance
- Mobile vs desktop
- Traffic source quality
- Content relevance

**Evidence Needed:**
- Page speed metrics
- Device breakdown
- Source-level bounce
- Time on page

**Likely Causes:**
1. Slow page load
2. Mobile UX problems
3. Wrong traffic
4. Content mismatch
5. Technical errors

**Recommended Playbook(s):** D4: Funnel Conversion Recovery

**Urgency:** Immediate

---

## Funnel Diagnostics

### R10: Top-of-Funnel Strong, Bottom Weak
**Trigger:** Leads/MQLs ↑ but SQLs/Wins ~ or ↓

**Checks:**
- Lead qualification criteria
- Sales follow-up rates
- Competitive win/loss
- Pricing feedback

**Evidence Needed:**
- Stage-by-stage conversion
- Sales activity metrics
- Win/loss analysis
- Competitive mentions

**Likely Causes:**
1. Lead quality issues
2. Sales process problems
3. Pricing misalignment
4. Product gaps
5. Competitor strength

**Recommended Playbook(s):** D4: Funnel Conversion Recovery, Lead qualification review

**Urgency:** This Week

---

### R11: Middle Funnel Bottleneck
**Trigger:** Lead→MQL or MQL→SQL conversion ↓ >20%

**Checks:**
- Qualification criteria changes
- Nurture engagement
- Sales handoff process
- Lead scoring accuracy

**Evidence Needed:**
- Nurture email metrics
- Lead score vs outcome correlation
- Handoff timing data
- Qualification reason breakdown

**Likely Causes:**
1. Qualification too strict
2. Nurture ineffective
3. Lead scoring off
4. Sales handoff slow
5. Content gaps in nurture

**Recommended Playbook(s):** D4: Funnel Conversion Recovery

**Urgency:** This Week

---

### R12: Pipeline Velocity Slowdown
**Trigger:** Average deal cycle ↑ >25% or pipeline aging

**Checks:**
- Stage duration by stage
- Deal progression patterns
- Sales activity levels
- Customer decision blockers

**Evidence Needed:**
- Stage time trending
- Activity per deal
- Stuck deals analysis
- Customer feedback

**Likely Causes:**
1. More stakeholders in decisions
2. Economic uncertainty
3. Sales bandwidth
4. Competitive evaluation
5. Unclear value proposition

**Recommended Playbook(s):** Sales enablement, Value proposition work

**Urgency:** This Month

---

## Value Diagnostics

### R13: AOV Decline
**Trigger:** AOV ↓ >10% without strategic intent

**Checks:**
- Product mix changes
- Discount usage
- Customer segment shifts
- Bundle performance

**Evidence Needed:**
- Product/category mix
- Coupon/discount rate
- New vs returning AOV
- Cross-sell attach rates

**Likely Causes:**
1. Heavier discounting
2. Mix shift to lower-value items
3. Bundle breakage
4. Customer segment change
5. Competitive pricing pressure

**Recommended Playbook(s):** Pricing optimization, Upsell program

**Urgency:** This Week

---

### R14: Churn Rate Increase
**Trigger:** Churn ↑ >2 percentage points or >25% increase

**Checks:**
- Customer segment affected
- Tenure distribution of churners
- Product usage patterns
- Competitive losses

**Evidence Needed:**
- Churn by cohort
- Usage metrics pre-churn
- Exit survey data
- Competitive intelligence

**Likely Causes:**
1. Product/service issues
2. Customer support failures
3. Competitive alternatives
4. Price sensitivity
5. Acquisition quality

**Recommended Playbook(s):** D3: LTV Improvement Initiative

**Urgency:** Immediate

---

### R15: Revenue Growth without Profit
**Trigger:** Revenue ↑ but Contribution Margin ↓

**Checks:**
- CAC trends
- Discount rates
- Product margin changes
- Customer mix

**Evidence Needed:**
- Fully loaded CAC
- Margin by product/segment
- Discount analysis
- Channel profitability

**Likely Causes:**
1. Over-discounting
2. CAC inflation
3. Margin compression
4. Mix shift
5. Hidden costs

**Recommended Playbook(s):** D1: CAC Reduction, Profitability analysis

**Urgency:** Immediate

---

## Channel Diagnostics

### R16: Single Channel Dependency
**Trigger:** One channel >60% of conversions or revenue

**Checks:**
- Historical channel mix
- Platform concentration risk
- Alternative channel tests
- Cross-channel effects

**Evidence Needed:**
- Channel distribution trend
- New customer source mix
- Channel correlation
- Test history

**Likely Causes:**
1. Natural fit not diversified
2. Resource constraints
3. Other channels not optimized
4. Risk not recognized

**Recommended Playbook(s):** D2: Channel Diversification

**Urgency:** This Month

---

### R17: Paid Cannibalizing Organic
**Trigger:** Paid ↑, Organic ↓, Total ~

**Checks:**
- Brand vs non-brand split
- Organic traffic trends
- Paid incrementality
- Search impression share

**Evidence Needed:**
- Organic search visibility
- Brand keyword costs
- Incrementality tests
- Attribution path analysis

**Likely Causes:**
1. Brand keyword bidding
2. Attribution confusion
3. SEO decline masked
4. Paid taking credit

**Recommended Playbook(s):** D7: Attribution Model Optimization

**Urgency:** This Month

---

## Emergency Diagnostics

### R18: Sudden Performance Cliff
**Trigger:** Key metrics ↓ >30% overnight/sudden

**Checks:**
- Tracking status
- Platform outages
- Site availability
- Campaign status

**Evidence Needed:**
- Real-time analytics
- Platform status pages
- Server logs
- Campaign audit

**Likely Causes:**
1. Tracking breakage
2. Technical outage
3. Campaign paused/disapproved
4. Budget exhausted
5. External event

**Recommended Playbook(s):** Emergency technical audit

**Urgency:** Immediate

---

### R19: Zero Conversions
**Trigger:** Conversions = 0 with active spend

**Checks:**
- Conversion tracking
- Pixel/tag firing
- Form/checkout working
- Attribution window

**Evidence Needed:**
- Tag manager debug
- Real-time conversion data
- Site checkout test
- Server-side events

**Likely Causes:**
1. Tracking broken
2. Site down/erroring
3. Attribution issue
4. Spend not delivering

**Recommended Playbook(s):** Emergency technical audit

**Urgency:** Immediate
