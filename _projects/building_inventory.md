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

This scatter plot explores the relationship between building age and square footage across nine major Illinois state agencies. The visualization reveals patterns in how different agencies manage their building portfolios, with some agencies maintaining older, smaller buildings while others operate newer, larger facilities.

### Design Choices

-- The visualization uses quantitative encoding for both axes. Building Age on the x-axis and Square Footage on the y-axis with a logarithmic scale. The log scale was essential given the extreme range in building sizes—from small 20 square foot structures to facilities exceeding 200,000 square feet. Without the log transformation, smaller buildings would be compressed at the bottom of the chart, making patterns impossible to discern.

-- Color encoding distinguishes the nine agencies using a nominal categorical scale. I selected Altair's default categorical color scheme because it provides sufficient contrast to differentiate between agencies while remaining visually accessible. The agencies chosen for this visualization represent diverse state functions: universities (University of Illinois, Southern Illinois University, Illinois State University), public services (Department of Human Services, Department of Juvenile Justice, Department of State Police), and specialized agencies (Historic Preservation Agency, Department of Agriculture, Department of Military Affairs).

Each data point is rendered as a circle mark with tooltips providing detailed information including building name, location, usage type, and status, enabling deep exploration of individual facilities.

### Data Transformations:

Several data cleaning steps were necessary to create an accurate visualization. First, I filtered out invalid year values—removing buildings with Year Constructed values of 0 or unrealistic dates (before 1800 or after 2025). This eliminated 295 records with data quality issues.

Second, I removed buildings with zero reported square footage (25 buildings), as these represented incomplete records that would skew the visualization. While these buildings may be important for administrative purposes, including them would create misleading patterns.

Third, I created a calculated "Building Age" column by subtracting the Year Constructed from 2025, converting the temporal data into a more intuitive measure of building age for analysis.

Finally, I filtered the dataset to include only nine agencies from the original 35+ agencies in the dataset. This focused selection prevents overcrowding while still representing a diverse cross-section of state operations with sufficient data points (2,590 buildings total) to reveal meaningful patterns.

### Interactivity:

The visualization features legend-based selection interactivity. Users can click on agency name in the legend to highlight specific agency while fading others to 20% opacity. This interactive filtering allows for focused analysis of individual agencies or comparative analysis between selected agencies.

This interactivity enhances the visualization by enabling users to answer specific questions like "How does the University of Illinois building portfolio compare to Southern Illinois University?" or "Does the Historic Preservation Agency maintain older buildings than other agencies?" without cluttering the initial view. The tooltips complement this by providing detailed building information on hover, supporting both exploratory analysis and specific information lookup.

---

## Visualization 2: Building Construction Over Time

<vegachart schema-url="{{ site.baseurl }}/assets/json/building_usage_dashboard.json" style="width: 100%"></vegachart>

## About this visualization

This linked dashboard analyzes Illinois state buildings under 2,000 square feet, examining both the distribution of building usage types and the size characteristics within those categories. The dual-chart design with interactive brushing enables dynamic exploration of how different building purposes correlate with building size.

### Design Choices

-- The dashboard uses a horizontal concatenation layout (side-by-side arrangement) to facilitate comparison between categorical distribution and quantitative distribution.

-- The left chart employs a horizontal bar chart with nominal encoding for building usage types on the y-axis, sorted in descending order by count. The x-axis uses quantitative encoding to show the number of buildings in each category. This design makes it easy to quickly identify that "Unusual" buildings dominate the inventory, followed by Storage and Industrial facilities. The horizontal orientation provides more space for category labels and improves readability.

-- The right chart is a histogram using quantitative encoding with binning. Square Footage is binned into 30 intervals on the x-axis, while the y-axis shows the count of buildings in each size range. This binning strategy balances detail with readability—too few bins would obscure the distribution, while too many would create noise.

-- Color encoding in the left chart uses a conditional scheme. Selected usage types display in a blue gradient based on their count value, while unselected types appear in light gray. This provides clear visual feedback about what is currently selected and emphasizes the filtered data. The right histogram uses a consistent blue color since it dynamically updates based on the selection.

### Data Transformations:

The primary transformation for this visualization was filtering to buildings under 2,000 square feet. This subset represents 4448 of the 8,862 buildings in the dataset—the smaller structures that serve specialized purposes across the state.

This filtering decision serves two purposes: first, it focuses on a meaningful subset where usage type patterns are more consistent (very large buildings tend to be multipurpose). And second, it creates a more readable histogram distribution. The full dataset's histogram would be heavily right-skewed with extreme outliers, making the distribution of typical building sizes difficult to interpret.

The histogram uses automatic binning set to a maximum of 30 bins, allowing Altair to optimize bin boundaries based on the data distribution. This creates intuitive size ranges that align with common building size categories.

### Interactivity:

The dashboard implements brushing and linking through an interval selection on the y-axis of the left chart. Users click and drag across usage type categories to select one or multiple types. Selected categories remain colored while unselected categories fade to gray, providing clear visual feedback.

The right histogram is dynamically filtered through a transform filter linked to the brush selection—it instantly updates to show only the size distribution of the selected usage types. This linked interaction enables comparative questions like "Are Storage buildings generally smaller than Industrial buildings?" or "What's the typical size range for Residential facilities?"

The interactivity makes this visualization significantly more powerful than two static charts. Users can explore hypotheses, compare categories, and discover unexpected patterns (for example, that "Unusual" buildings have a relatively consistent size profile despite their diverse purposes). Tooltips on both charts provide exact counts and size ranges on hover, supporting precise interpretation. This interaction model follows the "overview first, zoom and filter, details on demand" principle, making the dashboard both accessible for casual exploration and powerful for detailed analysis.

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