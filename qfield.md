---
title: 'QField Training: Mapping Grocery Stores to Identify Potential Food Deserts'
teaching: 35
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 


- What does a QField grocery-store mapping workflow look like from start to finish?
- What fields should we collect at groccery stores to support a later food-desert analysis?
- How do we keep field data consistent and QA-ready?


::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- See an end-to-end demonstration workflow using Lafayette grocery stores as an example.
- Understand the rationale behind point placement, attribute choices, and GPS accuracy rules.
- Learn what 'good' field data looks like before doing it yourself.

::::::::::::::::::::::::::::::::::::::::::::::::

## Scenario

Imagine you are on a community research team in **Lafayette-West Lafayette, Indiana**. Your goal is to understand where **grocery access may be limited**, so you can later map **potential food deserts** using demographic and network/travel-time analysisi.

Before you can analyze food access, you need a clean consistent dataset of **grocery store locations and basic access attributes**. This tutorial is a **walk-through demonstration** of how that dataset can be created by using **QField** in the field and **QGIS** on a computer, using **Lafayette grocery stores as examples**.

:::: callout

## This is a demo, not a lab

You do **not** need to download anything or click along. The goal is to understand the workflow and what "good data" looks like.

::::

## What will be demonstrated

In the demo, the mapper collects:

-**One point per grocery store**, placed at the **main public entrance**
- A standardized set of attributes
- A photo of storefront signage
- A short note documenting anything unusual.

The result is a dataset ready for later food-access/ food desert analysis

## Project setup

In a real project, the instructor prepares a QGIS project that includes:

- An offline basemap
- A study area boundary for Lafayette-West Lafayette
- An editable layer called **Grocery Stores**
- A prebuilt **data-entry form** with dropdowns (domains) to keep entries consistent

::::: callout

## Why preconfigure?

Field collection fails when every person invents their own fields and categories. A prebuilt form keeps the dataset clean and analyzable.
::::::


## Data schema shown in the demo (What gets collect and why)

The **Grocer Stores** layer uses a form like this:

- 'store_name' (text) - needed to deduplicate and verify
- 'store_type' (dropwdown) - lets you compare supermarkets vs convenience, etc.
- 'address' (text) - helps match to other datasets/verify location
- 'city' (dropdown) - supports filtering and reporting
- 'zip' (text) - supports nieghborhood-level summaries
- 'snap_accepted' (Yes/No/Unknown) - access for benefits users
- 'wic_accepted' (Yes/No/Unknown) - additonal access signal
- 'produce_available' (Yes/No/Unknown) - "healthy food" availability proxy
- 'hours_observed' (text) - can matter for access (night shifts, weekends)
- 'notes' (text) - preserves context without inventing new fields
- 'photo_1' (attatchment) evidence/verification for QA

::::::: callout

## Why dropdowns matter

If one person writes "EBT," another writes "SNAP," and onother writes "Yes," your later analysis becomes messy. Dropdowns prevent category drift.

::::::::::

## Part 1 - Opening the project and checking readiness

The mapper opens QField and performs a fast readiness check:

1. Confirm the basemap displays.
2. Confirm the study boundary loads.
3. Confirm **Grocery Stores** is visible and editable.

::: callout

## Why this check is shown

It's the most common failure pint: missing layers, broken paths, or non-editable files often discovered *after* arriving at the first location.

::::

## Part 2 - GPS rules

The mapper waits for GPS accuracy to stabilize and applies a rule:

- **Preferred:** record a point when accuracy is **< 10 meters**
- **If not possible:** record anyway and document the issue in 'notes'

:::: callout

## Why accuracy is a big deal for food access

A store point shifted 30-50 meters can change whether it falls inside a buffer/service area, especially near boundaries or along road networks

::::::

## Part 3 - Collecting a grocery store point

### Example A: A full-service supermarket

**Demo location:** "Example Supermarket" (Lafayette, IN)

**What the mapper does:**

1. Stands near the **main public entrance** (consistent placement rule)
2. Creates **one pint** for the store.
3. Fills the form:
  - 'store_name': "Example Supermarket"
  - 'store_type': Supermarket
  - 'snap_accepted': Yes (based on posted signage)
  - 'wic_accepted': Unknown (no clear sign visible)
  - 'produce available': Yes (visible produce section)
  - 'hours_observed': copied from door signage
4. Adds a storefront pot that captures:
  - store name signage
  - posted hours (if visible)
  
::: callout

## Why the "entrance" rule is demonstrated

Entrances are consistent, repeatable, and relevant for walking-time analysis. The centroid of a building is less meaningful for access.

:::::

### Example B: A small market / convenience-style grocery

**Demo location:** "Example Neighborhood Market"

**What changes in the form:**
- 'store_type' might be "Convenience" or "Small Market"
- 'produce_available' might be "Unknown" or "No" (depending on what's visible)
- The mapper is careful not to assume SNAP/WIC without evidence

:::: callout

## Why we use "Unknown"

"Unknown" is better than guessing. Guessing introduces systematic bias into the dataset.

:::::

## Part 4 - Handling common edge cases

### Edge case 1: Duplicate risk

If the mapper sees a nearby exisiting point with the same store name:
- They **edit the exisiting feature** instead of creating a new one.

**Why:** duplicates inflate stores counts and distort service coverage.

### Edge case 2: Poor GPS

If accuracy is high (worse than 10 m,) the mapper:
- records the point anyway
- writes a note like: "GPS ~22m; point approximated at main entrance"

**Why:** transparency beats false precision.

### Edge case 3: Store closed/renovation

The mapper can still record the location and note:
- "Closed during visit"/"Under renovation"
- and leave uncertain fields as unknown

**Why:** closure status can matter for real access

## Part 5 - Sync and quick QA in QGIS

Back on the computer, the mapper opens the project in QGIS and checks:

1. **Completeness**
  - Are required fields filled?
2. **Spatial sanity**
  - Do points fall inside the study area?
  - Any points in impossible locations?
3. **Duplicates**
  - Same name and very close geometry?
4. **Photo verification**
  - Can photos be opened and do they match the record
  
  
:::: callout

## Why QA is shown as part of collection

If you QA right away, you will remember what you saw. Waiting weeks turns fixable issues into permanent uncertainty.

:::::

## What "good output" lookes like

At the end of the demo, the dataset has:

- One record per store (no duplicates)
- Consistent categories (dropdown-controlled)
- Minimal guessing (Unknown used appropiately)
- Photos that support verification
- Notes that caputre exceptions without creating new categories 

This is the foundation you need before any foo desert mapping begins.


## Next module

Placeholderplaceholderplaceholderplaceholder












::::::::::::::::::::::::::::::::::::: keypoints 

- A clear scenarion and consistent schema makes field data analyzable
- Demonstrations should highlight *why* each step exists, not just which buttons to press.
- QA is part of collection, not a separate afterthought
::::::::::::::::::::::::::::::::::::::::::::::::

