---
name: Illinois Building Inventory Project
tools: [Python, Altair, vega-lite]
image: [assets/json/building_age_size_scatter.json, assets/json/building_usage_dashboard.json]
description: Interactive visualizations of Illinois state building data showing agency space distribution and construction trends over time!
custom_js:
  - vega.min
  - vega-lite.min
  - vega-embed.min
  - justcharts
---


# Illinois State Building Inventory

Interactive analysis of over 8,000 Illinois state-owned buildings

---

## Visualization 1: Agency Space Analysis

<vegachart schema-url="{{ site.baseurl }}/assets/json/building_age_size_scatter.json" style="width: 100%"></vegachart>

## About this visualization


### Design Choices


### Data Transformations:

### Interactivity:

---

## Visualization 2: Building Construction Over Time

<vegachart schema-url="{{ site.baseurl }}/assets/json/building_usage_dashboard.json" style="width: 100%"></vegachart>

## About this visualization


### Design Choices


### Data Transformations:

### Interactivity:

---



<!-- these are written in a combo of html and liquid --> 

---
## The Data

Illinois state building inventory data containing information about 8,862 buildings including square footage, construction year, agency ownership, location, and usage type.

<div class="left">
{% include elements/button.html link="https://raw.githubusercontent.com/UIUC-iSchool-DataViz/is445_data/main/building_inventory.csv" text="The Data" %}
</div>

## The Analysis

Complete Python analysis using Pandas and Altair to create these interactive visualizations.

<div class="right">
{% include elements/button.html link="https://github.com/smritit2/smritit2.github.io/blob/main/python_notebooks/Workbook.ipynb" text="The Analysis" %}
</div>
---