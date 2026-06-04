# 🌐 City Open Data API Sources

All APIs listed here are free, public, and require no authentication for basic use.

## United States — City APIs

| City | Data Portal | API Type | Key Datasets |
|---|---|---|---|
| Boston, MA | data.boston.gov | Socrata | Council votes, budget, 311 reports |
| New York, NY | data.cityofnewyork.us | NYC Open Data | Council votes, capital budget, infrastructure |
| Chicago, IL | data.cityofchicago.org | Socrata | Council minutes, budget, service requests |
| Los Angeles, CA | data.lacity.org | Socrata | Council actions, budget documents |
| Seattle, WA | data.seattle.gov | Socrata | Council bills, capital projects |
| Houston, TX | data.houstontx.gov | ArcGIS | Council agendas, infrastructure |

## Federal APIs

| Source | URL | What It Provides |
|---|---|---|
| Congress.gov | api.congress.gov | Federal legislation, votes |
| USASpending.gov | api.usaspending.gov | Federal budget data |
| Data.gov | api.data.gov | Gateway to all federal datasets |

## Socrata API Pattern (used by most US cities)

```javascript
// Example: Get Boston council votes
const BOSTON_VOTES_API = 'https://data.boston.gov/api/3/action/datastore_search';

async function fetchBostonVotes() {
  const res = await fetch(`${BOSTON_VOTES_API}?resource_id=DATASET_ID&limit=10`);
  const data = await res.json();
  return data.result.records;
}
```

Replace `DATASET_ID` with the specific dataset ID from the city portal.

## How to Find the Right Dataset

1. Go to the city's data portal (e.g., data.boston.gov)
2. Search for "council votes" or "city council" or "budget"
3. Click a dataset → look for the "API" button or "Export" → "SODA API"
4. The dataset ID is in the URL: `data.boston.gov/resource/DATASET-ID.json`

## Rate Limits

Most Socrata APIs allow:
- **Anonymous:** 1,000 requests/hour
- **Registered (free):** 10,000 requests/hour

Register at each city's portal for a free app token to increase limits.

## Phase 2 Integration Plan

```javascript
// Future backend pattern (Node.js)
const CITY_APIS = {
  boston: {
    votes: 'https://data.boston.gov/resource/VOTES-ID.json',
    budget: 'https://data.boston.gov/resource/BUDGET-ID.json',
    meetings: 'https://data.boston.gov/resource/MEETINGS-ID.json',
  },
  nyc: {
    votes: 'https://data.cityofnewyork.us/resource/VOTES-ID.json',
    // ...
  }
};

async function fetchCityData(city, type) {
  const url = CITY_APIS[city][type];
  const res = await fetch(url, {
    headers: { 'X-App-Token': process.env.SOCRATA_TOKEN }
  });
  return res.json();
}
```
