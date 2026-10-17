---
title: "Acquiring Imagery: Scanned Maps and Satellite Data"
teaching: 30
exercises: 20
---

:::::::::::::::::::::::::::::::::::::: questions

- Where can I find historic maps and satellite imagery?
- What is the difference between a scanned map and a georeferenced image?
- How do I find and download declassified CORONA and Sentinel-2 imagery?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain spatial, spectral and temporal resolution
- Download a scanned historic map from a library collection
- Search for and download CORONA imagery from the CAST atlas and USGS EarthExplorer
- Search for and download Sentinel-2 imagery from the Copernicus Browser
- Open a downloaded image in QGIS

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

Paper maps, air photos and other images scanned at high resolution are often **georeferenced** (given real
coordinates) so they can sit under other layers in a GIS. Features in them, such as old buildings, roads or
field boundaries, can then be **digitized** into vector layers for analysis. Satellite images add a view of
the whole landscape, often repeated over time.

Many websites offer this kind of raster data for free:

- **Scanned historic maps** are usually plain images with no coordinates. You must georeference them
  before use. (See the section on georeferencing in the Data Management module.)
- **Modern satellite imagery** is already georeferenced and can be opened directly.
- Some sources are offered as **web services** that QGIS can display without downloading anything.

## Resolution: three kinds

| Kind | Question it answers | Example |
|---|---|---|
| **Spatial** resolution | How large is one pixel on the ground? | Sentinel-2: 10 m; Landsat color bands: 30 m; best CORONA: about 2 m (6 feet) |
| **Spectral** resolution | How many wavelength bands, and which? | A photograph has 3 (red, green, blue); Sentinel-2 has 13, including near-infrared |
| **Temporal** resolution | How often is the same place imaged? | Sentinel-2: about every 5 days; CORONA: occasional missions from 1960 to 1972 |

Higher spatial resolution shows smaller objects; more spectral bands help tell vegetation, water, soil and
buildings apart; frequent revisits let you track change.

## Sources

::::::::::::::::::::::::::::::::::::: spoiler

### Scanned historic maps

- [Perry-Castañeda Library Map Collection, University of Texas](https://maps.lib.utexas.edu/maps/): thousands of scanned maps, free to download
- [Old Maps Online](https://www.oldmapsonline.org/): a search engine across many map libraries, by place and date
- [National Library of Australia Trove](https://trove.nla.gov.au/): digitized maps, photographs and newspapers
- University library collections, such as those found through the [Big Ten Academic Alliance Geoportal](https://geo.btaa.org/)

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: spoiler

### Satellite imagery and elevation (most require a free account)

- [USGS EarthExplorer](https://earthexplorer.usgs.gov/): Landsat, declassified CORONA imagery, aerial photos and elevation data, including the SRTM 30 m elevation model
- [Copernicus Browser](https://browser.dataspace.copernicus.eu/): Sentinel-1, Sentinel-2 and other European satellite data
- [CORONA Atlas, University of Arkansas CAST](https://corona.cast.uark.edu/): CORONA images that have already been georeferenced
- [OpenTopography](https://www.opentopography.org/): elevation data, including SRTM and high-resolution lidar

::::::::::::::::::::::::::::::::::::::::::::::::

## Part 1: Download a historic map (beginner)

The University of Texas Perry-Castañeda Library (PCL) Map Collection hosts thousands of scanned paper maps,
organized by region and country.

1. Go to <https://maps.lib.utexas.edu/maps/>.
2. Open the **Historical Maps** section (or browse a region).
3. Browse until you find a useful map. Large series, such as military topographic maps, often have
   **index maps** that help you find the sheet for a particular area.
4. To save a map, right-click it and choose **Save Image As**, and save it in your project folder.
5. Note where the map came from: title, date, publisher and the page address. You will need these to
   cite it.

The saved file is an ordinary image. To use it with other layers, you must georeference it in QGIS
(**Layer > Georeferencer**) by matching points on the map to known coordinates.

## Part 2: Declassified CORONA imagery (intermediate)

During the Cold War, the United States ran a series of secret photo reconnaissance satellites. The
**CORONA** program (1960 to 1972) produced more than 860,000 black-and-white images, the first satellite
photographs of much of the Earth's surface. The images were declassified in 1995. The best of them, from the
KH-4B cameras (1967 to 1972), show objects as small as about 6 feet (2 m), and were taken as overlapping
stereo pairs on long, narrow film strips, each covering a strip of ground well over 100 km long.

CORONA images have become a valuable record of landscapes before modern urban growth, dam building and
industrial farming. Archaeologists, historians and geographers use them to find ancient sites, old field
systems, and settlements that have since disappeared.

### 2a. Georeferenced CORONA images from CAST

The **CORONA Atlas & Referencing System**, run by the University of Arkansas Center for Advanced Spatial
Technologies (CAST), offers CORONA images that have already been georeferenced, free of charge. It does not
cover the whole world, but it is a good first place to look.

1. Go to <https://corona.cast.uark.edu/> and click **Explore Atlas**.
2. Red outlines show the areas covered by CORONA missions in the atlas. Zoom in to one of them.
3. Use the slider at the bottom of the screen to compare CORONA with modern imagery side by side.
4. Expand the **Corona Imagery** layer with the **+** button to see the images being displayed. As you zoom
   in, the list gets shorter.
5. Turn images on and off to choose the one you want, then click the blue **down-arrow** next to it to
   download it. The files are large, so this can take a while.
6. Move the file from your Downloads folder to a project folder, for example `GIS/CORONA`.
7. In QGIS, go to **Layer > Add Layer > Add Raster Layer**, browse to the file and click **Add**.

### 2b. Raw CORONA scans from USGS EarthExplorer

USGS EarthExplorer holds the complete CORONA collection. Its images are not georeferenced, and the interface
takes some getting used to, but it covers far more of the world.

1. Log in, or create a free account, at <https://earthexplorer.usgs.gov/>.
2. In the map on the right, navigate to your area of interest. Either click to draw a polygon around it,
   or zoom to it and press **Use Map** in the **Search Criteria** tab.
3. In the **Data Sets** tab, expand **Declassified Data** and check **Declass 1 (1996)**.
4. In the **Additional Criteria** tab, set **Camera Resolution** to **Stereo High**. This keeps only the
   high-quality KH-4B images.
5. Optionally, set **Download Availability** to **Yes** to show only images that are already scanned. Unscanned
   frames can be scanned on request for a fee ($30 per frame at the time of writing).
6. Click **Results**.
7. Use the **Footprint** and **Image Overlay** icons to see where each image falls. The **Show Metadata and
   Browse** icon opens a preview, where you can check for clouds and clarity.
8. When you have chosen an image, click the **Download Options** icon and download it.

The download is a compressed archive (`.tgz`). Extract it (on Windows, with a tool such as 7-Zip, you may need
to extract twice: first the `.tgz`, then the `.tar` inside it). Because each film strip is so long, the image
is usually split into several `.tif` files ending in `a`, `b`, `c` and `d`. You will need to georeference them
before use.

## Part 3: Sentinel-2 multispectral imagery (intermediate)

**Sentinel-2** is part of the European Union's Copernicus Earth observation program. Since 2015 its satellites
(Sentinel-2A and 2B, joined by 2C, launched in 2024) have imaged all land surfaces about every 5 days in **13 spectral
bands**, at 10 m, 20 m and 60 m resolution. They are used to map land cover, crops, forests, water, urban
growth and disaster damage. The data is free.

Compared with the 30 m color bands of Landsat, Sentinel-2's 10 m bands show much more detail. Commercial
imagery (such as that in Google Earth) can be sharper still, but Sentinel-2's extra bands, especially
near-infrared, and its frequent revisits make it well suited to studying change over time.

### Find and preview imagery

1. Open the [Copernicus Browser](https://browser.dataspace.copernicus.eu/) and log in, or create a free
   account with the **Register** button.
2. Zoom the map to your area of interest.
3. The panel on the left has two tabs, **Visualize** and **Search**. In **Visualize**, choose a date (days
   with imagery are highlighted in the calendar) or click **Show latest date**, and limit cloud cover with
   the slider.
4. Choose a **layer**, such as **True color**, **False color** (vegetation shows red) or **NDVI** (a
   vegetation index), to view different band combinations.

### Search and download

1. Open the **Search** tab. Choose **Sentinel-2**, then **MSI**, then **L2A** (surface reflectance, already
   corrected for the atmosphere).
2. Set a **time range** and click **Search**. Each result is shown as an outline on the map; hovering over a
   result highlights it.
3. Click the **i** button on a result to see its details, including cloud cover.
4. To download, click the **download** icon next to the result. The file size is shown, and large products
   can take a while.

The download is a `.SAFE.zip` file. Unzip it; the individual bands are stored as `.jp2` image files inside the
`GRANULE/.../IMG_DATA` folders, and QGIS can open them with **Add Raster Layer**.

::::::::::::::::::::::::::::::::::::: callout

## Too big to download?

A single Sentinel-2 product is often 500 MB to 1 GB. Download only what you need: in the Copernicus Browser
you can also download a single band file, or export just the visible area as an image. The Data Analysis
module's NDVI notebooks show how to work with satellite bands in Python.

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Find a historic map

Using the PCL Map Collection or Old Maps Online, find a map of your hometown (or of Lafayette, Indiana)
made before 1950. Note its title, date, scale and publisher.

:::::::::::::::: solution

Answers will vary. A good record of a map includes its title, date, scale (for example 1:24,000), publisher,
the collection that holds it, and the web address. Old Maps Online lets you filter by date with a slider, and
shows each map's footprint on a modern map.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Download a CORONA image

Find a CORONA image of your area of interest, or of a famous landmark, in the CAST atlas. If the atlas does
not cover it, search EarthExplorer instead. Then open the image in QGIS.

:::::::::::::::: solution

The CAST atlas does not cover every area; if yours is missing, EarthExplorer holds the complete collection. An image from CAST lines up with
other layers immediately; an image from EarthExplorer appears without coordinates until you georeference it.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Which source?

Which imagery source would you use for each task?

1. Comparing farmland around a Middle Eastern village in 1968 and today
2. Mapping where crops were stressed by drought in Indiana last summer
3. Showing what downtown Lafayette looked like in 1900

:::::::::::::::: solution

1. **CORONA** for 1968 (try CAST first), and **Sentinel-2** or modern high-resolution imagery for today
2. **Sentinel-2**: frequent revisits and a near-infrared band for vegetation indices such as NDVI
3. A **scanned historic map**, such as a Sanborn fire insurance map, from a library collection

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Raster data includes scanned maps (which need georeferencing) and satellite images (already georeferenced)
- Consider spatial, spectral and temporal resolution when choosing imagery
- Declassified CORONA images (1960 to 1972) are a free historical record; CAST offers georeferenced copies
- Sentinel-2 provides free 10 m multispectral imagery about every 5 days, from the Copernicus Browser

::::::::::::::::::::::::::::::::::::::::::::::::
