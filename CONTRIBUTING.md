# Contributing to CivicWatch

Thank you for wanting to contribute. CivicWatch is a civic project — it works better the more people are involved.

## Ways to Contribute

- **Add your city's data** — the most impactful contribution
- **Fix accessibility issues** — ARIA labels, keyboard navigation, screen reader support
- **Improve mobile layout** — test on real devices and fix what breaks
- **Write documentation** — help other developers understand the codebase
- **Report bugs** — open an issue with steps to reproduce
- **Suggest features** — open an issue tagged `enhancement`

## Adding a New City

1. Open `index.html` and find the `CITY_DATA` object
2. Add a new key using the city's lowercase short name (e.g. `phoenix`)
3. Follow the exact same data shape as the existing cities:

```javascript
CITY_DATA.phoenix = {
  budget: {
    total: '$X.XXB',
    change: '↑/↓ X.X% from FY2025',
    items: [
      { name: 'Department Name', pct: 30, amount: '$XXXm', color: '#hexcode' },
      // ...
    ]
  },
  votes: [
    {
      title: 'Vote Title',
      status: 'live' | 'pend' | 'pass' | 'fail',
      impact: 'high' | 'medium' | 'low',
      yea: 7, nay: 4, total: 13,
      date: 'Jun 1, 2026',
      body: 'City Council',
      desc: 'Description of the vote and its implications.'
    },
    // ...
  ],
  meetings: [
    {
      month: 'JUN', day: '15',
      title: 'Meeting Name',
      location: 'Address',
      time: '6:00 PM',
      agenda: '5 items',
      today: false
    },
    // ...
  ],
  infra: [
    {
      icon: '🛣️',
      name: 'Infrastructure Name',
      status: 'critical' | 'warning' | 'ok',
      statusText: 'Status description',
      last: 'Updated Xh ago'
    },
    // ...
  ],
  stats: { votes: 20, meetings: 5, alerts: 2 }
};
```

4. Add the city to the `<select>` dropdown in the HTML:
```html
<option value="phoenix">Phoenix, AZ</option>
```

5. Data sources: use your city's open data portal (listed in `docs/API_SOURCES.md`). All data must be from official public sources only.

## Pull Request Process

1. Fork the repository
2. Create a branch: `git checkout -b feature/add-phoenix-data`
3. Make your changes
4. Test by opening `index.html` directly in your browser
5. Commit with a clear message: `git commit -m "feat: add Phoenix, AZ city data"`
6. Push and open a Pull Request
7. Fill in the PR template — describe what you changed and why

## Code Style

- 2-space indentation
- Descriptive variable names (`currentCity`, not `cc`)
- Comment anything non-obvious
- Keep functions small and single-purpose
- No external dependencies without discussion first

## Reporting Bugs

Open an issue with:
- Browser and OS
- Steps to reproduce
- What you expected vs. what happened
- Screenshot if applicable

## Code of Conduct

Be kind. This is a civic project. Everyone is welcome regardless of political views, background, or experience level.
