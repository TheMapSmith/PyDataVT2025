# Interactive Vermont Geology Explorer
## A Geospatial Python Workshop

---

### Workshop Overview

Welcome! This notebook demonstrates a complete geospatial workflow using real-world Vermont GIS data. You'll learn to:

- **Fetch data from REST APIs**: Query ArcGIS REST endpoints to retrieve GeoJSON data
- **Build interactive visualizations**: Create dynamic maps with user controls
- **Perform spatial operations**: Clip, intersect, and analyze vector geometries
- **Analyze spatial data**: Calculate statistics and create visualizations
- **Optimize workflows**: Implement caching to reduce redundant API calls

### What We're Building

By the end of this notebook, you'll have an interactive tool that allows you to:
1. Select any Vermont town from a dropdown menu
2. View bedrock geology on an interactive map
3. Extract geology data for that specific town
4. Analyze the distribution of geologic units
5. Visualize results with charts and tables

### Learning Objectives

**Data Access**
- Query ArcGIS REST Feature Services and Map Services
- Understand REST API parameter structures
- Implement local caching strategies

**Geospatial Analysis**
- Work with coordinate reference systems (CRS)
- Perform spatial queries (bounding box intersections)
- Clip geometries using spatial overlays
- Calculate areas for polygon features

**Interactive Visualization**
- Create interactive web maps with Python
- Add user interface controls (dropdowns, buttons)
- Implement hover and click interactions
- Layer different data sources effectively

**Python Geospatial Ecosystem**
- Use GeoPandas for vector data manipulation
- Apply Shapely for geometric operations
- Build maps with Folium or ipyleaflet
- Leverage ipywidgets for interactivity

### Data Sources

This workshop uses public data from Vermont state agencies:

**1. Town Boundaries**
- **Source**: Vermont Center for Geographic Information (VCGI)
- **Endpoint**: VCGI OpenData Boundary Service
- **License**: Public domain
- **Format**: GeoJSON via ArcGIS REST API

**2. Bedrock Geology**
- **Source**: Vermont Agency of Natural Resources (ANR)
- **Endpoint**: ANR Geologic Map Service
- **License**: Public domain
- **Format**: GeoJSON via query (vector) and tile service (raster)

**3. Basemap**
- **Source**: National Geographic / Esri
- **Type**: Vector tile layer
- **Purpose**: Provides geographic context

### Prerequisites

**Python Knowledge**
- Basic Python syntax and data structures
- Familiarity with pandas DataFrames helpful but not required

**GIS Concepts**
- Basic understanding of coordinate systems (will be explained)
- Familiarity with vector data (points, lines, polygons)
- No prior GIS software experience required!

### Workflow Overview

```
1. Setup & Imports
   ↓
2. Fetch Town Boundaries → Cache Locally
   ↓
3. Create Town Selector UI
   ↓
4. Display Map with Geology Layer
   ↓
5. Query Geology for Selected Town → Cache Locally
   ↓
6. Clip Geology to Town Boundary
   ↓
7. Add Clipped Layer to Map (Interactive)
   ↓
8. Analyze & Visualize Results
```

---

### About This Notebook

This educational material was developed openly and transparently with AI assistance from Claude Code. The workflow demonstrates real-world geospatial analysis patterns you can adapt for your own projects.

**Repository**: [PyDataVT2025](https://github.com/yourusername/PyDataVT2025)

---

Let's get started!


## Environment Setup

First, let's import the required libraries. If you don't have these installed, see the `requirements.txt` file in the repository.

### Required Libraries:

- **`geopandas`**: GeoPandas extends pandas to work with geospatial data. It combines the capabilities of pandas with geometric operations from shapely.
- **`shapely`**: Library for geometric operations (automatically installed with geopandas)
- **`folium`**: Creates interactive Leaflet maps in Python
- **`requests`**: Simple HTTP library for making API calls
- **`ipywidgets`**: Interactive UI components for Jupyter notebooks
- **`matplotlib`**: Plotting library for charts and visualizations
- **`pathlib`**: Object-oriented filesystem paths (part of standard library)

### Coordinate Reference Systems (CRS)

We'll be working with two coordinate systems:
- **EPSG:32145** - Vermont State Plane (NAD83) - Used by Vermont state data, units in meters
- **EPSG:4326** - WGS84 - Standard for web maps (Google Maps, OpenStreetMap), units in degrees

### Create Data Directory

We'll cache downloaded data locally to avoid repeated API calls. This is a best practice when working with external data sources:
- Faster execution on subsequent runs
- Reduces load on data providers
- Enables offline work after initial download
- Makes your analysis reproducible

### Configuration

Let's define the URLs and parameters we'll use throughout the notebook. Keeping these at the top makes the code easier to maintain and adapt for other regions or data sources.


---

## Ready to Begin!

With our environment configured, we're ready to start fetching and working with geospatial data. In the next section, we'll download Vermont town boundaries and explore the data structure.

### Key Concepts to Remember:

1. **Caching**: We save downloaded data locally to avoid repeated API calls
2. **CRS**: Always be aware of which coordinate system your data uses
3. **REST APIs**: We'll interact with ArcGIS REST services using simple HTTP requests
4. **GeoJSON**: A standard format for encoding geographic data structures

Let's dive in! 🗺️



---

## Step 2: Fetching Vermont Town Boundaries

Now we'll fetch town boundary data from the VCGI OpenData portal. This demonstrates:
- Making HTTP requests to ArcGIS REST endpoints
- Implementing a caching strategy
- Loading GeoJSON into GeoPandas
- Inspecting geospatial data

### Understanding ArcGIS REST Services

ArcGIS REST services are web APIs that provide access to geographic data. The URL we're using includes:
- **Service endpoint**: Points to the specific layer (town boundaries)
- **Query parameters**:
  - `outFields=*` - Return all attribute fields
  - `where=1=1` - SQL clause that returns all features (always true)
  - `f=geojson` - Return format as GeoJSON

### Caching Strategy

We'll check if data exists locally before downloading. This:
- Speeds up subsequent notebook runs
- Reduces server load
- Enables offline work
- Ensures consistent data across runs


---

## Key Takeaways - Data Fetching

✅ **What we accomplished:**
1. Fetched Vermont town boundaries from ArcGIS REST endpoint
2. Implemented smart caching to avoid redundant downloads
3. Loaded GeoJSON data into a GeoPandas GeoDataFrame
4. Explored the data structure, attributes, and coordinate system
5. Identified the town name field for future selection

💡 **Key Concepts:**
- **REST APIs** provide programmatic access to GIS data
- **Caching** improves performance and enables offline work
- **GeoDataFrame** extends pandas with spatial capabilities
- **CRS (Coordinate Reference System)** defines how coordinates map to real-world locations

🔜 **Next Steps:**
In the next section, we'll create an interactive dropdown to select towns and view their properties.

---

### Town Name List

Let's get a sorted list of all Vermont town names. We'll use this in the next step to create our interactive selector.



### Sample Town Data

Let's look at a few example towns to understand the data structure better.

### Examining Attributes

Let's see what attribute fields are available for each town.


### Exploring the Data

Let's examine what we just downloaded. A GeoDataFrame is like a pandas DataFrame but with a special `geometry` column that stores shapes (polygons in this case).