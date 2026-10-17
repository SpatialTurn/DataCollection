---
title: "QField Demonstration: Mapping Grocery Stores"
teaching: 35
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions

- What does a QField data collection project look like from start to finish?
- What should we record at each grocery store to support a later food access analysis?
- How do we keep field data consistent and ready for quality checks?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Follow an end-to-end field workflow, using grocery stores in Lafayette and West Lafayette as the example
- Explain the reasons behind point placement, attribute choices and GPS accuracy rules
- Recognize what good field data looks like before collecting it yourself

::::::::::::::::::::::::::::::::::::::::::::::::

## Scenario

Imagine you are on a community research team in **Lafayette and West Lafayette, Indiana**. Your goal is to
understand where **access to groceries may be limited**, so that you can later map potential **food deserts**
using demographic data and travel distances along the road network.

Before you can analyze food access, you need a clean, consistent dataset of **grocery store locations and
basic access information**. Public sources help: OpenStreetMap, for example, lists more than 60 food stores
in the two cities. But they cannot tell you whether a store sells fresh produce or accepts SNAP benefits, and
some entries may be out of date. This episode **demonstrates** how a team would check and complete that
dataset with **QField** in the field and **QGIS** on a computer.

::::::::::::::::::::::::::::::::::::: callout

## This is a demonstration

You do not need to install anything or follow along on a phone. The goal is to understand the workflow and
what good field data looks like. If you want to try QField yourself, see the box at the end of this episode.

::::::::::::::::::::::::::::::::::::::::::::::::

## What the mapper collects

- **One point per grocery store**, placed at the **main public entrance**
- A standard set of attributes, chosen from dropdown lists
- A photo of the storefront sign
- A short note about anything unusual

The result is a dataset ready for a food access analysis, such as the network analysis in the next episode.

## Project setup

Before anyone goes out, the project leader prepares a project in QGIS that includes:

- An offline basemap, so the map works without mobile data
- The study area boundary for Lafayette and West Lafayette
- An editable point layer called **Grocery Stores**, starting from the stores already listed in
  OpenStreetMap
- A prebuilt **data entry form** with dropdown lists

The project is then packaged for QField with the **QFieldSync** plugin in QGIS, and copied to each phone,
either by cable or through **QFieldCloud**, QField's optional online syncing service.

::::::::::::::::::::::::::::::::::::: callout

## Why prepare the form in advance?

Field collection fails when every person invents their own fields and categories. A prepared form keeps the
dataset clean and ready to analyze.

::::::::::::::::::::::::::::::::::::::::::::::::

## The data schema (what gets collected, and why)

| Field | Type | Why |
|---|---|---|
| `store_name` | Text | Needed to identify stores and find duplicates |
| `store_type` | Dropdown | Compare supermarkets with convenience stores and other types |
| `address` | Text | Match the store to other datasets and verify its location |
| `city` | Dropdown | Filter and report by city |
| `zip` | Text | Summarize by ZIP code area |
| `snap_accepted` | Yes / No / Unknown | Access for people using SNAP benefits |
| `wic_accepted` | Yes / No / Unknown | An additional access signal |
| `produce_available` | Yes / No / Unknown | A simple measure of healthy food availability |
| `hours_observed` | Text | Hours matter for access, for example for night-shift workers |
| `verification` | Dropdown | Whether the record was checked in the field, and when |
| `notes` | Text | Keeps context without inventing new fields |
| `photo_1` | Attachment | Evidence for later checking |

::::::::::::::::::::::::::::::::::::: callout

## Why dropdowns matter

If one person writes "EBT", another writes "SNAP" and another writes "Yes", the later analysis becomes messy.
Dropdowns prevent this kind of category drift.

::::::::::::::::::::::::::::::::::::::::::::::::

## Part 1: Opening the project and checking it is ready

The mapper opens QField and runs a quick check:

1. The basemap displays.
2. The study area boundary loads.
3. The **Grocery Stores** layer is visible and can be edited.

This is the most common point of failure: missing layers, broken file paths or read-only layers are often
discovered only after arriving at the first store.

## Part 2: The GPS rule

The mapper waits for the GPS accuracy to settle, then applies a rule:

- **Preferred:** record a point when the accuracy is **better than 10 meters**
- **If that is not possible:** record it anyway and describe the problem in `notes`

A store point that is 30 to 50 meters off can change whether it falls inside a service area or which road it
is assigned to, especially near boundaries.

## Part 3: Recording a store

### Example A: a full-service supermarket

**What the mapper does:**

1. Stands at the **main public entrance** (the placement rule).
2. If the store is already on the map, opens that point instead of creating a new one. Otherwise, creates
   **one point** for the store.
3. Fills in the form:
   - `store_name`: as shown on the sign
   - `store_type`: Supermarket
   - `snap_accepted`: Yes (based on a posted sign)
   - `wic_accepted`: Unknown (no sign visible)
   - `produce_available`: Yes (produce section visible)
   - `hours_observed`: copied from the door
   - `verification`: Field verified, with the date
4. Takes a storefront photo showing the store's name and, if visible, its posted hours.

Why the entrance? Entrances are consistent and repeatable, and they are what matters for walking distance. The
center of a large building, or its parking lot, is much less meaningful for access.

### Example B: a small market or convenience store

**What changes in the form:**

- `store_type` might be Convenience or Small market
- `produce_available` might be Unknown or No, depending on what is visible
- The mapper does not assume SNAP or WIC without evidence

"Unknown" is better than a guess. Guessing introduces systematic bias into the dataset.

## Part 4: Common problems

| Situation | What the mapper does | Why |
|---|---|---|
| A point with the same store name is already nearby | Edits the existing point instead of adding a new one | Duplicates inflate store counts and distort access |
| GPS accuracy is worse than 10 m | Records the point anyway and notes it, for example "GPS about 22 m; placed at main entrance" | Being open about error is better than false precision |
| The store is closed or being renovated | Records it, notes "Closed during visit", and leaves uncertain fields as Unknown | Whether a store is open affects real access |
| The store is not in the starting data | Adds a new point | Public datasets miss stores, especially small ones |
| A store on the map no longer exists | Sets `verification` to "Not found" rather than deleting it | Keeps a record of what was checked |

## Part 5: Sync and check in QGIS

Back at the computer, the mapper syncs the project and opens it in QGIS to check:

1. **Completeness**: are the required fields filled in?
2. **Location**: do points fall inside the study area, and none in impossible places?
3. **Duplicates**: any points with the same name very close together?
4. **Photos**: do they open, and do they match their records?

Checking right away means you still remember what you saw. Waiting weeks turns fixable problems into
permanent uncertainty.

## What good output looks like

At the end of the demonstration, the dataset has:

- One record per store, with no duplicates
- Consistent categories, controlled by dropdowns
- "Unknown" used where appropriate, instead of guesses
- Photos that support checking
- Notes that capture exceptions without creating new categories
- A record of which stores were verified, and when

This is the foundation you need before any food desert mapping begins.

::::::::::::::::::::::::::::::::::::: challenge

## Look at the starting data

The grocery stores used in the next episode came from OpenStreetMap. Open the file in QGIS
(**Layer > Add Layer > Add Vector Layer**, **Protocol: HTTP(S), cloud, etc.**) with this address:

`https://raw.githubusercontent.com/SpatialTurn/DataCollection/main/data/grocery_stores.geojson`

Open its attribute table. Which fields from the schema above are present, and which would a field visit
need to add?

:::::::::::::::: solution

The file has `store_name`, `store_type`, `address`, `city`, `osm_id`, `source` and `verification`. Every
record says "Not field verified", and some have no address or no name. A field visit would add
`snap_accepted`, `wic_accepted`, `produce_available`, `hours_observed`, `notes` and photos, fill in missing
names and addresses, and update `verification`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: callout

## Want to try QField yourself?

1. Install QField on your phone from <https://qfield.org/> (Android, iOS) or on a computer.
2. In QGIS, install the **QFieldSync** plugin (**Plugins > Manage and Install Plugins**).
3. Build a small project with one editable point layer, set dropdowns in **Layer Properties > Attributes
   Form** (choose the **Value Map** widget), and package it with QFieldSync.
4. Copy the package to your phone, or use QFieldCloud, and map a few places around you.

The [QField documentation](https://docs.qfield.org/get-started/) walks through each step.

::::::::::::::::::::::::::::::::::::::::::::::::

## Next

In the next episode, we use grocery store points like these, together with the road network, to measure how
far people must travel to reach a supermarket.

::::::::::::::::::::::::::::::::::::: keypoints

- A clear scenario and a consistent schema make field data analyzable
- Prepare the project and form in QGIS before going out, and package it with QFieldSync
- Place points by a fixed rule, record GPS accuracy, and use "Unknown" instead of guessing
- Check the data in QGIS as soon as possible after collection

::::::::::::::::::::::::::::::::::::::::::::::::
