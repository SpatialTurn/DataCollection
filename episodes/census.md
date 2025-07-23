---
title: "U.S. Census Bureau Data"
teaching: 100
exercises: 5
---

:::::::::::::::::::::::::::::::::::::: questions 

- What are the kinds of datasets available from the U.S. Census Bureau?
- How can you visualize and analyze these datasets for your region of interest?
- Where can you find additional information about a particular dataset?
- How do you combine spatial and tabular data from the Census Bureau?
- What are the variables in the ACS dataset?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Provide an overview of the data available from the U.S. Census Bureau
- Explain how to download and visualize spatial data from the Census Bureau
- Demonstrate how to query and analyze the spatial data
- Demonstrate how to perform complex spatial joins

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

There are three broad categories of datasets available from the U.S. Census Bureau:

1. Census TIGER/Line Shapefiles
2. Decennial Census of Population and Housing
3. American Community Survey (ACS)

### Census TIGER/Line Shapefiles

TIGER (Topologically Integrated Geographic Encoding and Referencing) system. It is the primary geospatial data provided by Census Bureau. 
TIGER/Line shapefiles are available from 2007 to present. Data before 2007 are available in ASCII format. 
It includes all legal boundaries and names of different geographic units in United States, including states, counties, places, zip codes, urban areas, census blocks, census block groups, and census tracts. 
These shapefiles include a standard geographic identifier (GEOID) for each record which links to the GEOID in the census data.
TIGER/Line Shapefiles use the American National Standards Institute (ANSI) codes to identify geographic entities. 
The ANSI include both the Federal Information Processing Series (FIPS) codes and the U.S. Geological Survey’s Geographic Names Information System (GNIS) codes. 
The fields in the shapefiles include these information. For example, “STATEFP” filed means state FIPS code, and “STATENS” field means state GNIS code. 
County level FIPS codes usually have five digits. The first two are the FIPS code of the state to which the county belongs and the rest three are county codes.

### Decennial Census of Population and Housing

It is conducted every ten years which counts every person living in the U.S. 
It provides general population characteristics such as age, sex, race, ethnicity, and household composition. 
It is a point-in-time data which sample every person with smallest margin of error.

Variables:

- Population data by sex, age, race, Hispanic origin and more. 
- Housing data by occupancy, vacancy status, and tenure at the highest geographic resolution (all levels).

### American Community Survey (ACS)

ACS is conducted every year by collecting information from a sample population. 
It includes topics not included in the decennial census such as education, employment, internet access, and transportation. 
ACS 1-year estimate is based on 12-month continuous survey and ACS 5-year estimate is based on a 60-month continuous survey. 
Compared to decennial census data, ACS survey information has relatively high margin of error (i.e. less reliable estimates).

Variables:
In addition to demographic and housing data, ACS also include:

1. Social characteristics
- school enrollment
- educational attainment
- marital status
- fertility
- grandparents caring for children
- veteran status
- disability status
- language spoken at home
2. Income and benefits
- food Stamps/Supplemental Nutrition Assistance Program (SNAP)
- health insurance coverage
- income
3. Employment
- employment location
- mode of travel to work
4. Many other variables
- ancestry
- citizenship status
- place of birth
- year of entry


::::::::::::::::::::::::::::::::::::: keypoints 

- Census data can be used for planning services for certain population groups
- It can be used for site selection for new businesses or service facilities
- Public policy analysis
- Spatial analysis of hazard impact, epidemiological models, etc.

::::::::::::::::::::::::::::::::::::::::::::::::

# Module Overview

| Lesson | Overview                                                                                                                                                         | 
| ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| [Beginner](https://hub.cyberfaces.org/hub/user-redirect/git-pull?repo=https%3A%2F%2Fgithub.com%2FSpatialTurn%2FDataCollection-Notebooks&urlpath=lab%2Ftree%2Fmodules%2FDataCollection-Notebooks%2FCensus%2FBeginner.ipynb+&branch=main)       | Learn how to visualize and analyze shapefiles and tabular data downloaded from the U.S. Census Bureau. |

