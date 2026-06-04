# 📓 CivicPulse — Developer Journal

> A honest, daily record of building CivicPulse from zero.
> Written by a first-year developer. No filter. Real progress, real failures.

---

## Phase 1, Day 1 — June 3, 2026

### 🌅 How Today Started

I woke up at 6:45 AM knowing I wanted to actually build something that mattered today — not a todo app, not a calculator, not another tutorial clone. I'd been thinking about civic tech for a while. The idea that hit me was simple but it felt real: **why is it so hard to know what your city government is actually doing?**

I spent about 45 minutes before writing a single line of code just thinking through the problem on paper. I wrote out these questions:

- Who is the user? (Any resident. Non-technical. On their phone during a commute.)
- What's the core pain? (Government data exists but is scattered, jargon-heavy, and not real-time.)
- What's the MVP? (Votes + Budget + Meetings + Infrastructure — the four things that affect your daily life most directly.)
- What does success look like? (A person can open one URL and understand what their city is doing right now, in under 30 seconds.)

That last question was the one that shaped everything. 30 seconds. That's the constraint.

---

### 🏗️ What I Built Today

**The full Phase 1 application.** Here's a breakdown:

#### 1. Project Architecture Decision
I made a deliberate choice to use **zero frameworks and zero dependencies** for Phase 1. No React, no Vue, no npm, no webpack. Just HTML, CSS, and vanilla JavaScript.

**Why?** Three reasons:
1. I want anyone to be able to fork this and run it by literally double-clicking a file. No setup barrier.
2. Government websites need to be accessible on old devices and slow connections. A 2MB React bundle fails that test.
3. I'm learning the fundamentals. Building in vanilla JS forces me to understand what frameworks are actually doing under the hood.

This was a real architectural decision, not laziness. I'll add a backend (Node.js + Express) in Phase 2 when I need persistent data.

#### 2. The Four Panels

**Vote Tracker** — This was the hardest panel to design because votes have *state*. A vote can be Live (happening now), Pending (scheduled), Passed, or Failed. I built a status icon system using colored circles and symbols. The expandable card pattern — click to reveal the vote description and a yea/nay bar chart — took me about an hour to get right. The CSS transition from `display:none` to visible while also animating the bar fill required me to use `requestAnimationFrame()` for the first time, which was a new concept I had to research.

**Budget Visualizer** — This one taught me about CSS custom properties (variables). I defined all the colors as `--civic`, `--accent`, `--gold` etc. at the `:root` level, which made theming the whole app dramatically easier. The animated budget bars use a `data-target` attribute trick I came up with: set the width to `0%` in the HTML, then JavaScript reads the `data-target` and sets the final width after a 200ms delay, so the CSS transition plays on load. Feels polished.

**Meeting Calendar** — The RSVP button was my first real user-interaction feature. It uses `classList.toggle()` to flip between states and calls a `showToast()` function to give the user feedback. Small thing, but it felt like a real product moment when I tested it.

**Infrastructure Status Board** — I used a three-tier severity system (critical/warning/ok) that changes both the right-side accent stripe color AND the status text color. The "Report Issue" button demonstrates the future city API integration pattern — right now it fires a toast notification, but in Phase 2 it'll POST to a city endpoint.

#### 3. Multi-City Support
I built a `CITY_DATA` object that holds data for multiple cities and a `renderCity()` function that re-renders all four panels when the city dropdown changes. This was my first real data architecture decision. I chose a nested object structure:

```javascript
CITY_DATA = {
  boston: {
    budget: { ... },
    votes: [ ... ],
    meetings: [ ... ],
    infra: [ ... ]
  },
  nyc: { ... },
  ...
}
```

This makes it easy to add new cities — you just add a new key with the same shape. In Phase 2, this structure will map directly to API endpoint calls.

#### 4. The Animated Number Counter
When a city loads, the stats in the hero section count up from 0 to the actual number. This is done with `setInterval()`:

```javascript
function animateCount(id, target) {
  let start = 0;
  const step = Math.ceil(target / 20);
  const timer = setInterval(() => {
    start = Math.min(start + step, target);
    el.textContent = start;
    if (start >= target) clearInterval(timer);
  }, 40);
}
```

Simple, but it makes the dashboard feel alive. Little details like this are what separate a project from a demo.

#### 5. The Toast Notification System
I built a reusable toast system that can be called from anywhere in the app:

```javascript
showToast('📅 RSVP Confirmed', 'You\'re registered for: City Council Session');
```

It uses CSS transitions (`transform: translateY`) to slide in from the bottom-right. The hardest part was the auto-dismiss logic — I used `clearTimeout()` to reset the timer if multiple toasts fire in sequence, so they don't stack awkwardly.

#### 6. Design System
I spent real time on the visual design because I believe **a civic tool that looks professional gets used**. The aesthetic is inspired by newspaper editorial design — the kind of visual language people already trust for serious information. 

I used:
- **Syne** (display font — geometric, authoritative) for headlines and numbers
- **DM Mono** (monospace) for labels, metadata, and UI chrome — gives a "data dashboard" feel
- **Lora** (serif) for body text — readable, editorial, warm

The color palette is deliberately muted and papery (`#f5f0e8` background, `#1a3a2a` civic green) with `#c84b2f` as a sharp accent for alerts and active states. This avoids the generic "startup purple gradient" that makes most apps look the same.

---

### 🐛 Problems I Hit Today

**Problem 1: The CSS animation on SVG pulse didn't work**
I put the `@keyframes` inside the SVG's `<style>` tag but the browser couldn't find it from the outer CSS. Fixed by keeping all animations in the `<head>` style block, except for SVG-specific ones which need to live inside the SVG itself.

**Problem 2: The ticker scroll jumped**
My first version of the ticker stopped and restarted visibly. The fix was duplicating all ticker items in JavaScript so the list is twice as long as the container — when the animation reaches 50%, it wraps back to 0% and looks seamless because the second half is identical to the first.

**Problem 3: Modal closed when clicking inside it**
My `onclick="closeModal(event)"` on the overlay also fired when clicking the modal content inside it. Fixed with event propagation: only close if `event.target === overlay` (the backdrop itself), not any child element.

**Problem 4: Budget bars didn't animate on city switch**
When switching cities, the budget bars were already rendered and the CSS transition didn't replay. Fixed by setting the width to `0%` every time `renderBudget()` runs, then using `requestAnimationFrame()` + `setTimeout(200)` to trigger the animation after the DOM update.

---

### 📚 New Things I Learned Today

1. **`requestAnimationFrame()`** — tells the browser to run a function before the next repaint. Critical for triggering CSS transitions programmatically.

2. **CSS custom properties (`var()`)** — much more powerful than I thought. You can change a whole theme by changing 10 `:root` variables.

3. **`position: sticky`** — the budget sidebar stays visible as you scroll the vote list. I'd read about this but never used it in production.

4. **SVG inline animation** — `@keyframes` inside an SVG's `<style>` scope works independently from the page's CSS scope.

5. **`classList.toggle()` vs `.add()/.remove()`** — toggle is cleaner for binary states like expanded/collapsed.

6. **Semantic HTML matters** — using `<header>`, `<main>`, `<section>`, `<footer>` instead of nested `<div>`s is both better for accessibility and makes the CSS more readable.

---

### 🤔 Decisions I'm Uncertain About

**1. Is vanilla JS the right call long-term?**
For a dashboard that re-renders on city switch, I'm already manually updating the DOM in multiple places. If the app grows, this becomes hard to maintain. React's component model would make state management cleaner. But I stand by the decision for Phase 1 — I need to understand the problem before I abstract it.

**2. Should the data structure be an array or a map?**
I used a plain object keyed by city name. An array with `.find()` would be more "correct" but the object gives me O(1) lookup by key which matters when switching cities. I'll revisit this when there are 50+ cities.

**3. Accessibility — I haven't done enough**
The RSVP button has no ARIA label. The vote cards expand on click but a keyboard user can't navigate them. This is a real gap I need to fix in Day 2. Every resident means every resident, including those using screen readers.

---

### 📊 Today's Stats

| Metric | Value |
|---|---|
| Lines of code written | ~820 |
| Hours worked | ~7.5 |
| Bugs squashed | 7 |
| Stack Overflow visits | 4 |
| MDN Web Docs visits | 11 |
| Times I considered using React | 3 |
| Times I stayed with vanilla JS | 3 |
| Cups of coffee | 2 |

---

### 🎯 What Phase 1, Day 2 Will Cover

1. **Keyboard navigation** — every interactive element should be reachable by Tab key
2. **ARIA labels** — proper accessibility markup throughout
3. **`CONTRIBUTING.md`** — clear guide for other developers who want to add cities
4. **GitHub Pages deployment** — get the live URL working
5. **Open Graph meta tags** — so when shared on social media it shows a proper preview card
6. **Start the Node.js backend** — basic Express server structure for Phase 2 API integration
7. **Unit tests** — test the `renderVotes()`, `renderBudget()`, and city-switching logic

---

### 💭 Final Thought for Day 1

The thing that stuck with me today is how much of software is just **deciding what to leave out**. I could have built a social feed, a comment system, a map view, push notifications. I didn't. I built four things and made them work well.

There's a civic tech quote I came across while researching today from Micah Sifry's work on digital democracy: the best civic technology is the kind that gets out of the way and lets citizens and government actually connect. That's the north star for CivicPulse.

The code works. The idea is real. The work continues tomorrow.

---

*Next entry: [Phase 1, Day 2 →]()*

---

**Journal Index**
- [Phase 1, Day 1](JOURNAL.md) ← You are here
- Phase 1, Day 2 *(coming soon)*
- Phase 1, Day 3 *(coming soon)*

