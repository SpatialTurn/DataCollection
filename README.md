# GIS Data Collection for Social Scientists

Source for the **Data Collection** module of
[Enabling the Geospatial Turn in the Social Sciences](https://spatialturn.github.io/),
published at <https://spatialturn.github.io/DataCollection/>.

The lesson is built with [The Carpentries Workbench](https://carpentries.github.io/sandpaper-docs/).

## Repository layout

| Folder | Contents |
|---|---|
| `episodes/` | The six lesson pages and their figures |
| `notebooks/` | Google Colab notebooks linked from the Census episode (`01a` to `01c`) and the Geocoding episode (`02a` to `02c`) |
| `data/` | `museums.txt`, read by URL in the Geocoding episode and notebook 2a |
| `learners/`, `instructors/`, `profiles/` | Setup, glossary, instructor notes and learner profiles |

| Episode file | Topic |
|---|---|
| `introduction.md` | Introduction to data collection |
| `repositories.md` | Finding data in repositories |
| `census.md` | Data from the U.S. Census Bureau (with notebooks 01a to 01c) |
| `geocoding.md` | Geocoding and adding spatial context (with notebooks 02a to 02c; moved from the Data Analysis module in October 2026) |
| `imagery.md` | Scanned maps, CORONA and Sentinel-2 imagery |
| `field.md` | Collecting data in the field |

### Data

| File | Contents | Source |
|---|---|---|
| `data/museums.txt` | Names and street addresses of 15 U.S. museums (tab separated, no header), for geocoding practice | This project |

The QField demonstration and the QGIS network analysis, with their Lafayette GeoJSON files, moved to the
[Case Studies module](https://github.com/SpatialTurn/CaseStudies) in October 2026.

Figures named `dc_*.png` in `episodes/` were generated with Python from U.S. Census Bureau data (American
Community Survey 2020-2024 5-year estimates, 2020 Decennial Census, TIGER/Line and cartographic boundary
files) and OpenStreetMap data.

The notebooks need a free Census API key: <https://api.census.gov/data/key_signup.html>.

Contact: ilindsay@purdue.edu
