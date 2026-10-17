---
title: 'Instructor Notes'
---

## Overall approach

- The module follows one thread: find existing data, judge it, and fill the gaps with data you create
  (geocoded points or field data). The grocery access example (Lafayette and West Lafayette) runs through
  the Census and field episodes, and the Case Studies module finishes it with the QField demonstration and
  the QGIS network analysis (moved there in October 2026).
- **Census API keys** are the most common delay. Ask learners to request and activate a key before the
  session (see Setup); activation requires clicking a link in an email.
- All lesson data is read from the web: the notebooks read Census files, the Census Geocoder and
  OpenStreetMap directly, and `museums.txt` from this repository's `data/` folder. Imagery episodes do involve
  downloads, because finding and downloading imagery is the skill being taught.
- Suggested timing for a full day: Introduction 25 min; Repositories 35 min; Census 65 min (including
  notebook 1a or 1b); Geocoding 50 min (including notebook 2a); Imagery 50 min; Field data 40 min.
  Notebooks 1c, 2b and 2c work well as take-home practice.

## Episode by episode

### Introduction to Data Collection

- The "existing data or new data?" challenge works well as a pair discussion. Ask learners to bring a
  question from their own research.

### Finding Data in Repositories

- Purdue is a member of the Big Ten Academic Alliance, so the BTAA Geoportal search for "Tippecanoe" gives
  local results.
- Loading Natural Earth by URL in QGIS is a good first QGIS task.

### Data from the U.S. Census Bureau

- Have everyone open one API address in a browser before running Python; seeing the raw JSON makes the
  notebooks easier to follow.
- The margin of error figure is a good discussion starter: why are small counties less certain? Why is
  LaGrange County so different?
- Tract 104 (Purdue's west campus) returns `-666666666` for median household income and has no households,
  because almost everyone there lives in residence halls. Learners from Purdue usually recognize it.

### Geocoding and Adding Spatial Context

- The Census Geocoder is free and needs no key, but only covers U.S. addresses in its database.
  Campus addresses (for example "610 Purdue Mall") return no match; the notebooks use
  101 N Grant St (Purdue Memorial Union) instead.
- Two museums fail: the National Gallery (no street number; fixable as an intersection) and the
  Philadelphia Museum of Art (not in the Census database). Use them to discuss address quality.
- Nominatim (used in notebooks 2b and 2c) allows one request per second. In a room of 30 people sharing
  one network, requests may be throttled; ask learners to wait and rerun.
- Raise privacy: geocoding personal addresses creates sensitive location data.
- The OpenStreetMap part prepares learners for the Data Analysis module's Network Analysis episode, which
  uses the same OSM tags.

### Acquiring Imagery

- EarthExplorer and the Copernicus Browser both need accounts; ask learners to register in advance if you
  plan a live download.
- Satellite downloads are large. In a classroom, demonstrate the search and download steps, and let
  learners download a small product or a single band.

### Collecting Data in the Field

- Use the "Spot the problems" table to start a discussion about schemas before showing QField.
- If you have IRB-approved projects in your department, mention how they handled consent and location
  privacy.

## Common problems

| Symptom | Likely cause | Fix |
|---|---|---|
| Census API shows "Missing Key" | No key, or it was not pasted | Add `&key=` and the key to the address, or paste it in the notebook |
| Census API shows "Invalid Key" | Key not activated, or mistyped | Click the activation link in the email; copy the key again |
| `error: unknown variable` | Variable code misspelled, or wrong dataset path | Profile variables (DP) need `/profile` in the dataset path; check case |
| A join gives no matches | GEOID stored as a number, or different years | Keep GEOIDs as text; use boundaries and data from compatible years |
| A web layer loads but nothing appears | Off screen or under another layer | Right-click > **Zoom to Layer**; reorder layers |
| Census Geocoder returns `(None, None)` | Address not in the Census database (campus addresses such as "610 Purdue Mall") | Use a building's street address, or Nominatim |
| Geocoder or OSM timeout | Free server busy or rate limited | Wait a minute and rerun |
| Map shows "403 Access blocked" or "API key required" behind the points | OpenStreetMap and CARTO tiles do not work inside Colab | Add `tiles="Esri.WorldGrayCanvas"` to `.explore()` |
