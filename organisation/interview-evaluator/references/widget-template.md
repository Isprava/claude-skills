# Widget Template Reference

This is the base HTML/JS scaffolding for the interview evaluator widget.
Do not copy verbatim — adapt `blocks[]`, `weights[]`, colors, dimension badges, and task content to the specific role and candidate.

---

## Base HTML structure

```html
<style>
*{box-sizing:border-box;margin:0;padding:0}
.wrap{padding:1rem 0;font-family:var(--font-sans)}
.timeline{display:flex;gap:3px;margin-bottom:1.5rem;border-radius:var(--border-radius-md);overflow:hidden}
.seg{height:10px;cursor:pointer;transition:opacity .15s}
.seg:hover{opacity:.75}
.seg.active{outline:2px solid var(--color-border-primary);outline-offset:1px}
.legend{display:flex;flex-wrap:wrap;gap:10px;margin-bottom:1.5rem}
.leg-item{display:flex;align-items:center;gap:5px;font-size:11px;color:var(--color-text-secondary);cursor:pointer}
.leg-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.block-nav{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:1.5rem}
.bn{font-size:11px;padding:5px 10px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);background:transparent;color:var(--color-text-secondary);cursor:pointer;white-space:nowrap}
.bn.active{background:var(--color-background-secondary);color:var(--color-text-primary);border-color:var(--color-border-primary);font-weight:500}
.block-card{background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);overflow:hidden}
.block-header{padding:14px 16px;display:flex;align-items:center;gap:12px;border-bottom:0.5px solid var(--color-border-tertiary)}
.bh-dot{width:10px;height:10px;border-radius:50%;flex-shrink:0}
.bh-title{font-size:15px;font-weight:500;color:var(--color-text-primary);flex:1}
.bh-time{font-size:12px;color:var(--color-text-secondary);font-weight:500;background:var(--color-background-secondary);padding:3px 8px;border-radius:var(--border-radius-md)}
.bh-dim{font-size:11px;padding:3px 8px;border-radius:var(--border-radius-md)}
.block-body{padding:16px}
.goal-row{font-size:13px;color:var(--color-text-secondary);line-height:1.6;margin-bottom:14px;padding-bottom:14px;border-bottom:0.5px solid var(--color-border-tertiary)}
.goal-row strong{color:var(--color-text-primary);font-weight:500}
.qs-label{font-size:11px;font-weight:500;letter-spacing:.05em;text-transform:uppercase;color:var(--color-text-secondary);margin-bottom:8px}
.q-item{margin-bottom:10px;padding:12px;background:var(--color-background-secondary);border-radius:var(--border-radius-md)}
.q-number{font-size:11px;color:var(--color-text-secondary);margin-bottom:4px}
.q-text{font-size:13px;color:var(--color-text-primary);line-height:1.5;margin-bottom:6px;font-style:italic}
.q-listen{font-size:12px;color:var(--color-text-secondary);line-height:1.5}
.q-listen span{color:var(--color-text-primary);font-weight:500}
.flags-row{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:14px}
.flag-mini{padding:10px;border-radius:var(--border-radius-md)}
.flag-mini.g{background:var(--color-background-success);border:0.5px solid var(--color-border-success)}
.flag-mini.r{background:var(--color-background-danger);border:0.5px solid var(--color-border-danger)}
.flag-mini-label{font-size:11px;font-weight:500;margin-bottom:5px}
.flag-mini.g .flag-mini-label{color:var(--color-text-success)}
.flag-mini.r .flag-mini-label{color:var(--color-text-danger)}
.flag-mini-item{font-size:12px;color:var(--color-text-primary);line-height:1.6}
.flag-mini-item::before{content:"· "}
.tip-box{margin-top:14px;padding:10px 12px;border-left:2px solid #7F77DD;background:#EEEDFE;border-radius:0}
.tip-box p{font-size:12px;color:#3C3489;line-height:1.6}
.nav-buttons{display:flex;justify-content:space-between;margin-top:1rem}
.timer-bar{display:flex;align-items:center;gap:10px;padding:10px 14px;background:var(--color-background-secondary);border-radius:var(--border-radius-md);margin-bottom:1.5rem}
.timer-label{font-size:12px;color:var(--color-text-secondary)}
.timer-val{font-size:18px;font-weight:500;color:var(--color-text-primary);font-variant-numeric:tabular-nums;min-width:52px}
.timer-btns{margin-left:auto;display:flex;gap:6px}
.tbtn{font-size:12px;padding:5px 10px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);background:transparent;color:var(--color-text-primary);cursor:pointer}
.summary-panel{background:var(--color-background-secondary);border-radius:var(--border-radius-lg);padding:16px}
.summary-row{display:flex;justify-content:space-between;align-items:center;padding:8px 0;border-bottom:0.5px solid var(--color-border-tertiary)}
.summary-row:last-of-type{border-bottom:none}
.summary-name{font-size:13px;color:var(--color-text-primary)}
.summary-score{font-size:13px;font-weight:500}
.total-row{margin-top:16px;padding:12px;border-radius:var(--border-radius-md);background:var(--color-background-primary);border:0.5px solid var(--color-border-secondary);display:flex;justify-content:space-between;align-items:center}
.total-label{font-size:15px;font-weight:500;color:var(--color-text-primary)}
.total-score{font-size:22px;font-weight:500}
.verdict{margin-top:12px;padding:10px 14px;border-radius:var(--border-radius-md);font-size:13px;line-height:1.5}
.verdict.strong{background:var(--color-background-success);color:var(--color-text-success)}
.verdict.lean{background:var(--color-background-warning);color:var(--color-text-warning)}
.verdict.pass{background:var(--color-background-danger);color:var(--color-text-danger)}
.stars{display:flex;gap:4px}
.star{width:28px;height:28px;border-radius:6px;border:0.5px solid var(--color-border-secondary);background:transparent;cursor:pointer;font-size:12px;display:flex;align-items:center;justify-content:center}
.star.filled{background:var(--color-background-warning);border-color:var(--color-border-warning)}
.score-row{display:flex;align-items:center;gap:12px;margin-top:16px;padding-top:16px;border-top:0.5px solid var(--color-border-tertiary)}
.score-label{font-size:13px;color:var(--color-text-secondary);flex:1}
.star-val{font-size:13px;font-weight:500;color:var(--color-text-primary);min-width:30px;text-align:right}
.dq-item{margin-bottom:6px;padding:10px 12px;background:var(--color-background-danger);border:0.5px solid var(--color-border-danger);border-radius:var(--border-radius-md);font-size:12px;line-height:1.5;color:var(--color-text-danger)}
.candidate-bar{display:flex;gap:16px;background:var(--color-background-secondary);border-radius:var(--border-radius-md);padding:10px 14px;margin-bottom:1.5rem;align-items:center}
.cb-name{font-size:14px;font-weight:500;color:var(--color-text-primary)}
.cb-detail{font-size:12px;color:var(--color-text-secondary)}
.cb-gap{margin-left:auto;font-size:12px;background:var(--color-background-warning);color:var(--color-text-warning);padding:3px 8px;border-radius:var(--border-radius-md)}
</style>

<div class="wrap">

<div class="timer-bar">
  <div class="timer-label">Block timer</div>
  <div class="timer-val" id="timer-display">0:00</div>
  <div class="timer-btns">
    <button class="tbtn" id="t-start" onclick="timerToggle()">Start</button>
    <button class="tbtn" onclick="timerReset()">Reset</button>
  </div>
  <div style="margin-left:12px;font-size:12px;color:var(--color-text-secondary)">Total: <span style="font-weight:500;color:var(--color-text-primary)">DURATION min</span></div>
</div>

<div class="candidate-bar">
  <div>
    <div class="cb-name">CANDIDATE_NAME</div>
    <div class="cb-detail">CANDIDATE_SUMMARY</div>
  </div>
  <div class="cb-gap">KEY_GAP</div>
</div>

<div class="timeline" id="timeline"></div>
<div class="legend" id="legend"></div>
<div class="block-nav" id="block-nav"></div>
<div class="block-card" id="block-card"></div>

<div class="nav-buttons">
  <button class="tbtn" onclick="prevBlock()" id="btn-prev">← Prev block</button>
  <button class="tbtn" onclick="nextBlock()" id="btn-next">Next block →</button>
</div>

</div>

<script>
// ── REPLACE THIS DATA ─────────────────────────────────────────────────
const blocks = [
  {
    id: 0,
    title: "Opening & context setting",
    minutes: 5,
    color: "#888780",
    dim: "Rapport",
    dimColor: "#F1EFE8",
    dimText: "#444441",
    goal: "Calibrate, not evaluate. Watch how they hold themselves in the first 2 minutes.",
    insight: "First unprompted question tells you more than the answer to your first question.",
    questions: [
      {
        n: "Set-up",
        q: "\"Today I want to understand how you think, not just what you know. Don't worry about perfect answers — I care about how you reason.\"",
        listen: "Say this verbatim. Watch if they visibly relax or get more nervous. Relaxed = confident in their reasoning. More nervous = rehearsed answers they can no longer deploy."
      },
      {
        n: "Warm-up",
        q: "\"Tell me in 60 seconds what you have been up to since [last role / graduation] — work, projects, anything you have tried on your own.\"",
        listen: "<span>Listen for:</span> self-directed activity. Projects beat certificates. Initiative beats credentials."
      }
    ],
    green: ["Asks a clarifying question unprompted", "Mentions self-initiated work beyond coursework", "Energy and specificity in how they describe themselves"],
    red: ["Lists qualifications instead of describing themselves", "Waits passively for next question after answering", "Only describes formal credentials"]
  }
  // Add remaining blocks here — one per dimension, plus live task, plus close
];

// One weight per scored dimension (exclude opening and close from scoring)
// Must sum to 1.0
const weights = [0.25, 0.25, 0.25, 0.15, 0.10];

// Automatic disqualifiers — role-specific, shown in Summary tab
const disqualifiers = [
  "Role-specific disqualifier 1 — describe the behaviour and why it is fatal for this role",
  "Role-specific disqualifier 2",
  "Role-specific disqualifier 3 — live task: no structured output and no process = automatic pass for execution roles"
];

// Scorecard dimension labels (must match weights array length)
const dimLabels = [
  "Dimension 1 name (weight%)",
  "Dimension 2 name (weight%)",
  "Dimension 3 name (weight%)",
  "Dimension 4 name (weight%)",
  "Dimension 5 name (weight%)"
];
// ── END REPLACE ────────────────────────────────────────────────────────

let current = 0;
let timerInterval = null;
let timerSeconds = 0;
let timerRunning = false;
const scores = new Array(weights.length).fill(0);
const rated = new Array(weights.length).fill(false);

function buildTimeline() {
  const total = blocks.reduce((s, b) => s + b.minutes, 0);
  const tl = document.getElementById('timeline');
  tl.innerHTML = '';
  blocks.forEach((b, i) => {
    const seg = document.createElement('div');
    seg.className = 'seg' + (i === current ? ' active' : '');
    seg.style.background = b.color;
    seg.style.flex = b.minutes / total;
    seg.title = b.title + ' (' + b.minutes + ' min)';
    seg.onclick = () => goTo(i);
    tl.appendChild(seg);
  });
}

function buildLegend() {
  const lg = document.getElementById('legend');
  lg.innerHTML = '';
  blocks.forEach((b, i) => {
    const item = document.createElement('div');
    item.className = 'leg-item';
    item.onclick = () => goTo(i);
    item.innerHTML = '<div class="leg-dot" style="background:' + b.color + '"></div><span>' + b.minutes + 'min — ' + b.title + '</span>';
    lg.appendChild(item);
  });
}

function buildNav() {
  const nav = document.getElementById('block-nav');
  nav.innerHTML = '';
  const allTabs = [...blocks.map(b => b.title.split(' ').slice(0,2).join(' ')), 'Summary'];
  allTabs.forEach((label, i) => {
    const btn = document.createElement('button');
    btn.className = 'bn' + (i === current ? ' active' : '');
    btn.textContent = (i + 1) + '. ' + label;
    btn.onclick = () => goTo(i);
    nav.appendChild(btn);
  });
}

function renderBlock() {
  const totalTabs = blocks.length + 1;
  const isSummary = current === totalTabs - 1;

  document.getElementById('btn-prev').style.opacity = current === 0 ? '0.3' : '1';
  document.getElementById('btn-next').style.opacity = current === totalTabs - 1 ? '0.3' : '1';

  if (isSummary) {
    renderSummary();
    return;
  }

  const b = blocks[current];
  let minutesUsed = 0;
  for (let i = 0; i < current; i++) minutesUsed += blocks[i].minutes;

  const qs = b.questions.map(q => `
    <div class="q-item">
      <div class="q-number">${q.n}</div>
      <div class="q-text">${q.q}</div>
      <div class="q-listen">${q.listen}</div>
    </div>`).join('');

  const flags = `<div class="flags-row">
    <div class="flag-mini g">
      <div class="flag-mini-label">Green flags</div>
      ${b.green.map(f => `<div class="flag-mini-item">${f}</div>`).join('')}
    </div>
    <div class="flag-mini r">
      <div class="flag-mini-label">Red flags</div>
      ${b.red.map(f => `<div class="flag-mini-item">${f}</div>`).join('')}
    </div>
  </div>`;

  const tip = b.tip ? `<div class="tip-box"><p><strong>If they stall:</strong> ${b.tip}</p></div>` : '';

  document.getElementById('block-card').innerHTML = `
    <div class="block-header">
      <div class="bh-dot" style="background:${b.color}"></div>
      <div class="bh-title">${b.title}</div>
      <div class="bh-time">Min ${minutesUsed + 1}–${minutesUsed + b.minutes} · ${b.minutes} min</div>
      <div class="bh-dim" style="background:${b.dimColor};color:${b.dimText}">${b.dim}</div>
    </div>
    <div class="block-body">
      <div class="goal-row">${b.goal}<br><br><strong>${b.insight}</strong></div>
      <div class="qs-label">Questions & what to listen for</div>
      ${qs}
      ${flags}
      ${tip}
    </div>`;
}

function renderSummary() {
  const rows = dimLabels.map((label, d) => {
    const starsHtml = Array.from({length: 5}, (_, s) => {
      const filled = rated[d] && s < scores[d] ? ' filled' : '';
      return `<button class="star${filled}" onclick="rate(${d}, ${s+1})">${s+1}</button>`;
    }).join('');
    const scoreText = rated[d] ? scores[d] + '/5' : 'Not rated';
    const scoreColor = rated[d]
      ? (scores[d] >= 4 ? 'var(--color-text-success)' : scores[d] >= 3 ? 'var(--color-text-warning)' : 'var(--color-text-danger)')
      : 'var(--color-text-secondary)';
    return `
      <div class="summary-row">
        <span class="summary-name">${label}</span>
        <div class="score-row" style="margin:0;padding:0;border:none;flex-direction:row;gap:8px">
          <div class="stars">${starsHtml}</div>
          <div class="star-val" style="color:${scoreColor}">${scoreText}</div>
        </div>
      </div>`;
  }).join('');

  let weighted = 0;
  let totalW = 0;
  rated.forEach((r, d) => { if (r) { weighted += scores[d] * weights[d]; totalW += weights[d]; } });

  let totalHtml = '—';
  let verdictHtml = '';
  if (totalW > 0) {
    const adj = weighted / totalW;
    const col = adj >= 4 ? 'var(--color-text-success)' : adj >= 3 ? 'var(--color-text-warning)' : 'var(--color-text-danger)';
    totalHtml = `<span style="color:${col}">${adj.toFixed(1)} / 5</span>`;
    const cls = adj >= 4 ? 'strong' : adj >= 3 ? 'lean' : 'pass';
    const msg = adj >= 4
      ? 'Strong hire signal. Proceed to offer stage.'
      : adj >= 3
        ? 'Lean hire — review which dimensions pulled the score down. A role-critical dimension below 3 is a serious flag.'
        : 'Pass. Candidate does not meet the bar for this role.';
    verdictHtml = `<div class="verdict ${cls}">${msg}</div>`;
  }

  const dqHtml = disqualifiers.map(d => `<div class="dq-item">${d}</div>`).join('');

  document.getElementById('block-card').innerHTML = `
    <div class="block-header">
      <div class="bh-dot" style="background:#888780"></div>
      <div class="bh-title">Interview summary</div>
      <div class="bh-dim" style="background:var(--color-background-secondary);color:var(--color-text-secondary)">Weighted scorecard</div>
    </div>
    <div class="block-body">
      <div class="summary-panel">${rows}</div>
      <div class="total-row">
        <span class="total-label">Weighted score</span>
        <span class="total-score">${totalHtml}</span>
      </div>
      ${verdictHtml}
      <div class="qs-label" style="margin-top:20px;padding-top:16px;border-top:0.5px solid var(--color-border-tertiary)">Automatic disqualifiers</div>
      <div style="margin-top:8px">${dqHtml}</div>
    </div>`;
}

function rate(dim, val) {
  scores[dim] = val;
  rated[dim] = true;
  renderSummary();
}

function goTo(i) {
  const totalTabs = blocks.length + 1;
  current = Math.max(0, Math.min(i, totalTabs - 1));
  buildTimeline();
  buildNav();
  renderBlock();
  timerReset();
}

function nextBlock() { goTo(current + 1); }
function prevBlock() { goTo(current - 1); }

function timerToggle() {
  if (timerRunning) {
    clearInterval(timerInterval);
    timerRunning = false;
    document.getElementById('t-start').textContent = 'Resume';
  } else {
    timerRunning = true;
    document.getElementById('t-start').textContent = 'Pause';
    timerInterval = setInterval(() => {
      timerSeconds++;
      const m = Math.floor(timerSeconds / 60);
      const s = timerSeconds % 60;
      const disp = document.getElementById('timer-display');
      disp.textContent = m + ':' + (s < 10 ? '0' : '') + s;
      const limit = current < blocks.length ? blocks[current].minutes * 60 : Infinity;
      disp.style.color = timerSeconds >= limit ? 'var(--color-text-danger)' : 'var(--color-text-primary)';
    }, 1000);
  }
}

function timerReset() {
  clearInterval(timerInterval);
  timerRunning = false;
  timerSeconds = 0;
  document.getElementById('timer-display').textContent = '0:00';
  document.getElementById('timer-display').style.color = 'var(--color-text-primary)';
  document.getElementById('t-start').textContent = 'Start';
}

buildTimeline();
buildLegend();
buildNav();
renderBlock();
</script>
```

---

## Notes on adapting this template

1. Replace everything in the `// ── REPLACE THIS DATA ──` section with role-specific content
2. The `blocks[]` array drives everything — timeline, navigation, content, timer
3. `weights[]` must have the same length as `dimLabels[]` and must sum to 1.0
4. The Summary tab is auto-generated from `dimLabels`, `weights`, and `disqualifiers` — no separate block needed
5. Add a `tip` key to any block that needs a stall nudge — omit the key entirely if no nudge is needed
6. The opening block and close block are typically not scored (they reveal character, not skill) — only include dimensions in `dimLabels` that map to your scored blocks
