# CivicWatch — Real-Time Civic Engagement Dashboard

![Version](https://img.shields.io/badge/version-1.0.0-green)
![License](https://img.shields.io/badge/license-MIT-blue)
![Status](https://img.shields.io/badge/status-active-brightgreen)
![Phase](https://img.shields.io/badge/phase-1--day--1-orange)
![HTML](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)

> **"Democracy works better when people actually know what's happening."**

CivicWatch is a real-time, open-source civic transparency dashboard that aggregates local government data — council votes, annual budgets, public meetings, and infrastructure alerts — into a single, clean, resident-facing interface. No login required. No paywall. Just your city, fully visible.

---

## The Problem

Most cities publish public data — but it's buried across 6 different websites, written in government jargon, and impossible to track in real time. As a result:

- **Fewer than 8%** of residents attend public meetings, even when they directly affect their neighborhood
- Budget allocations are decided with almost no public awareness
- Infrastructure failures (water advisories, transit outages) spread faster on social media than official channels
- Council votes on zoning, housing, and safety pass with minimal scrutiny

**CivicWatch solves this.** One dashboard. Every city. Every resident.

---

## Features

### Live Vote Tracker
- Real-time status of all active city council votes (Live / Pending / Passed / Failed)
- Expandable vote cards showing description, vote counts, and visual yea/nay breakdown
- Impact tagging (High / Medium / Low) so residents know what matters most

### Annual Budget Visualizer
- Full breakdown of city budget allocation by department
- Percentage bars with dollar amounts for each category
- Year-over-year change indicator

### Public Meeting Calendar
- Upcoming city council sessions, zoning boards, and planning meetings
- One-click RSVP tracking so residents never miss a meeting
- Agenda item counts so you know what's being decided

### Infrastructure Status Board
- Live status for roads, bridges, water systems, power grid, and transit
- Three-tier alert system: Critical / Warning / OK
- Resident issue reporting with direct city routing

### Multi-City Support
- Switch between 6+ major cities with one dropdown
- Boston, New York, Chicago, LA, Houston, Seattle
- Designed to scale to any city with open data APIs

### Live News Ticker
- Continuous scrolling feed of active civic events
- Color-coded by urgency (red/yellow/green)

### Unified Search
- Single search bar across votes, meetings, projects, and alerts

---

## Tech Stack

| Layer | Technology | Why |
|---|---|---|
| Frontend | HTML5, CSS3, Vanilla JS | Zero dependencies, maximum accessibility |
| Fonts | Google Fonts (Syne, DM Mono, Lora) | Distinctive editorial aesthetic |
| Data | Embedded JS objects (v1) → City Open Data APIs (v2) | Progressive enhancement |
| Hosting | GitHub Pages | Free, open, always available |
| Future | Node.js + Express backend, PostgreSQL | Persistent data + real API integration |

**No frameworks. No build tools. No npm.** This is intentional — CivicWatch is designed to run in any browser, on any device, without a build step. Accessibility first.

---

## Getting Started

### Option 1 — View Live (GitHub Pages)
Visit: `https://github.com/neodragon-tuff/CivicWatch.git`

### Option 2 — Run Locally
```bash
# Clone the repository
git clone git clone https://github.com/neodragon-tuff/CivicWatch.git

# Navigate into the project
cd civicwatch

# Open in browser (no server needed)
open index.html
# or on Windows:
start index.html
# or on Linux:
xdg-open index.html
```

That's it. No `npm install`. No `.env` file. No Docker. Just open and run.

---

## Project Structure

```
civicwatch/
├── index.html              # Main application (self-contained)
├── README.md               # This file
├── LICENSE                 # MIT License
├── CONTRIBUTING.md         # How to contribute
├── .gitignore              # Git ignore rules
├── docs/
│   ├── JOURNAL.md          # Daily developer journal
│   ├── ROADMAP.md          # Feature roadmap
│   └── API_SOURCES.md      # City open data API references
└── src/                    # Future modular source files
    ├── data/               # City data modules
    ├── components/         # Reusable UI components
    └── utils/              # Helper functions
```

---

## Roadmap

### Phase 1 — Foundation (Current)
- [x] Core dashboard UI with all four main panels
- [x] Multi-city support (6 cities)
- [x] Vote tracker with expandable detail
- [x] Budget visualizer with animated bars
- [x] Meeting calendar with RSVP
- [x] Infrastructure status board
- [x] Live news ticker
- [x] Toast notification system
- [x] Responsive mobile layout
- [x] GitHub Pages deployment

### Phase 2 — Real Data Integration
- [ ] Connect to Boston Open Data API (`data.boston.gov`)
- [ ] Connect to NYC Open Data API (`data.cityofnewyork.us`)
- [ ] Node.js backend for data caching and normalization
- [ ] Scheduled API polling (every 15 minutes)
- [ ] Email/SMS alert subscriptions for votes and meetings

### Phase 3 — Community Features
- [ ] User accounts (civic identity, no social media)
- [ ] Comment threads on votes and meetings
- [ ] Neighborhood-level filtering
- [ ] Petition creation linked to open votes
- [ ] Accessibility: screen reader optimization, language support

### Phase 4 — Scale
- [ ] 50-city coverage via open data partnerships
- [ ] Mobile app (React Native)
- [ ] Embed widget for local news sites
- [ ] Data export (CSV, JSON) for journalists and researchers

---

## Real Data Sources

CivicWatch is designed to pull from these **free, public government APIs**:

| City | Portal | API |
|---|---|---|
| Boston | data.boston.gov | Socrata Open Data API |
| New York | data.cityofnewyork.us | NYC Open Data API |
| Chicago | data.cityofchicago.org | Socrata Open Data API |
| Los Angeles | data.lacity.org | Socrata Open Data API |
| Seattle | data.seattle.gov | Socrata Open Data API |
| Federal | api.congress.gov | Congress.gov API |

All data sources are **100% free and public** under open government data laws (US FOIA, state-level equivalents).

---

## Contributing

Contributions are genuinely welcome. CivicWatch is a civic project — it belongs to everyone.

**Ways to help:**
- Add your city's data
- Improve accessibility (ARIA labels, keyboard nav)
- Build the Node.js backend
- Write tests
- Translate the UI

See [CONTRIBUTING.md](docs/CONTRIBUTING.md) for detailed guidelines.

```bash
# Fork the repo on GitHub, then:
git clone https://github.com/[your-fork]/civicwatch.git
git checkout -b feature/your-feature-name
# Make your changes
git commit -m "feat: describe your change clearly"
git push origin feature/your-feature-name
# Open a Pull Request
```

---

## Developer Journal

I'm documenting every day of development in [`docs/JOURNAL.md`](docs/JOURNAL.md).

This includes what I built, what broke, what I learned, and what's next. If you're learning to code or interested in civic tech, the journal is a real, honest record of how this project was built from scratch.

---

## License

MIT License — see [LICENSE](LICENSE) for full text.

You are free to use, copy, modify, and distribute this project for any purpose, including commercial use, as long as you include the original license.

---

## Author

Built by a first-year developer passionate about civic technology and government transparency.

- **GitHub:** [@neodragon-tuff](https://github.com/neodragon-tuff)
- **Project started:** June 3, 2026
- **Status:** Active development

---

## ⭐ If This Helps You

If CivicWatch is useful to you, your city, or your newsroom — **star the repo**. It helps more people find it, and it helps me keep building.

> *"The price of liberty is eternal vigilance."* — Thomas Jefferson

