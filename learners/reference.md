---
title: 'Reference'
---

## Glossary

American Community Survey (ACS)
:   A yearly U.S. Census Bureau survey of about 3.5 million addresses that produces estimates on social,
    economic and housing topics. Published as 1-year and 5-year estimates, each with a margin of error.

Annotation code
:   A special negative value, such as `-666666666`, that the Census API returns instead of an estimate when
    a value cannot be calculated. Replace it with "missing" before calculating.

API (Application Programming Interface)
:   A way for a program to request data from a server with a structured web address, instead of a person
    clicking through a website.

Block group
:   A census geography inside a tract, usually with 600 to 3,000 people. The smallest area with ACS 5-year
    estimates.

Cartographic boundary file
:   A simplified Census Bureau boundary file, clipped to the shoreline, designed for thematic maps. Its
    file names start with `cb_`.

Census tract
:   A small, fairly permanent census area of about 1,200 to 8,000 people (4,000 on average), used to compare
    neighborhoods over time.

Coefficient of variation (CV)
:   A measure of how reliable an estimate is: the standard error as a percentage of the estimate. For ACS
    data, `CV = (MOE / 1.645) / estimate x 100`.

CORONA
:   A U.S. reconnaissance satellite program (1960 to 1972) whose more than 860,000 images were declassified
    in 1995.

Coordinate reference system (CRS)
:   The system that links map coordinates to places on Earth, identified by an EPSG code such as EPSG:4326
    (latitude and longitude) or EPSG:26916 (UTM zone 16N, in meters).

Decennial Census
:   The U.S. count of every person, taken every ten years. It has no margin of error but asks only a few
    questions.

Digitizing
:   Creating vector features by tracing them from a map or image.

FAIR principles
:   Guidelines for making data Findable, Accessible, Interoperable and Reusable.

FIPS code
:   A Federal Information Processing Standards code identifying a state (2 digits) or county (3 digits).

GEOID
:   A census geography's identifier, built by joining FIPS and other codes, for example `18157` for
    Tippecanoe County, Indiana. Used to join census tables to boundaries. Keep it as text.

Georeferencing
:   Assigning real-world coordinates to a scanned map or image so it lines up with other layers.

GNSS (Global Navigation Satellite System)
:   Satellite positioning systems, including GPS, Galileo, GLONASS and BeiDou, used by phones and receivers
    to determine location.

Group quarters
:   Places where people live in a group, such as university residence halls, nursing homes and prisons.
    Their residents are not counted as households.

Margin of error (MOE)
:   The range around an ACS estimate within which the true value lies with 90% confidence.

Metadata
:   Documentation describing a dataset: who made it, when, how, where it covers, its attributes, its
    coordinate system and its license.

Network analysis
:   Analysis of movement along a network, such as roads, for example finding shortest paths or service
    areas.

QField
:   A free, open source app for collecting field data on phones and tablets, using projects prepared in
    QGIS.

Raster data
:   Data stored as a grid of cells, each with a value, such as a satellite image or elevation model.

Resolution
:   For imagery: the ground size of one pixel (spatial), the number of wavelength bands (spectral), or how
    often an area is imaged (temporal).

Schema
:   The planned list of fields in a dataset, with their types and allowed values.

Sentinel-2
:   European Union Copernicus satellites providing free 13-band imagery at 10 to 60 m resolution about
    every 5 days.

Service area
:   The part of a network that can be reached from a starting point within a given distance or time.

Shortest path
:   The route between two points along a network with the lowest total distance (or time).

TIGER/Line
:   The Census Bureau's full-detail geographic files of boundaries and features such as roads. Their file
    names start with `tl_`.

Vector data
:   Data stored as points, lines or polygons, each with attributes.

ZCTA (ZIP Code Tabulation Area)
:   A census approximation of a ZIP code's area, used to publish census data by ZIP code.

## Further reading and tools

- [Census Data API user guide](https://www.census.gov/data/developers/guidance/api-user-guide.html)
- [Census Bureau: when to use 1-year or 5-year estimates](https://www.census.gov/programs-surveys/acs/guidance/estimates.html)
- [Census Bureau mapping files (TIGER/Line and cartographic boundaries)](https://www.census.gov/geographies/mapping-files.html)
- [USGS: declassified satellite imagery](https://www.usgs.gov/centers/eros/science/usgs-eros-archive-declassified-data-declassified-satellite-imagery-1)
- [Copernicus Browser documentation](https://documentation.dataspace.copernicus.eu/Applications/Browser.html)
- [QField documentation](https://docs.qfield.org/)
- [GO FAIR: the FAIR principles](https://www.go-fair.org/fair-principles/)
