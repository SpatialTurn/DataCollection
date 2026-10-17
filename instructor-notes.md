---
title: 'Instructor Notes'
---

## Overall approach

- The module follows one thread: find existing data, judge it, fill the gaps with field data, and use the
  result. The grocery access case (Lafayette and West Lafayette) ties the Census, QField and network analysis
  episodes together.
- **Census API keys** are the most common delay. Ask learners to request and activate a key before the
  session (see Setup); activation requires clicking a link in an email.
- All lesson data is read from the web: the notebooks read Census files directly, and QGIS loads the network
  analysis files from this repository's `data/` folder by URL. Imagery episodes do involve downloads, because
  finding and downloading imagery is the skill being taught.
- Suggested timing for a full day: Introduction 25 min; Repositories 35 min; Census 65 min (including
  notebook 1a or 1b); Imagery 50 min; Field data 40 min; QField demonstration 45 min; Network analysis 75 min.
  Notebook 1c works well as take-home practice.

## Episode by episode

### Introduction to Data Collection

- The "existing data or new data?" challenge works well as a pair discussion. Ask learners to bring a
  question from their own research.

### Finding Data in Repositories

- Purdue is a member of the Big Ten Academic Alliance, so the BTAA Geoportal search for "Tippecanoe" gives
  local results.
- Loading Natural Earth by URL in QGIS is a good first QGIS task, and it prepares learners for the network
  episode.

### Data from the U.S. Census Bureau

- Have everyone open one API address in a browser before running Python; seeing the raw JSON makes the
  notebooks easier to follow.
- The margin of error figure is a good discussion starter: why are small counties less certain? Why is
  LaGrange County so different?
- Tract 104 (Purdue's west campus) returns `-666666666` for median household income and has no households,
  because almost everyone there lives in residence halls. Learners from Purdue usually recognize it.

### Acquiring Imagery

- EarthExplorer and the Copernicus Browser both need accounts; ask learners to register in advance if you
  plan a live download.
- Satellite downloads are large. In a classroom, demonstrate the search and download steps, and let
  learners download a small product or a single band.

### Collecting Data in the Field

- Use the "Spot the problems" table to start a discussion about schemas before showing QField.
- If you have IRB-approved projects in your department, mention how they handled consent and location
  privacy.

### QField Demonstration

- This is a demonstration. If time and devices allow, a short walk to map a few campus locations with a
  prepared QField project makes it memorable.

### Network Analysis for Grocery Access

- The most important setting is the **project CRS** (EPSG:26916). If learners see costs around 0.04, their
  project is still in EPSG:4326.
- Do **not** clip the roads to the city limits; the episode shows why. All 17 supermarkets are reachable with
  the provided road layer.
- With the full layer, routes from the Purdue Memorial Union to the 17 supermarkets average about 5.7 km by
  road against 5.0 km in a straight line. About 11% of city street length is within 800 m of a supermarket
  along the network, and about 40% within 1,600 m.
- The grocery store data comes from OpenStreetMap (October 2026) and is not field verified; say so when
  presenting results.

## Common problems

| Symptom | Likely cause | Fix |
|---|---|---|
| Census API shows "Missing Key" | No key, or it was not pasted | Add `&key=` and the key to the address, or paste it in the notebook |
| Census API shows "Invalid Key" | Key not activated, or mistyped | Click the activation link in the email; copy the key again |
| `error: unknown variable` | Variable code misspelled, or wrong dataset path | Profile variables (DP) need `/profile` in the dataset path; check case |
| A join gives no matches | GEOID stored as a number, or different years | Keep GEOIDs as text; use boundaries and data from compatible years |
| Network costs are tiny | Project CRS is EPSG:4326 | Set the project CRS to EPSG:26916 |
| Some routes have a NULL cost | Network broken, often by clipping | Use the full road layer |
| A web layer loads but nothing appears | Off screen or under another layer | Right-click > **Zoom to Layer**; reorder layers |
