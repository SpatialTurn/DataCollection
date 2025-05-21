---
title: "Geocoding"
teaching: 100
exercises: 5
---

:::::::::::::::::::::::::::::::::::::: questions 

- What are the various geocoding services that can be used?
- What are some limitations of the geocoding API?
- What are some categories of places that can be geocoded using the Open Street Map (OSM) API?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Learn how to use the Census geocoding API
- Learn how to use the Nominatim and Overpass APIs to access Open Street Map (OSM) data

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

The geocoding API is a service that converts street addresses into geographic coordinates. This can be done either way, which is converting geographic coordinates back to street addresses.
Features of geocoding APIs include:

1. Geocoding – addresses to geographic coordinates.
2. Reverse geocoding - geographic coordinates to address.
3. Region Biasing – constrain results to specific region, county, or postal code.
4. Place IDs – place ID to address and vice versa.

There are several practical applications of geocoding such as:

1. Location Based Services: Delivery Companies like uber, doordash convert user addresses into GPS
coordinates for efficient dispatching.
2. Mapping and GIS: Real estate platforms use geocode to display properties of interest on maps.
3. Emergency Services: Police, fire, and medical services use geocoding for precise identification
and to reduce response times by finding the fastest route.

Geocoding APIs also have certain limitations that need to be taken into account when using them. They are designed to convert predefined, static addresses and can result in an error if the 
address is incorrect. Several APIs may also impose daily usage limits for free access. Finally, geographic data involving geocoding needs to be constantly updated to avoid inaccuracies over time.

### Open Street Map


::::::::::::::::::::::::::::::::::::: keypoints 

- Geocoding APIs can be used to identify locations of specific categories such as grocery stores or restaurants

::::::::::::::::::::::::::::::::::::::::::::::::

## Hands-on Exercises

| Lesson | Overview                                                                                                                                                         | 
| ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| [Beginner](https://jupyter.iguide.illinois.edu/hub/user-redirect/git-pull?repo=https%3A%2F%2Fgithub.com%2FSpatialTurn%2FDataCollection-Notebooks&urlpath=lab%2Ftree%2FDataCollection-Notebooks%2FCensus%2FBeginner.ipynb+&branch=main)       | Learn how to query and visualize locations of points of interest (e.g., museums) or specific grocery stores. |

