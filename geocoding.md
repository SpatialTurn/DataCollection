---
title: "Geocoding and Adding Spatial Context"
teaching: 50
exercises: 20
---

:::::::::::::::::::::::::::::::::::::: questions

- What is geocoding, and why do social scientists need it?
- How do we turn a list of addresses into points on a map?
- How can OpenStreetMap add context such as stores, schools or parks?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Geocode U.S. addresses with the free U.S. Census Geocoder
- Check match rates and find addresses that failed
- Turn coordinates into a GeoDataFrame and map it
- Download features from OpenStreetMap by tag
- Handle rate limits and ambiguous place names when geocoding many places

::::::::::::::::::::::::::::::::::::::::::::::::

## Why geocoding matters

Most social science data has a location written as text: a survey respondent's address, a list of
clinics, a business directory. **Geocoding** turns that text into latitude and longitude so the data
can be mapped and analyzed spatially.

Geocoding is a form of data collection: it creates new spatial data from records that already exist,
without a field visit. It sits between the two paths in the
[Introduction](introduction.md): the records are existing data, but the points are yours to create and
check.

| Input (text) | Output (coordinates) |
|---|---|
| `1600 Pennsylvania Ave NW, Washington, DC 20500` | 38.8977, -77.0365 |

Once your data are points, you can combine them with **OpenStreetMap (OSM)** layers. Census data
tells you *who* lives in an area; OSM tells you *what is there* (stores, schools, transit).
Together they support access studies, public health work and planning research.

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

Stress responsible use of free services: one request per second for Nominatim, and no bulk
geocoding of personal addresses without considering privacy. Remind learners that match rates
depend heavily on address quality.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

## 1. Geocode one address with the Census Geocoder

```python
import requests

def get_coordinates(address):
    reply = requests.get(
        "https://geocoding.geo.census.gov/geocoder/locations/onelineaddress",
        params={"address": address, "benchmark": "Public_AR_Current", "format": "json"},
        timeout=30,
    )
    matches = reply.json()["result"]["addressMatches"]
    if matches:
        point = matches[0]["coordinates"]
        return point["y"], point["x"]   # latitude, longitude
    return None, None

get_coordinates("101 N Grant St, West Lafayette, IN 47906")
```

## 2. Geocode a list and turn it into map points

```python
import pandas as pd
import geopandas as gpd

# pandas reads the file straight from its web address into memory
museums_url = "https://raw.githubusercontent.com/SpatialTurn/DataCollection/main/data/museums.txt"
museums = pd.read_csv(museums_url, sep="\t", header=None, names=["Name", "Address"])
results = museums["Address"].apply(get_coordinates)
museums["Latitude"] = [lat for lat, lon in results]
museums["Longitude"] = [lon for lat, lon in results]

matched = museums.dropna(subset=["Latitude"])
points = gpd.GeoDataFrame(
    matched,
    geometry=gpd.points_from_xy(matched["Longitude"], matched["Latitude"]),
    crs="EPSG:4326",     # latitude and longitude
)
points.explore(tooltip="Name", tiles="Esri.WorldGrayCanvas")
```

`tiles="Esri.WorldGrayCanvas"` sets a light grey background map. Some popular backgrounds do not work
inside Colab: the default OpenStreetMap one shows "403 Access blocked" and CARTO shows "API key required".

Always check the rows that did not match (`museums[museums["Latitude"].isna()]`). Missing street
numbers, typos, and places absent from the Census address database (campuses, parks, large landmarks)
are the usual causes. Campus addresses such as "610 Purdue Mall" fail for this reason.

## 3. Add context from OpenStreetMap

OSM features are described by **tags** such as `shop=supermarket` or `amenity=school`
(see the [Map Features list](https://wiki.openstreetmap.org/wiki/Map_features)).

```python
import osmnx as ox

stores = ox.features_from_place("West Lafayette, Indiana, USA", tags={"shop": "supermarket"})
stores = stores.reset_index()[["name", "geometry"]]
stores["geometry"] = stores.geometry.representative_point()   # polygons to points
stores.explore(tooltip="name", color="green", tiles="Esri.WorldGrayCanvas")
```

## 4. Measure what is nearby

To count features within a distance, first **reproject to meters**. Buffers on latitude and
longitude would be measured in degrees.

```python
lat, lon = get_coordinates("101 N Grant St, West Lafayette, IN 47906")
campus = gpd.GeoDataFrame(geometry=gpd.points_from_xy([lon], [lat]), crs="EPSG:4326")

campus_m = campus.to_crs(epsg=5070)      # USA Contiguous Albers, units are meters
stores_m = stores.to_crs(epsg=5070)

one_mile = campus_m.buffer(1600).iloc[0]          # circle with a 1 mile (1,600 m) radius
stores_m[stores_m.within(one_mile)]               # supermarkets within 1 mile of campus
```

:::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: Query a different OSM feature

Download schools (`amenity=school`) or parks (`leisure=park`) for West Lafayette and map them.

:::::::::::::::::::::::: solution

```python
parks = ox.features_from_place("West Lafayette, Indiana, USA", tags={"leisure": "park"})
parks.explore(color="darkgreen", tiles="Esri.WorldGrayCanvas")
```

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::: challenge

## Challenge 2: Why did it fail?

The National Gallery of Art is listed as `Constitution Ave NW, Washington, DC 20565`.
Why does the Census Geocoder fail on it, and how would you fix it?

:::::::::::::::::::::::: solution

There is no street number, so the geocoder cannot place it on the street. The gallery sits at a
corner, and the Census Geocoder understands intersections written with `&`:
`6th St & Constitution Ave NW, Washington, DC 20565` gives a match.

Some complete addresses still fail because they are not in the Census address database (in this list,
the Philadelphia Museum of Art). For those, try another geocoder such as Nominatim (notebook 2c).

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Geocoding converts text addresses into coordinates
- The U.S. Census Geocoder is free and works best with complete U.S. street addresses
- Always check match rates and inspect failed addresses
- OpenStreetMap tags (`key=value`) let you download context layers such as stores or schools
- Reproject to a meter based CRS before buffering or measuring distance

::::::::::::::::::::::::::::::::::::::::::::::::

## Notebooks

Work through these in order. Each one opens in Google Colab.

| Level | Notebook | What you will do |
|---|---|---|
| Beginner | <a href="https://colab.research.google.com/github/SpatialTurn/DataCollection/blob/main/notebooks/02a_Geocoding_Addresses.ipynb" target="_blank">2a. Geocoding Addresses</a> | Geocode museum addresses with the Census Geocoder and map them |
| Intermediate | <a href="https://colab.research.google.com/github/SpatialTurn/DataCollection/blob/main/notebooks/02b_Finding_Places_with_OSM.ipynb" target="_blank">2b. Finding Places with OpenStreetMap</a> | Download supermarkets by tag and reverse geocode a point |
| Advanced | <a href="https://colab.research.google.com/github/SpatialTurn/DataCollection/blob/main/notebooks/02c_Batch_Geocoding_and_Ambiguous_Names.ipynb" target="_blank">2c. Batch Geocoding and Ambiguous Names</a> | Geocode many places politely and resolve names like Springfield |
