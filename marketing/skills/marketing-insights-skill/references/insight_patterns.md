# Marketing Insight Patterns

## Pattern Format
- **Signature:** Observable data pattern
- **Interpretation:** What it means for the business
- **Likely Causes:** Ranked list of probable reasons
- **Next Tests:** How to validate the hypothesis
- **Default Recommendation:** Standard action to take

---

## Acquisition Patterns

### P1: CAC Rising, Volume Flat
- **Signature:** CAC ↑ >10%, Conversions ~, Spend ↑
- **Interpretation:** Acquisition efficiency declining; paying more for same results
- **Likely Causes:**
  1. Market saturation / audience exhaustion
  2. Increased competition (auction dynamics)
  3. Ad fatigue (creative staleness)
  4. Targeting drift (wrong audiences)
- **Next Tests:**
  - Segment CAC by channel to isolate issue
  - Check frequency/reach metrics
  - Review audience overlap
- **Default Recommendation:** Refresh creatives, test new audiences, evaluate channel mix

### P2: CPL Down, CAC Up
- **Signature:** CPL ↓, CAC ↑, Lead Volume ↑
- **Interpretation:** Getting cheaper leads but they're lower quality
- **Likely Causes:**
  1. Targeting too broad (low-intent audiences)
  2. Lead magnet attracting wrong profile
  3. Channel mix shifted to cheaper but lower-quality sources
- **Next Tests:**
  - Lead-to-customer conversion by source
  - Lead scoring distribution analysis
  - MQL rate by channel
- **Default Recommendation:** Tighten targeting, qualify leads earlier, review lead magnets

### P3: CAC Declining with Scale
- **Signature:** CAC ↓, Spend ↑, Conversions ↑
- **Interpretation:** Healthy scaling - economies of scale or improved efficiency
- **Likely Causes:**
  1. Strong product-market fit
  2. Effective optimization
  3. Brand building reducing CAC
  4. Network effects / virality
- **Next Tests:**
  - Validate marginal CAC isn't rising
  - Check if blended vs incremental CAC
- **Default Recommendation:** Continue scaling with monitoring; test higher spend levels

---

## Efficiency Patterns

### P4: LTV:CAC Ratio Declining
- **Signature:** LTV:CAC ↓, either LTV ↓ or CAC ↑ (or both)
- **Interpretation:** Unit economics deteriorating; growth becoming less profitable
- **Likely Causes:**
  1. CAC rising faster than LTV
  2. Retention issues reducing LTV
  3. AOV/ARPU compression
  4. Customer quality declining
- **Next Tests:**
  - Separate LTV trend from CAC trend
  - Cohort analysis for retention changes
  - New vs returning customer behavior
- **Default Recommendation:** Address dominant factor (CAC or LTV); pause aggressive scaling

### P5: ROAS Declining, Spend Flat
- **Signature:** ROAS ↓, Spend ~, Revenue ↓
- **Interpretation:** Same spend generating less revenue - efficiency problem
- **Likely Causes:**
  1. Conversion rate declining
  2. AOV declining
  3. Attribution window changes
  4. Competitive pressure on pricing
- **Next Tests:**
  - CVR trend analysis
  - AOV trend analysis
  - Basket composition changes
- **Default Recommendation:** Diagnose CVR vs AOV issue; optimize landing pages or pricing

### P6: Payback Period Extending
- **Signature:** CAC Payback ↑ months, CAC ↑, ARPU ~
- **Interpretation:** Takes longer to recover customer acquisition investment
- **Likely Causes:**
  1. CAC rising without ARPU increase
  2. Gross margin compression
  3. Slower monetization velocity
- **Next Tests:**
  - Gross margin trend
  - Time-to-first-purchase analysis
  - Upsell/cross-sell performance
- **Default Recommendation:** Focus on early monetization; consider CAC ceiling limits

---

## Channel Patterns

### P7: Channel Performance Divergence
- **Signature:** Channel A ROAS ↑, Channel B ROAS ↓, Total ROAS ~
- **Interpretation:** Portfolio shift needed; reallocation opportunity
- **Likely Causes:**
  1. Different audience saturation rates
  2. Algorithm/platform changes
  3. Creative performance variance
  4. Seasonality affecting channels differently
- **Next Tests:**
  - Incremental impact analysis
  - Cross-channel attribution
  - New customer % by channel
- **Default Recommendation:** Shift budget toward winning channel; diagnose losing channel

### P8: Single Channel Dependency
- **Signature:** One channel >60% of conversions
- **Interpretation:** Concentration risk; vulnerable to platform changes
- **Likely Causes:**
  1. Natural fit with channel audience
  2. Underinvestment in diversification
  3. Other channels haven't been optimized
- **Next Tests:**
  - Test budgets on alternative channels
  - Evaluate audience overlap across channels
- **Default Recommendation:** Allocate 10-20% budget to test new channels; build redundancy

### P9: Paid Cannibalizing Organic
- **Signature:** Paid ↑, Organic ↓, Total ~
- **Interpretation:** Paid potentially capturing organic demand
- **Likely Causes:**
  1. Brand keyword bidding
  2. Attribution model issues
  3. Paid taking credit for organic intent
- **Next Tests:**
  - Brand vs non-brand paid split
  - Incrementality testing
  - Paid pause test (if feasible)
- **Default Recommendation:** Reduce brand keyword spend; focus paid on net-new demand

---

## Engagement Patterns

### P10: CTR Down, CVR Stable
- **Signature:** CTR ↓, CVR ~, Impressions ~
- **Interpretation:** Ad relevance declining but landing page still effective
- **Likely Causes:**
  1. Creative fatigue
  2. Ad copy not matching search intent
  3. Audience mismatch
  4. Competitive creative improvements
- **Next Tests:**
  - Creative age analysis
  - A/B test new creatives
  - Audience engagement segmentation
- **Default Recommendation:** Refresh ad creatives immediately; test new messaging angles

### P11: CTR Up, CVR Down
- **Signature:** CTR ↑, CVR ↓, Traffic ↑
- **Interpretation:** Ads attracting more clicks but wrong audience
- **Likely Causes:**
  1. Clickbait-style creative
  2. Misleading ad messaging
  3. Targeting too broad
  4. Landing page disconnect
- **Next Tests:**
  - Message match audit (ad vs landing page)
  - Bounce rate by source
  - Time on page by source
- **Default Recommendation:** Align ad messaging with landing page; qualify audience in ad

### P12: Bounce Rate Spike
- **Signature:** Bounce Rate ↑ >20%, Session Duration ↓
- **Interpretation:** Traffic quality or landing experience issue
- **Likely Causes:**
  1. Page load speed issues
  2. Mobile experience problems
  3. Content mismatch with expectation
  4. Technical errors
- **Next Tests:**
  - Page speed analysis (Core Web Vitals)
  - Device/browser breakdown
  - Heatmap and session recordings
- **Default Recommendation:** Technical audit; page speed optimization; UX review

---

## Funnel Patterns

### P13: Top of Funnel Strong, Bottom Weak
- **Signature:** Leads ↑, MQL ↑, SQL ~, Won ↓
- **Interpretation:** Awareness working but conversion failing
- **Likely Causes:**
  1. Lead quality issues
  2. Sales process friction
  3. Pricing/packaging problems
  4. Competitive losses in decision stage
- **Next Tests:**
  - Stage-by-stage conversion analysis
  - Sales call recording review
  - Win/loss analysis
- **Default Recommendation:** Improve lead qualification; sales enablement; pricing review

### P14: Middle Funnel Bottleneck
- **Signature:** Leads ~, MQL ↓, SQL ~
- **Interpretation:** Marketing qualification failing
- **Likely Causes:**
  1. MQL criteria too strict
  2. Nurture sequence ineffective
  3. Lead scoring model outdated
  4. Engagement content not converting
- **Next Tests:**
  - MQL criteria audit
  - Nurture email performance
  - Lead score vs actual conversion correlation
- **Default Recommendation:** Review MQL definitions; optimize nurture content; recalibrate scoring

### P15: High Volume, Low Conversion
- **Signature:** Impressions/Clicks ↑↑, Leads ↓
- **Interpretation:** Traffic not converting to leads
- **Likely Causes:**
  1. Wrong traffic (intent mismatch)
  2. Landing page UX issues
  3. Value proposition unclear
  4. Form friction too high
- **Next Tests:**
  - Traffic source quality analysis
  - Landing page A/B tests
  - Form abandonment analysis
- **Default Recommendation:** Quality over quantity; refine targeting; simplify conversion path

---

## Value Patterns

### P16: AOV Declining, Volume Up
- **Signature:** AOV ↓, Orders ↑, Revenue ~
- **Interpretation:** More customers buying less per transaction
- **Likely Causes:**
  1. Discount/promotion dependency
  2. Product mix shift to lower-value items
  3. Customer segment shift
  4. Bundle breakage
- **Next Tests:**
  - Promo vs non-promo comparison
  - Product mix analysis
  - Customer segment profiling
- **Default Recommendation:** Reduce discount dependency; implement upsell strategies; bundle optimization

### P17: LTV Declining
- **Signature:** LTV ↓, Churn ↑, Repeat Purchase Rate ↓
- **Interpretation:** Customer lifetime shrinking; retention problem
- **Likely Causes:**
  1. Product/service quality issues
  2. Customer experience problems
  3. Competitive alternatives
  4. Customer fit issues at acquisition
- **Next Tests:**
  - Cohort retention curves
  - NPS/CSAT trends
  - Churn reason analysis
- **Default Recommendation:** Customer success investment; retention program; acquisition quality focus

### P18: Revenue Up, Profit Down
- **Signature:** Revenue ↑, Gross Margin ↓, CAC ↑
- **Interpretation:** Growth at the expense of profitability
- **Likely Causes:**
  1. Aggressive discounting
  2. CAC inflation
  3. Mix shift to lower-margin products
  4. Operational cost increases
- **Next Tests:**
  - Unit economics by segment
  - Discount impact analysis
  - Contribution margin by channel
- **Default Recommendation:** Focus on profitable growth; set CAC/LTV guardrails; review discount strategy

---

## Seasonal & Trend Patterns

### P19: YoY Improvement, MoM Decline
- **Signature:** YoY metrics ↑, MoM metrics ↓
- **Interpretation:** Seasonal dip but overall growth trajectory healthy
- **Likely Causes:**
  1. Normal seasonality
  2. Cyclical business patterns
  3. Industry-wide trends
- **Next Tests:**
  - Historical seasonality patterns
  - Industry benchmark comparison
- **Default Recommendation:** Continue strategy; adjust expectations to seasonality; plan for peak season

### P20: Sudden Performance Cliff
- **Signature:** Key metrics ↓ >25% suddenly
- **Interpretation:** Something broke - technical, tracking, or market event
- **Likely Causes:**
  1. Tracking/attribution issues
  2. Platform algorithm change
  3. Site/app technical problems
  4. External market shock
- **Next Tests:**
  - Technical audit immediately
  - GA/tracking verification
  - Platform announcements review
- **Default Recommendation:** Immediate technical audit; verify data accuracy before reacting to metrics
