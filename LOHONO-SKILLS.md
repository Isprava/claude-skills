# Lohono Stays — Skills Guide

How to use the 6 Lohono Stays marketing skills in Claude Code. Each skill is a specialist assistant trained on Lohono's brand, voice, destinations, and offerings. You invoke a skill, provide the inputs it asks for, and get a structured, brand-aligned output ready to use or refine.

---

## Table of Contents

1. [How Skills Work](#how-skills-work)
2. [Quick Reference](#quick-reference)
3. [Skill 1: `/lohono-brief` — Campaign Brief Writer](#skill-1-lohono-brief)
4. [Skill 2: `/lohono-persona` — Guest Persona Builder](#skill-2-lohono-persona)
5. [Skill 3: `/lohono-linkedin` — LinkedIn Post Writer](#skill-3-lohono-linkedin)
6. [Skill 4: `/lohono-adcopy` — Ad Copy Generator](#skill-4-lohono-adcopy)
7. [Skill 5: `/lohono-review` — Brand Content Reviewer](#skill-5-lohono-review)
8. [Skill 6: `/lohono-report` — Campaign Report Writer](#skill-6-lohono-report)
9. [Combining Skills: End-to-End Workflows](#combining-skills)
10. [Tips for Best Results](#tips-for-best-results)

---

## How Skills Work

These skills run inside **Claude Code** (the CLI or desktop app). Each skill is a `.md` file that loads specialized brand context and a structured output format into Claude's session.

**To invoke a skill**, type its name as a slash command:

```
/lohono-brief
```

Claude will ask for the inputs it needs (or you can provide them upfront in the same message). It then produces a complete, structured output — a campaign brief, a persona, two LinkedIn posts, three ad variants, a brand review, or a campaign report.

**You don't need to explain what Lohono is.** Each skill already knows the brand, the destinations, the offerings, the tone rules, and the banned phrases. You only need to provide the task-specific inputs.

---

## Quick Reference

| Skill | Invoke with | Ask for | Gets you |
|-------|------------|---------|----------|
| Campaign brief | `/lohono-brief` | Goal, destination, audience, key message | Full structured campaign brief |
| Guest persona | `/lohono-persona` | Destination + occasion | Vivid guest portrait with conversion triggers |
| LinkedIn posts | `/lohono-linkedin` | Topic or property | 2 posts: story-driven + insight-driven |
| Ad copy | `/lohono-adcopy` | Property, audience, platform | 3 ad variations (Meta / Google / WhatsApp) |
| Brand review | `/lohono-review` | Paste any copy | Score /25 + specific feedback + revised version |
| Campaign report | `/lohono-report` | Campaign metrics + objective | Full stakeholder performance report |

---

## Skill 1: `lohono-brief`

**What it does:** Writes a complete campaign brief — the single document that aligns every creative and channel decision before work begins.

### How to invoke

```
/lohono-brief
```

Claude will ask:
1. Campaign goal
2. Destination or property
3. Audience segment
4. Key message (or ask Claude to suggest one)

### You can also front-load the inputs:

```
/lohono-brief

Goal: Generate honeymoon enquiries for Goa properties in December–January
Destination: Goa (beachfront villas)
Audience: Couples, 28–38, Mumbai and Bangalore, recently engaged or married within the last year
Key message: Goa is not just a party destination — it is where you begin
```

### Example output (excerpt)

```
LOHONO STAYS — CAMPAIGN BRIEF
Campaign name: First Light, Goa
Date: 13 April 2026

1. OBJECTIVE
Drive 80 qualified honeymoon enquiries for Goa properties in the
December 2026 – January 2027 window, with a target CPL under ₹3,500.

Supporting goals:
- Grow the honeymoon segment as a % of total Goa bookings from 18% to 25%
- Build a WhatsApp broadcast list of 500+ engaged/recently married couples

Primary KPI: Qualified enquiries (defined as couples with a travel
window within 90 days)
Supporting KPI 1: CPL across paid channels
Supporting KPI 2: Email open rate on honeymoon nurture sequence

---

2. AUDIENCE PROFILE
Priya and Arjun. She's a UX lead at a Bangalore startup; he's in finance
in Mumbai. Married six months ago. They did a quick trip to Bali for the
honeymoon but always said they'd do "the real one" later. This feels like
the right window — before life gets complicated. They want privacy, a view,
a breakfast that doesn't require planning. They've seen Lohono on Instagram
through a friend who posted from Alibaug. They're ready, they just need to
be shown the right villa.

Where they are: Instagram (primary), WhatsApp (direct), Google (intent)
What would convert them: Seeing the exact breakfast setup. A specific photo
of a bed facing the sea. A WhatsApp from a consultant who knows their names.

---

3. TONE GUIDANCE
Intimate. Anticipatory. Salt-and-light.
Emotional territory: The particular excitement of something you've been
looking forward to finally arriving.

Proof points:
- A private villa where the only other people are your own chef and concierge
- An Arabian Sea view from a pool that is entirely yours
- A sunrise breakfast set up on the terrace before you've asked for it
```

---

## Skill 2: `lohono-persona`

**What it does:** Builds a vivid, specific guest persona — not a demographic slide, but a portrait of a real person with inner life, travel motivation, booking behaviour, and the exact things that would convert them.

### How to invoke

```
/lohono-persona
```

Claude will ask:
1. Destination
2. Occasion type

### Example prompt

```
/lohono-persona

Destination: Alibaug farmhouse villa
Occasion: Family holiday (parents + 2 kids under 10)
```

### Example output (excerpt)

```
LOHONO STAYS — GUEST PERSONA
Persona: Vikram & Meghna, Family of Four
Destination + Occasion: Alibaug — Family Holiday

---

THE PERSON
Name: Vikram Malhotra
Age: 41
City: Mumbai, Bandra West
Occupation: Co-founder of a logistics tech company (Series A)
Household income: ₹1.2–₹1.8Cr
Travel frequency: 3–4 trips per year, ₹3–6L per trip
How they found Lohono: Meghna saw a reel of the Alibaug farmhouse
on Instagram — the infinity pool with paddy fields behind it. She
sent it to the family WhatsApp group.

---

THEIR WORLD
You've been promising this trip for three months. The kids keep
asking. Meghna has stopped asking — which is worse. You keep saying
"next weekend" and then something comes up. This time, you've blocked
the calendar and told your EA it's non-negotiable. You want to show
up as a dad for a whole weekend, not a founder who happens to be
present in the same house.

---

IN THEIR OWN WORDS
"I just want to get there and not have to think about anything. No
driving around for dinner. No one asking me what's for breakfast.
The kids can run around, Meghna gets a proper break, and I can
actually sit by a pool without my phone for three hours."

---

VILLA STAY PREFERENCES
Privacy level: Fully private — no shared spaces with other guests.
Pool: Large enough for the kids to swim freely; paddy field view
      essential for Meghna (she's the decision-maker on aesthetics)
Chef: Yes — particularly someone who can do child-friendly food
      without making a production of it. The adults want proper food.
Concierge: Airport/Mumbai pickup coordinated; zero-planning energy
           for activities — but a list ready if they want to do something
Space: Needs 3 bedrooms minimum; open living area where kids can
       play indoors if it rains
Must-haves: Fully private pool, private chef for all meals, strong
            WiFi (Vikram will check in once a day — he knows it)
Nice-to-haves: A naturalist or kids' activity option;
               a couple's spa treatment for Saturday evening

---

WHAT CONVERTS THEM
1. Seeing a video of the actual pool and the paddy field view —
   not a styled shoot, a real video from a family who stayed
2. A WhatsApp from the Lohono consultant referencing that it's a
   family stay and asking about the kids' food preferences
3. A meal photo from the chef — something that shows both a kid's
   plate and a proper adult dinner from the same kitchen
4. The words "fully private" appearing early in any communication
5. Another Mumbai family they know has stayed and loved it
```

---

## Skill 3: `lohono-linkedin`

**What it does:** Writes two LinkedIn posts on any Lohono topic — one story-driven (opens mid-scene), one insight-driven (opens with a bold perspective). Both use a soft CTA that invites, never sells.

### How to invoke

```
/lohono-linkedin
```

Claude will ask for the topic or property to highlight.

### Example prompt

```
/lohono-linkedin

Topic: What a proper break actually does for founders and senior leaders.
Property angle: Alibaug farmhouses — close enough that you actually go.
```

### Example output

```
POST 1 — STORY-DRIVEN

The founder arrived on Friday evening with three unread Slack threads
open on his phone.

By Saturday morning, he hadn't checked it.

Not because he forced himself. Because the chef had set up breakfast
by the pool before he was awake. Because there was nowhere to be and
nothing to organize. Because the paddy fields don't care about Series B.

He told us later: "It was the first time in two years I remembered
what my brain feels like when it isn't solving something."

That's not a vacation stat. That's what rest actually is.

If someone you know needs exactly this — Alibaug is two hours from
Mumbai and fully private. The link is in the comments.

---

POST 2 — INSIGHT-DRIVEN

The founders who perform best over a decade are also the ones who
are genuinely good at stopping.

Not at detaching — at actually stopping. Letting the nervous system
complete a cycle. Coming back to the work with a different quality
of attention.

Most "holidays" don't do this. A hotel room in a city, a packed
itinerary, twelve restaurant decisions — that's a change of scenery,
not a restoration.

What works: a place where everything is already taken care of before
you arrive. Where the only decision on day one is whether you want
the coffee before or after the swim.

We see this with the guests who stay at Lohono's Alibaug properties
regularly. They're not escaping their work. They're protecting their
capacity to do it well.

Some places do that. Most don't.

#LeadershipWellbeing #FounderLife #Lohono
```

---

## Skill 4: `lohono-adcopy`

**What it does:** Generates 3 ad variations for a specific property, audience, and platform — each in the correct format with character-count-compliant headlines and body copy. Three angles: emotional/sensory, specific/proof-led, and occasion/identity.

### How to invoke

```
/lohono-adcopy
```

Claude will ask for property/destination, target audience, and platform.

### Example prompt

```
/lohono-adcopy

Property: Lohono villas, Bali
Audience: Indian couples, 30–40, from Mumbai and Bangalore, planning a
          10th anniversary trip
Platform: Meta (Instagram/Facebook)
```

### Example output

```
VARIATION A — Emotional / Sensory
Headline (28 chars):  A Bali morning, just yours
Primary text (87 chars): Rice terraces at dawn. A private pool. A chef who was there first.
CTA button: Learn More
Visual direction: Real footage, not styled — the view from the villa
  deck at 6:30am, mist still on the terraces, a single coffee cup

---

VARIATION B — Specific / Proof-led
Headline (29 chars):  Private villa. Personal chef.
Primary text (84 chars): A fully private Bali villa. Your own chef for every meal. No shared
  spaces. Lohono.
CTA button: Get Quote
Visual direction: Split shot — the pool from above + the chef plating
  a breakfast spread on the deck

---

VARIATION C — Occasion / Identity
Headline (27 chars):  Ten years. Make it count.
Primary text (89 chars): Some anniversaries deserve more than a dinner. Bali, fully private,
  with Lohono.
CTA button: Book Now
Visual direction: A couple (backs to camera) at the edge of an infinity
  pool looking out over jungle — golden hour
```

---

## Skill 5: `lohono-review`

**What it does:** Reviews any piece of Lohono marketing copy against 5 brand criteria, scores each out of 5 (total /25), gives specific feedback with exact quotes from the copy, then delivers a fully revised version.

### How to invoke

```
/lohono-review
```

Claude will ask you to paste the copy.

### Example prompt

```
/lohono-review

Here's the copy:

"Discover the luxury of a lifetime at Lohono Stays! Our world-class
villas in Goa offer unmatched amenities and breathtaking views. Book
now and experience the best of luxury travel. Don't miss out — limited
availability!"
```

### Example output

```
LOHONO STAYS — CONTENT REVIEW
Content type: Ad copy / Instagram caption
Review date: 13 April 2026

---

CRITERION 1: TONE — 1/5
What doesn't work: "Discover the luxury of a lifetime" opens with a
  phrase that could appear on a budget hotel's banner. "Don't miss out"
  and "Book now" in the same sentence creates a sale-rail urgency that
  is the opposite of how a premium private villa brand speaks. The
  exclamation mark after "Lohono Stays!" treats the brand name like a
  promo code. This copy is speaking at the reader, not inviting them in.

---

CRITERION 2: CLARITY — 3/5
What works: It is clear that villas in Goa are being promoted.
What doesn't work: "Best of luxury travel" tells us nothing specific
  about what the experience is. A reader would finish this and not know
  what differentiates a Lohono stay from any other villa in Goa.

---

CRITERION 3: SPECIFICITY TO LOHONO — 1/5
What doesn't work: Remove the Lohono logo. This copy could appear on
  a Marriott ad, an Airbnb Luxe listing, or a Goa resort aggregator
  unchanged. No chef. No concierge. No private villa experience. No
  specific sensory detail. Nothing that is Lohono.

---

CRITERION 4: CTA QUALITY — 2/5
What doesn't work: "Book now" is appropriate for retargeting — not
  for cold audience awareness copy. "Don't miss out — limited
  availability" is the language of a flash sale, not a handpicked
  luxury villa. It will repel the target audience.

---

CRITERION 5: AVOIDANCE OF CLICHÉS — 1/5
Banned phrases found:
  — "world-class" (line 2): on the banned list. Remove.
  — "unmatched amenities" (line 2): "unmatched" is banned.
    "Amenities" is vague and corporate.
  — "breathtaking views" (line 2): banned adjective. Replace with
    a specific sensory detail.
  — "Don't miss out" (line 3): banned phrase.
  — "luxury of a lifetime" (line 1): cliché.
  — "best of luxury travel" (line 3): generic superlative, no meaning.

OVERALL SCORE: 8/25 — Rewrite required.

---

PRIORITY FIXES
1. Replace every banned phrase with a specific, verifiable detail
   about a Goa Lohono villa (the view, the chef, the pool).
2. Remove the exclamation mark and the urgency language entirely —
   this is not a flash sale.
3. Open with a moment, not a claim.

---

REVISED VERSION

The Arabian Sea at 6pm has a particular shade of blue.

You notice it from your private pool. Your chef is setting up sundowners
on the deck. There's no one else here.

This is a Lohono villa in Goa — handpicked, fully private, with a
personal chef and concierge for the duration of your stay.

If Goa is on your mind, we'd love to show you what's available.
→ [Link in bio]
```

---

## Skill 6: `lohono-report`

**What it does:** Turns campaign metrics into a complete stakeholder-ready performance report — with executive summary, KPI performance table, channel breakdown, top performers, honest analysis of what worked and what didn't, and 3 specific recommendations for the next campaign.

### How to invoke

```
/lohono-report
```

Claude will ask for campaign metrics and the objective.

### Example prompt

```
/lohono-report

Campaign: Goa Monsoon Escape — June 2026
Objective: Generate 60 Goa villa enquiries during the June–July
  monsoon window (traditionally low season)
Dates: 1 June – 15 July 2026
Budget: ₹4,50,000 total
Channels: Instagram organic, Meta paid (₹2,80,000), Email (2 sends),
  1 influencer stay
Metrics:
  - Meta: 8.2M impressions, 1.1% CTR, ₹38 CPC, 42 leads, CPL ₹6,666
  - Email: 2,400 sent, 34% open rate, 8% CTR, 9 leads
  - Instagram organic: 180K reach, 4.2% engagement rate
  - Influencer reel: 420K views, 2,100 saves
  - Total leads: 51
  - Bookings confirmed from campaign: 7
  - Revenue from confirmed bookings: ₹18,60,000
```

### Example output (excerpt)

```
LOHONO STAYS — CAMPAIGN PERFORMANCE REPORT
Campaign: Goa Monsoon Escape
Period: 1 June – 15 July 2026
Report date: 13 April 2026

---

1. EXECUTIVE SUMMARY
The Goa Monsoon Escape campaign generated 51 qualified leads against
a target of 60 — 15% below goal — at an overall CPL of ₹8,823. Seven
bookings were confirmed, producing ₹18.6L in revenue and a 4.1x return
on total campaign spend. The campaign demonstrated that monsoon Goa has
a genuine, convertible audience; the shortfall was a distribution
problem, not a demand problem. The influencer reel (420K views, 2,100
saves) significantly outperformed paid social on cost-per-attention.
Recommendation: lead the next monsoon campaign with creator content
and use paid amplification on the top-performing organic assets rather
than generic creative.

Performance verdict: Partially delivered (15% below primary KPI,
strong ROAS).

---

2. KPI PERFORMANCE

| KPI              | Target | Actual | Variance | Status     |
|------------------|--------|--------|----------|------------|
| Leads generated  | 60     | 51     | -15%     | Not met    |
| CPL              | ₹5,000 | ₹8,823 | -76%     | Not met    |
| Bookings         | 10     | 7      | -30%     | Not met    |
| Revenue (ROAS)   | 3x     | 4.1x   | +37%     | Exceeded   |

Context: June saw two weeks of heavy monsoon media coverage across
Maharashtra. Anecdotally, several warm leads mentioned "waiting for
the rain to clear" — suggesting the timing window was correct but
the messaging did not adequately reframe monsoon as a feature rather
than a risk.

---

5. WHAT WORKED
- The influencer reel generated 2,100 saves at effectively zero paid
  media cost — the highest save rate of any Lohono asset this quarter.
  Saves indicate intent to return, not just passive viewing. This
  format and creator profile should be repeated.

- Email outperformed Meta on conversion rate: email drove 9 leads from
  2,400 sends (0.375% lead rate) vs Meta's 42 leads from 8.2M impressions
  (0.0005% lead rate). The existing CRM list converts at a dramatically
  higher rate than cold paid audiences.

- The overall ROAS of 4.1x on a traditionally slow season demonstrates
  that monsoon Goa is a commercially viable campaign window with the
  right audience.

---

6. WHAT DIDN'T WORK
- The Meta creative did not reframe monsoon as a positive. The top-spend
  ad featured a bright sunny pool shot — which is cognitively dissonant
  for someone looking at a rainy June forecast. CTR at 1.1% was below
  the 1.8% benchmark for this audience and placement.

- CPL at ₹6,666 (Meta) and ₹8,823 (blended) exceeded the ₹5,000 target.
  The paid creative failed to differentiate enough from generic villa
  advertising to justify the premium Lohono charges.

---

9. THREE RECOMMENDATIONS

Recommendation 1: Lead with creator content, amplify with paid
Data basis: The influencer reel delivered 420K views and 2,100 saves
at near-zero cost. The paid creative delivered 8.2M impressions at
₹2.8L with lower intent signals.
Action: For the next monsoon campaign, commission 2 creator stays in
the first two weeks. Identify the top-performing reel by day 7 and
put ₹80,000 of paid amplification behind it rather than producing
separate ad creative.

Recommendation 2: Reframe monsoon as the reason to go, not to wait
Data basis: Lead-to-booking conversion was 13.7% — respectable — but
total leads were 15% below target, suggesting a top-of-funnel messaging
failure, not a sales failure.
Action: Build the next monsoon campaign around a specific monsoon
sensory truth: the Goa villa in rain looks and feels different from the
sun-drenched version — and some guests specifically prefer it. Show the
villa in actual monsoon conditions in the hero creative.

Recommendation 3: Double the email send volume for the next campaign
Data basis: Email drove leads at 75x the efficiency of paid social
(0.375% vs 0.0005% lead conversion rate).
Action: Segment the CRM for the next campaign by guests who have stayed
in Goa OR enquired and not converted. Build a 3-part email sequence
(not a single send) with a monsoon angle and a clear lead-nurture path
to a WhatsApp consultation.
```

---

## Combining Skills: End-to-End Workflows

The skills are designed to work together. Here are two common workflows.

### Workflow A: New Campaign from Scratch

```
Step 1  /lohono-persona    → Build the target guest persona
Step 2  /lohono-brief      → Write the campaign brief (using insights from Step 1)
Step 3  /lohono-adcopy     → Generate ad copy for each channel
Step 4  /lohono-linkedin   → Create LinkedIn content for the campaign
Step 5  /lohono-review     → Review all copy before sending to creative team
Step 6  /lohono-report     → Report on results after the campaign runs
```

### Workflow B: Content Quality Check Before Publishing

```
Step 1  /lohono-review     → Paste any draft caption, ad, or email for review
Step 2  (refine based on feedback)
Step 3  /lohono-review     → Re-review the revised version (score should improve)
```

### Workflow C: Rapid LinkedIn Calendar

```
/lohono-linkedin  Topic: Harmony Weddings in Goa
/lohono-linkedin  Topic: Why the best corporate retreats happen away from cities
/lohono-linkedin  Topic: The Lohono Infinity programme — what returning guests get
/lohono-linkedin  Topic: Alibaug: the case for 48 hours away
```

Each invocation produces 2 posts. Four invocations = 8 posts (a month's LinkedIn calendar).

---

## Tips for Best Results

**Be specific in your inputs.**
"Goa honeymoon campaign" gets you a good brief. "Goa honeymoon campaign targeting couples in Mumbai aged 28–35 who follow travel creators, with a goal of 40 enquiries for the December–January window" gets you a great one.

**You can front-load all inputs in one message.**
You don't need to wait for Claude to ask each question. Provide all inputs in your first message and Claude will proceed directly to the output.

**Use `/lohono-review` on your own drafts, not just others'.**
Even experienced writers benefit from the brand review. Paste your draft before it goes to the creative team or gets published.

**For `/lohono-report`, partial data is fine.**
If you only have some of the metrics, paste what you have. The report will flag missing data explicitly and work with what's available.

**Iterate on the outputs.**
If a LinkedIn post is 90% right but one line is off, tell Claude: "Keep everything except the CTA — rewrite it to feel less like a link-in-bio prompt." The skill holds context within the session.

**The brand guide is always active.**
You never need to remind Claude not to say "world-class" or "luxury redefined." The skill knows the banned phrases and enforces them in everything it produces — including the revised version in `/lohono-review`.

---

## Adding More Lohono Skills

To add a new skill to this collection (e.g., `/lohono-email` for email copywriting or `/lohono-whatsapp` for WhatsApp sales scripts):

1. Copy `_templates/SKILL-TEMPLATE.md` to `marketing/lohono-{name}/SKILL.md`
2. Reference `marketing/lohono-brief/references/lohono-brand-guide.md` for brand context
3. Add the skill to `README.md` and `.claude-plugin/marketplace.json`
4. Follow the commit convention: `feat(marketing): add lohono-{name} skill`

---

*For questions about brand voice or to update the brand guide, edit `marketing/lohono-brief/references/lohono-brand-guide.md` — all skills reference it.*
