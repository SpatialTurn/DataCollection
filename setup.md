---
title: Setup
---

This module uses free tools only:

- **A web browser** for the repositories, the Census API and the imagery websites
- **Google Colab** for the Python notebooks in the Census and Geocoding episodes. It runs in your browser,
  so there is nothing to install.
- **QGIS** for the repositories and imagery episodes. It is a desktop program you install once.

## What you need

- A Google account (for Colab)
- A computer where you can install software (for QGIS)
- A free **Census API key** for Census notebooks 1b and 1c and the API examples (see below)
- Optional: free accounts on [USGS EarthExplorer](https://earthexplorer.usgs.gov/) and the
  [Copernicus Browser](https://browser.dataspace.copernicus.eu/) to download satellite imagery

## Part 1: Get a Census API key

**Every learner needs their own key.** It is free and takes a few minutes.

1. Go to <https://api.census.gov/data/key_signup.html>.
2. Enter your organization (for example, Purdue University) and your email address, and agree to the terms.
3. Check your email. The key arrives within a few minutes.
4. **Click the activation link in the email.** The key does not work until you do.
5. Keep the key somewhere safe. Treat it like a password: do not post it online or leave it in a notebook
   you share.

## Part 2: Google Colab

1. Click a notebook link in the table in the Census or Geocoding episode. It opens in Colab.
2. Click **File > Save a copy in Drive** so your changes are kept.
3. Paste your Census API key where the notebook asks for it.
4. Run cells from top to bottom: click a cell and press **Shift + Enter**.
5. If Colab warns that the notebook was not written by Google, click **Run anyway**.

The notebooks read all their data straight from the web (the Census Bureau's website, the Census Geocoder,
OpenStreetMap and this lesson's repository), so you never need to download anything. The geocoding notebooks
do not need a Census API key.

## Part 3: Install QGIS

**QGIS** is a free, open source Geographic Information System (GIS) for viewing, analyzing and mapping
spatial data.

1. Go to <https://qgis.org> and click **Download**.
2. Choose the **Long Term Release (LTR)** version, the most stable one.
   - **Windows:** the standalone installer (`.msi`)
   - **macOS:** the macOS installer (`.dmg`). The first time you open QGIS, you may need to right-click the
     app and choose **Open** to get past the security warning.
   - **Linux:** follow the instructions for your distribution on the QGIS download page
3. Run the installer and keep the default settings.
4. Open **QGIS Desktop**.

If you are new to QGIS, the Data Visualization module's "Getting Started with QGIS" episode introduces the
interface.

### Loading data from a web address in QGIS

The repositories episode loads data straight from the web:

1. **Layer > Add Layer > Add Vector Layer**
2. **Source Type**: **Protocol: HTTP(S), cloud, etc.**
3. Paste the address given in the episode into **URI**, then click **Add**

If you want to try field data collection with **QField**, see the setup page of the
[Case Studies module](https://spatialturn.github.io/CaseStudies/), where the QField demonstration lives.

## Troubleshooting

| Problem | Fix |
|---|---|
| The Census API returns a "Missing Key" or "Invalid Key" page | Check that you clicked the activation link in the email, and that the key was pasted completely |
| A notebook cell says `NameError` | A cell above it was skipped. Use **Runtime > Run before** |
| QGIS will not open on macOS | Right-click the app, choose **Open**, then confirm |
| A layer loaded from a web address shows nothing | Right-click the layer and choose **Zoom to Layer**; check that the address was pasted completely |
| The Census Geocoder returns no match | Check the address has a street number; campus and landmark addresses are often missing, so try Nominatim (notebook 2c) |
| An OpenStreetMap or Nominatim request times out | The free server is busy or rate limited; wait a minute and rerun the cell |
