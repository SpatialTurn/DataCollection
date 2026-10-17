# GIS Data Collection for Social Scientists

Source for the **Data Collection** module of
[Enabling the Geospatial Turn in the Social Sciences](https://spatialturn.github.io/),
published at <https://spatialturn.github.io/DataCollection/>.

The lesson is built with [The Carpentries Workbench](https://carpentries.github.io/sandpaper-docs/).

## Repository layout

| Folder | Contents |
|---|---|
| `episodes/` | The seven lesson pages and their figures |
| `notebooks/` | Google Colab notebooks linked from the Census episode (`01a` to `01c`) |
| `data/` | Small GeoJSON files loaded by URL in the network analysis episode |
| `learners/`, `instructors/`, `profiles/` | Setup, glossary, instructor notes and learner profiles |

| Episode file | Topic |
|---|---|
| `introduction.md` | Introduction to data collection |
| `repositories.md` | Finding data in repositories |
| `census.md` | Data from the U.S. Census Bureau (with notebooks 01a to 01c) |
| `imagery.md` | Scanned maps, CORONA and Sentinel-2 imagery |
| `field.md` | Collecting data in the field |
| `qfield.md` | QField demonstration: mapping grocery stores |
| `qfield-network.md` | Network analysis for grocery access in QGIS |

### Data

| File | Contents | Source |
|---|---|---|
| `data/grocery_stores.geojson` | 64 food stores in and around Lafayette and West Lafayette, Indiana (17 supermarkets, 2 wholesale, 45 convenience), October 2026 | (c) OpenStreetMap contributors, [Open Database License](https://opendatacommons.org/licenses/odbl/) |
| `data/roads.geojson` | 3,466 road segments covering both cities and a margin around them | U.S. Census Bureau, TIGER/Line 2024 (public domain) |
| `data/study_area.geojson` | City limits of Lafayette and West Lafayette | U.S. Census Bureau, 2024 cartographic boundary files (public domain) |

Figures named `dc_*.png` in `episodes/` were generated with Python from U.S. Census Bureau data (American
Community Survey 2020-2024 5-year estimates, 2020 Decennial Census, TIGER/Line and cartographic boundary
files) and OpenStreetMap data.

The notebooks need a free Census API key: <https://api.census.gov/data/key_signup.html>.

Contact: ilindsay@purdue.edu
