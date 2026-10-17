---
title: "Finding Data in Repositories"
teaching: 20
exercises: 15
---

:::::::::::::::::::::::::::::::::::::: questions

- Where can I find free vector data for my project?
- How do I judge whether a downloaded dataset is trustworthy?
- Can QGIS read data straight from the web?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Name several types of geospatial data repositories and what each is good for
- Search a geoportal and read a dataset's metadata
- Load a vector dataset into QGIS directly from a web address

::::::::::::::::::::::::::::::::::::::::::::::::

## Pre-existing vector data

Vector data for natural features, political boundaries, transportation networks and many other topics
already exists somewhere on the web, so you rarely have to create it from scratch. Many datasets are free
on government, university and open-source websites; some specialized datasets are sold. Quality varies
widely with the methods used to make them, so explore each dataset and its metadata before you rely on it.

## Kinds of repositories

| Kind | What you find there | Examples |
|---|---|---|
| **National statistical agencies** | Official boundaries and statistics | U.S. Census Bureau (next episode) |
| **State and local open data portals** | Parcels, roads, zoning, schools, local boundaries | IndianaMap, city and county GIS portals |
| **University geoportals** | Research datasets and scanned maps collected by libraries | Big Ten Academic Alliance Geoportal, GeoData@Tufts |
| **Open data hubs** | Datasets published by many organizations in one search | Esri ArcGIS Hub |
| **Global open datasets** | Consistent data for the whole world | Natural Earth, OpenStreetMap, HydroSHEDS |
| **Thematic repositories** | Data on one subject, often linked to surveys | DHS Program Spatial Data Repository |

## A starting list

Explore these sources. Bookmark the ones that seem most useful for your teaching or research. Data
sources specific to your area are usually on your state or local government's website.

| Source | What it offers |
|---|---|
| [Big Ten Academic Alliance Geoportal](https://geo.btaa.org/) | Search across the GIS data and scanned maps held by Big Ten universities, including Purdue |
| [GeoData@Tufts](https://geodata.tufts.edu/) | Search, preview and download geospatial data from several university repositories |
| [IndianaMap](https://www.indianamap.org/) | Indiana's statewide GIS data: boundaries, roads, imagery, geology, infrastructure and more |
| [Esri ArcGIS Hub](https://hub.arcgis.com/search) | Open datasets published by governments and organizations that use Esri software |
| [Natural Earth](https://www.naturalearthdata.com/) | Free country, state, coastline and city layers for the whole world, at three map scales |
| [Geofabrik OpenStreetMap downloads](https://download.geofabrik.de/) | OpenStreetMap data (roads, buildings, points of interest) cut into regions |
| [HydroSHEDS](https://www.hydrosheds.org/) | Global rivers, lakes and watershed boundaries |
| [DHS Spatial Data Repository](https://spatialdata.dhsprogram.com/home/) | Boundaries and survey indicators from the Demographic and Health Surveys in more than 90 countries |

::::::::::::::::::::::::::::::::::::: callout

## Read the license

"Free to download" does not always mean "free to reuse". U.S. federal data such as Census files is public
domain. OpenStreetMap data is free under the Open Database License, which requires you to credit
"OpenStreetMap contributors". Some university and commercial data may only be used by members of an
institution. The license is usually on the dataset's metadata page.

::::::::::::::::::::::::::::::::::::::::::::::::

## Reading metadata

Every good repository shows a **metadata** page for each dataset. When you open one, look for:

- **Title, author or publisher**, and a **date** (of the data, not just of the upload)
- An **abstract** or description of what is included
- The **spatial extent** (where it covers) and **scale** or **resolution**
- The **coordinate reference system**
- The **attributes** (columns) and what they mean
- **Lineage**: how the data was created and processed
- The **license** or use constraints

## Loading data straight from the web

You do not always have to download a file before using it. QGIS can open a file directly from its web
address. Let us load the Natural Earth countries layer this way.

1. In QGIS, go to **Layer > Add Layer > Add Vector Layer**.
2. For **Source Type**, choose **Protocol: HTTP(S), cloud, etc.**
3. Leave **Type** as **HTTP/HTTPS/FTP** and paste this address into **URI**:
   `https://raw.githubusercontent.com/nvkelso/natural-earth-vector/master/geojson/ne_110m_admin_0_countries.geojson`
4. Click **Add**, then **Close**.

The world's countries appear. Right-click the layer and choose **Open Attribute Table** to see its
attributes, such as `NAME`, `CONTINENT` and `POP_EST`. The rest of this module uses this method to load
the lesson data, so you never have to manage downloaded files.

::::::::::::::::::::::::::::::::::::: challenge

## Explore a geoportal

1. Open the [Big Ten Academic Alliance Geoportal](https://geo.btaa.org/) and search for **Tippecanoe**.
2. Pick one result and open its record.
3. Answer: Who published it? What year does the data describe? What format can you download? Is there a
   license or use statement?

:::::::::::::::: solution

Results change over time, but you will typically find county layers from IndianaMap and the Census Bureau,
scanned historical maps from university libraries, and aerial imagery. A good record lists the publisher,
the date of the data, the formats available (for example shapefile, GeoJSON or a web service) and a rights
statement. If a record is missing several of these, treat the data with caution.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Which source would you use?

Which source from the list above would you try first for each of these?

1. River networks for a study of flooding in Bangladesh
2. Country outlines for a world map in a slide presentation
3. Indiana school district boundaries
4. All cafes in Chicago

:::::::::::::::: solution

1. **HydroSHEDS**, which covers the whole world consistently
2. **Natural Earth**, designed for small-scale maps like this
3. **IndianaMap**, or the Census Bureau's school district boundaries
4. **OpenStreetMap** through Geofabrik (search for `amenity=cafe`). Coverage depends on local volunteers,
   so check it against another source

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Search existing repositories before creating data from scratch
- Different repositories serve different needs: official statistics, local data, research collections, global layers
- Read the metadata and the license before you use a dataset
- QGIS can open data directly from a web address, so you do not need to download files

::::::::::::::::::::::::::::::::::::::::::::::::
