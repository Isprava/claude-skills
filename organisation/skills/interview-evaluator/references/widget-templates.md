# Widget Templates

Starter HTML/JS patterns for both widgets. These are structural scaffolds — fill in content from the role analysis. Do not copy colors or dimension names without substituting role-specific values.

---

## Widget 1 — Dimension Scorecard

### Structure
- Candidate bar (top, always visible)
- Tab bar (one tab per dimension + Summary)
- Active panel (switches on tab click)
- Summary panel auto-calculates weighted score

### Key JS patterns

**State management:**
```javascript
const weights = [0.25, 0.25, 0.20, 0.15, 0.15]; // must sum to 1.0
const scores = [0, 0, 0, 0, 0];
const rated = [false, false, false, false, false];
```

**Weighted score calculation:**
```javascript
function calcWeighted() {
  let total = 0, weight = 0;
  for (let i = 0; i < scores.length; i++) {
    if (rated[i]) { total += scores[i] * weights[i]; weight += weights[i]; }
  }
  return weight > 0 ? total / weight : null;
}
```

**Verdict thresholds:**
```javascript
const score = calcWeighted();
if (score >= 4.0) verdict = 'Strong hire';
else if (score >= 3.0) verdict = 'Lean hire';
else verdict = 'Pass';
```

**Star rating builder:**
```javascript
function buildStars(dimIndex, containerId) {
  const container = document.getElementById(containerId);
  for (let s = 1; s <= 5; s++) {
    const btn = document.createElement('button');
    btn.className = 'star';
    btn.textContent = s;
    btn.style.fontSize = '12px';
    btn.onclick = () => rate(dimIndex, s);
    container.appendChild(btn);
  }
}
function rate(dim, val) {
  scores[dim] = val;
  rated[dim] = true;
  // update star fills
  const btns = document.getElementById('stars-' + dim).querySelectorAll('.star');
  btns.forEach((b, i) => b.classList.toggle('filled', i < val));
  document.getElementById('val-' + dim).textContent = val + '/5';
  updateSummary();
}
```

### CSS classes required
```css
.star { width:28px;height:28px;border-radius:6px;border:0.5px solid var(--color-border-secondary);background:transparent;cursor:pointer;font-size:12px;display:flex;align-items:center;justify-content:center; }
.star.filled { background:var(--color-background-warning);border-color:var(--color-border-warning); }
.tab { font-size:12px;padding:6px 12px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);background:transparent;color:var(--color-text-secondary);cursor:pointer; }
.tab.active { background:var(--color-background-secondary);color:var(--color-text-primary);border-color:var(--color-border-primary);font-weight:500; }
```

### Candidate bar pattern
```html
<div style="display:flex;gap:16px;background:var(--color-background-secondary);border-radius:var(--border-radius-md);padding:10px 14px;margin-bottom:1.5rem;align-items:center;">
  <div>
    <div style="font-size:14px;font-weight:500;color:var(--color-text-primary);">[CANDIDATE NAME]</div>
    <div style="font-size:12px;color:var(--color-text-secondary);">[KEY CREDENTIALS FROM RESUME]</div>
  </div>
  <div style="margin-left:auto;font-size:12px;background:var(--color-background-warning);color:var(--color-text-warning);padding:3px 8px;border-radius:var(--border-radius-md);">Key gap: [PRIMARY GAP]</div>
</div>
```

### Question block pattern
```html
<div style="background:var(--color-background-secondary);border-radius:var(--border-radius-md);padding:12px;margin-bottom:8px;">
  <div style="font-size:11px;color:var(--color-text-secondary);margin-bottom:4px;">[Q LABEL]</div>
  <div style="font-size:13px;color:var(--color-text-primary);line-height:1.5;margin-bottom:6px;font-weight:500;">"[EXACT QUESTION TEXT]"</div>
  <div style="font-size:12px;color:var(--color-text-secondary);line-height:1.5;">[WHAT TO LISTEN FOR]</div>
</div>
```

### Flag grid pattern
```html
<div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:8px;">
  <div style="background:var(--color-background-success);border:0.5px solid var(--color-border-success);border-radius:var(--border-radius-md);padding:10px;">
    <div style="font-size:11px;font-weight:500;color:var(--color-text-success);margin-bottom:6px;">Green flags</div>
    <!-- flag items with ::before "· " -->
  </div>
  <div style="background:var(--color-background-danger);border:0.5px solid var(--color-border-danger);border-radius:var(--border-radius-md);padding:10px;">
    <div style="font-size:11px;font-weight:500;color:var(--color-text-danger);margin-bottom:6px;">Red flags</div>
  </div>
</div>
```

### Automatic disqualifier pattern (in Summary tab)
```html
<div style="margin-top:20px;padding-top:16px;border-top:0.5px solid var(--color-border-tertiary);">
  <div style="font-size:11px;font-weight:500;letter-spacing:.05em;color:var(--color-text-secondary);margin-bottom:8px;">Automatic disqualifiers</div>
  <!-- 2-3 role-specific behaviors that are instant no regardless of score -->
  <div style="background:var(--color-background-secondary);border-radius:var(--border-radius-md);padding:12px;margin-bottom:6px;">
    <div style="font-size:13px;font-weight:400;color:var(--color-text-danger);">[DISQUALIFIER TEXT]</div>
  </div>
</div>
```

---

## Widget 2 — Timed Interview Run Sheet

### Key data structure
```javascript
const blocks = [
  {
    id: 0,
    title: "Opening & context setting",
    minutes: 5,
    color: "#888780",
    dim: "Rapport",
    dimBg: "#F1EFE8",
    dimText: "#444441",
    goal: "[What you're trying to find out]",
    goalHighlight: "[The specific unknown this block resolves]",
    questions: [
      {
        label: "Set-up",
        q: '"[Exact words to say]"',
        listen: "[What to observe]"
      }
    ],
    green: ["[Observable behavior]"],
    red: ["[Observable behavior]"],
    stall: "[Verbatim rescue prompt if candidate freezes]"
  }
  // ... one object per block
];
```

### Timer logic
```javascript
let timerInterval = null;
let timerSeconds = 0;
let timerRunning = false;

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
      document.getElementById('timer-display').textContent = m + ':' + (s < 10 ? '0' : '') + s;
      const limit = blocks[current].minutes * 60;
      document.getElementById('timer-display').style.color =
        timerSeconds >= limit ? 'var(--color-text-danger)' : 'var(--color-text-primary)';
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
```

### Timeline bar builder
```javascript
function buildTimeline() {
  const total = blocks.reduce((s, b) => s + b.minutes, 0);
  const tl = document.getElementById('timeline');
  tl.innerHTML = '';
  blocks.forEach((b, i) => {
    const seg = document.createElement('div');
    seg.style.cssText = 'height:10px;cursor:pointer;transition:opacity .15s;';
    seg.style.background = b.color;
    seg.style.flex = b.minutes / total;
    if (i === current) seg.style.outline = '2px solid var(--color-border-primary)';
    seg.title = b.title + ' (' + b.minutes + ' min)';
    seg.onclick = () => goTo(i);
    tl.appendChild(seg);
  });
}
```

### Block card renderer
```javascript
function renderBlock() {
  const b = blocks[current];
  let minuteStart = 1;
  for (let i = 0; i < current; i++) minuteStart += blocks[i].minutes;

  const qs = b.questions.map(q => `
    <div style="background:var(--color-background-secondary);border-radius:var(--border-radius-md);padding:12px;margin-bottom:8px;">
      <div style="font-size:11px;color:var(--color-text-secondary);margin-bottom:4px;">${q.label}</div>
      <div style="font-size:13px;font-style:italic;color:var(--color-text-primary);line-height:1.5;margin-bottom:6px;">${q.q}</div>
      <div style="font-size:12px;color:var(--color-text-secondary);line-height:1.5;">${q.listen}</div>
    </div>
  `).join('');

  const stall = b.stall ? `
    <div style="margin-top:14px;padding:10px 12px;border-left:2px solid #7F77DD;background:#EEEDFE;border-radius:0;">
      <div style="font-size:12px;color:#3C3489;line-height:1.6;"><strong>If they stall:</strong> ${b.stall}</div>
    </div>
  ` : '';

  document.getElementById('block-card').innerHTML = `
    <div style="padding:14px 16px;display:flex;align-items:center;gap:12px;border-bottom:0.5px solid var(--color-border-tertiary);">
      <div style="width:10px;height:10px;border-radius:50%;background:${b.color};flex-shrink:0;"></div>
      <div style="font-size:15px;font-weight:500;color:var(--color-text-primary);flex:1;">${b.title}</div>
      <div style="font-size:12px;color:var(--color-text-secondary);background:var(--color-background-secondary);padding:3px 8px;border-radius:var(--border-radius-md);">Min ${minuteStart}–${minuteStart + b.minutes - 1} · ${b.minutes} min</div>
      <div style="font-size:11px;padding:3px 8px;border-radius:var(--border-radius-md);background:${b.dimBg};color:${b.dimText};">${b.dim}</div>
    </div>
    <div style="padding:16px;">
      <div style="font-size:13px;color:var(--color-text-secondary);line-height:1.6;margin-bottom:14px;padding-bottom:14px;border-bottom:0.5px solid var(--color-border-tertiary);">
        ${b.goal}<br><br><strong style="color:var(--color-text-primary);">${b.goalHighlight}</strong>
      </div>
      <div style="font-size:11px;font-weight:500;letter-spacing:.05em;text-transform:uppercase;color:var(--color-text-secondary);margin-bottom:8px;">Questions & what to listen for</div>
      ${qs}
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:14px;">
        <div style="background:var(--color-background-success);border:0.5px solid var(--color-border-success);border-radius:var(--border-radius-md);padding:10px;">
          <div style="font-size:11px;font-weight:500;color:var(--color-text-success);margin-bottom:5px;">Green flags</div>
          ${b.green.map(f => `<div style="font-size:12px;color:var(--color-text-primary);line-height:1.6;">· ${f}</div>`).join('')}
        </div>
        <div style="background:var(--color-background-danger);border:0.5px solid var(--color-border-danger);border-radius:var(--border-radius-md);padding:10px;">
          <div style="font-size:11px;font-weight:500;color:var(--color-text-danger);margin-bottom:5px;">Red flags</div>
          ${b.red.map(f => `<div style="font-size:12px;color:var(--color-text-primary);line-height:1.6;">· ${f}</div>`).join('')}
        </div>
      </div>
      ${stall}
    </div>
  `;
}
```

---

## Responsive guard

Both widgets must include this at the outermost container:
```css
box-sizing: border-box;
width: 100%;
overflow: hidden;
```

Flag grid must use `minmax(0, 1fr)` not `1fr` to prevent overflow on small containers:
```css
display: grid;
grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
gap: 8px;
```
