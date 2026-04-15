---
title: 'Network Analysis for Grocery Access in QGIS'
teaching: 70
exercises: 35
---

:::::::::::::::::::::::::::::::::::::: questions 

- How can we move from collected grocery store points to a road-based accessibility analysis?
- How do shortest path and service area tools in QGIS answer different questions about grocery access?
- Why is network distance often better than straight-line distance for accesss studies?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Load and inspect grocery store points collected in QField
- Prepare a road network and confirm that all layers use an appropriate projected CRS.
- Calculate shortest paths from a selected origin to multiple grocery stores.
- Generate service areas from grocery stores to estimate walkable or drivable access.
- Interpret the outputs as part of a reproducible grocery access workflow.

::::::::::::::::::::::::::::::::::::::::::::::::

## Overview

In the previous lesson, learners simulated a collection of grocery store locations in the field using QField. In this lesson, learners will use those observation in QGIS to ask a new question:

**How accessible are grocery stores when movement is constrained by the road network?**

This episode shifts away from field **data collection** to **spatial analysis**. Instead of treating distance as a straight line, learners will use the street network to calculate routes. 

:::::::::::::::::::::::::::::::::::::::: prereq

## Before we begin

Learners should have downloaded:

- A point layer of grocery store locations (download link)
- a road layer for the study area (lesson link)
- study area boundary (lesson link)
- basic familiarity with QGIS (lesson link)

::::::::::::::::::::::::::::::::::::::::

## Lesson goals and scenario 

Imagine that a local class, community partner, or student groups wants to understand how easy/accessible it is to reach grocery stores from a particular residence hall, apartment area, or neighborhood. 

In this lesson, we will complete three related tasks:

1. prepare the grocery and road data
2. calculate routes from one origin to multiple stores
3. create service areas that estimate the streets reachable within chosen travel cost


## Data setup

You should have the following layers ready to open in QGIS:

- 'grocery_stores' - point layer "collected" in QField
- 'roads' - line layer representing the street network
- 'study_area' - boundary polygon for the lesson extent

::::::::::::::::::::::::::::::::::::::: callout

## Teaching note

For a workshop or classroom lesson/setting, use a small instructional sample instead of the full county data. A small area will run faster for your class, makes outputs and maps easier to read, and ensures your learners have a clear idea of the basics of network analysis

::::::::::::::::::::::::::::::::::::::::

## Step 1: Load and inspect the layers

1. Open QGIS.
2. Add the grocery store points, road netowrk, and study area boundary.
3. Open the attribute table for 'grocery_stores'.
4. confirm that the layer contains the fields we will be working with:
  - store name
  - store type
  - verification status
5. Visually inspect the grocery store points on top of the road network



Look and identify any obvious problems

- duplicate points
- points outside the study area
- stores placed in parking lots instead of near the entrance or parcel frontage
- roads that appear disconnected

:::::::::::::::::::::::::::::::::::::: challenge
## Quick inspection

What kinds of data quality problems would most directly affect a network analysis?

:::::::::::::::::::::::: solution
Problems that affect where a route starts or ends are especially important. For example:

- a grocery point placed far from the road network
- duplicate stores that inflate the number of destinations
- disconnected road segments that break routing
- a mismatched CRS that makes layers appear in the wrong place
:::::::::::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## Step 2: Reproject the data

Network analysis should be done in a projected CRS so that distances are measured in meaningful linear units like meters or feet.

For Lafayette / West Lafayette, choose an appropriate projected CRS for Indiana and your lesson goals such as NAD 1983/UTM 16N.

1. Right-click `grocery_stores`.
2. Choose **Export -> Save Features As...**
3. Save a projected copy named `grocery_stores_projected`.
4. Repeat for `roads` and `study_area` if needed.
5. Confirm that all projected layers align correctly.

:::::::::::::::::::::::::::::::::::::: caution
## CRS warning

Do not assume that layers are ready for analysis just because they draw in the same place on the map. Learners shoudl verify the CRS of each layer and make a projected copy when necessary.
:::::::::::::::::::::::::::::::::::::::::::::::

## Step 3: Clip to the study area

To reduce processing time and simplify the map, clip the road layer to the study area.

1. Open the **Processing Toolbox**.
2. Search for **Clip**.
3. Use:
   - **Input layer**: `roads_projected`
   - **Overlay layer**: `study_area_projected`
4. Save the output as `roads_clip`.

Optional: if the grocery layer includes stores outside the intended teaching extent, clip or filter that layer as well.

## Step 4: Create or choose an origin

You need a start point for route analysis.

- a manually created point representing a residence hall or apartment complex
- one point chosen from a learner-collected housing layer
- one point placed at a central campus location

To create an origin manually:

1. Create a new temporary point layer called `origin_point`.
2. Add one feature at the chosen starting location.
3. Save the layer if you want it to persist beyond the session.

:::::::::::::::::::::::::::::::::::::: discussion
## Why one origin first?

Why might it be better to start with a single origin before scaling up to many housing points or neighborhoods?
:::::::::::::::::::::::::::::::::::::::::::::::

A single origin keeps the first analysis legible. Learners can more easily inspect the routes, compare store access, and troubleshoot snapping or connectivity issues before moving to a more complex multi-origin workflow.

## Step 5: Run shortest path analysis to multiple stores

Now we will calculate routes from one origin to every grocery store.

In the Processing Toolbox, search for:

**Shortest path (point to layer)**

Set the parameters as follows:

- **Vector layer representing network**: `roads_clip`
- **Path type to calculate**: `Shortest`
- **Start point**: your chosen origin location
- **Vector layer with end points**: `grocery_stores_projected`
- **Shortest path**: save as `routes_to_grocery`
- **Non-routable features**: save as `non_routable_grocery` or create a temporary layer

Run the tool.

You should now have a line layer showing one route from the origin to each grocery store destination.

:::::::::::::::::::::::::::::::::::::: callout
## Why save the non-routable output? 

This layer is useful for teaching because it identifies destinations that could not be reached through the network. Those failures often reveal data quality problems, such as points too far from the road layer or disconnected network segments.
:::::::::::::::::::::::::::::::::::::::::::::::

## Step 6: Symbolize and inspect the routes

1. Style `routes_to_grocery` with a bold line color.
2. Style grocery stores with a distinct point symbol.
3. Style the origin point with a larger marker.
4. Zoom to the study area and inspect the output.


- Which stores appear easiest to reach?
- Are any routes unexpectedly long?
- Are any stores missing from the routed output?

If the output contains several nearly overlapping lines, filter to a subset of stores or select a smaller study area for demonstration.

## Step 7: Measure travel cost and identify the nearest options

1. Open the attribute table for `routes_to_grocery`.
2. Open the **Field Calculator**.
3. Create a field named `route_m` using `$length`.
4. Create another field named `route_km` using `$length / 1000` if desired.
5. Sort the attribute table by `route_m` in ascending order.

This lets learners identify which stores are nearest by network distance instead of by straight-line distance.

:::::::::::::::::::::::::::::::::::::: challenge
## Interpreting route results

A store appears close on the map, but its route distance is much longer than expected. Name two possible reasons.

:::::::::::::::::::::::: solution
Possible reasons include:

- the street network requires a detour because there is no direct connecting road
- the point is snapped to a road segment that is not the one learners expected
- barriers such as limited crossings or cul-de-sacs increase network travel distance
- the grocery point or origin point is placed slightly off the true access location
:::::::::::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::

## Step 8: Create service areas from grocery stores

Shortest routes answer the question, **how do I get from one place to a store?**

Service areas answer a different question, **how far along the network can I travel from each store within a given distance or time?**

In the Processing Toolbox, search for:

**Service area (from layer)**

Use these parameters:

- **Vector layer representing network**: `roads_clip`
- **Vector layer with start points**: `grocery_stores_projected`
- **Path type to calculate**: `Shortest`
- **Travel cost**: choose a value appropriate for your lesson, such as `800` meters for an approximate short walk or another value that matches your teaching goals
- save the output as `grocery_service_area`

Run the tool.

The resulting output shows the network segments reachable from each grocery store within the chosen cost threshold.


## Step 9: Interpret the service area

Service areas can support discussion questions such as:

- Which parts of the study area appear well served by the current store network?
- Which neighborhoods or campus zones appear less connected?
- How does the answer change if the travel cost is 400 m, 800 m, or 1600 m?

:::::::::::::::: instructor

At this stage, remind learners that the output is only as good as the network and assumptions behind it.

For example:

- a road centerline layer does not necessarily represent sidewalks
- a driving-oriented network may not be ideal for pedestrian access
- field-collected store points improve destination quality, but they do not fix a poor road dataset

:::::::::::::::: instructor

:::::::::::::::::::::::::::::::::::::: discussion
## Reflection

What kinds of real-world access are still missing from this analysis even after using a network instead of straight-line distance?
:::::::::::::::::::::::::::::::::::::::::::::::

Possible answers include sidewalk quality, crosswalks, traffic safety, store hours, prices, food quality, disability access, and whether the road network is truly walkable.

## Step 10: Save outputs for later episodes

Save the following layers into the lesson geopackage or project folder:

- `grocery_stores_projected`
- `roads_clip`
- `origin_point`
- `routes_to_grocery`
- `non_routable_grocery`
- `grocery_service_area`

:::::::::::::::: instructor

These outputs can be reused in later episodes on:

- accessibility comparison between neighborhoods
- joining service areas to census or block data
- map layout design
- reproducible analysis in the Processing Model Designer
- exporting results for a story map or final report
::::::::::::::::::
## Instructor notes

:::::::::::::::::::::::::::::::::::: instructor
### Suggested pacing

- Introduction and setup: 10 minutes
- Data inspection and projection: 15 minutes
- Shortest path analysis: 20 minutes
- Service area analysis: 15 minutes
- Discussion and interpretation: 10 minutes
- Challenge and troubleshooting time: 15 minutes

### Recommended teaching strategy

Keep the lesson focused on one clear idea: network distance differs from straight-line distance. Learners already collected grocery store data in the previous lesson, so the sequel should emphasize analytical payoff.

### Common learner problems

- layers are not projected consistently
- grocery points do not sit close enough to the road network
- road network is clipped too tightly and breaks valid routes
- learners confuse service areas with buffers
- outputs are saved as temporary layers and then lost

### Good extension ideas

- compare shortest versus fastest paths
- build a small housing-origin layer and use a many-to-one routing workflow
- compare service areas across different travel thresholds
- discuss whether a road network is an appropriate proxy for pedestrian access
:::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::: keypoints
- Grocery points collected in QField become much more analytically useful when paired with a road network.
- Network analysis answers access questions that straight-line distance cannot.
- Shortest path tools are useful for route comparison, while service area tools estimate reachable portions of the network.
- Projected data, clean destination points, and a connected road layer are essential for reliable outputs.
- Saving routable and non-routable results supports interpretation and troubleshooting.
:::::::::::::::::::::::::::::::::::::::::::::::


