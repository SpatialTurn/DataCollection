---
site: sandpaper::sandpaper_site
---

One of the main challenges in using digital data in the social sciences is knowing how to **collect** it:
where to find existing data, how to judge whether it can be trusted, and how to gather original data when
nothing suitable exists. This module covers both sides, from data repositories and the U.S. Census Bureau to
satellite imagery and field data collection with a phone.

| Episode | What you will learn | Tools |
|---|---|---|
| Introduction to Data Collection | When to use existing data or collect your own; vector and raster data; judging data quality; FAIR data | Concepts |
| Finding Data in Repositories | Where to find free vector data, how to read metadata, and how to load data from the web | Web browser, QGIS |
| Data from the U.S. Census Bureau | Census geography, the Decennial Census and the ACS, margins of error, and the Census API | Web browser, Python notebooks |
| Acquiring Imagery | Scanned historic maps, declassified CORONA imagery and Sentinel-2 satellite data | Web browser, QGIS |
| Collecting Data in the Field | Methods and apps, designing a schema, GPS accuracy, ethics and quality checks | Concepts |
| QField Demonstration | A complete field workflow for mapping grocery stores | QField, QGIS |
| Network Analysis for Grocery Access | Shortest paths and service areas along the road network | QGIS |

The Census, QField and network analysis episodes share one example: **access to grocery stores in
Lafayette and West Lafayette, Indiana**.

::::::::::::::::::::::::::::::::::::::::::: prereq

## Prerequisites

- A Google account, to open the notebooks in Google Colab
- A free Census API key (see Setup below)
- QGIS installed on your computer (see Setup below)
- For the notebooks: basic Python, such as running cells and working with a `pandas` DataFrame
- No prior GIS experience is needed

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Find, evaluate and cite existing geospatial datasets
- Download census boundaries and statistics with the Census API, and judge their reliability
- Find and download historic maps and satellite imagery
- Design a field data collection workflow with consistent, well-documented data
- Use collected data in a network analysis of access

::::::::::::::::::::::::::::::::::::::::::::::::

This module is part of [Enabling the Geospatial Turn in the Social Sciences](https://spatialturn.github.io/),
a set of training modules developed at Purdue University with support from the National Science Foundation.
