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


---

## Key Takeaways - Interactive UI

✅ **What we accomplished:**
1. Created an interactive dropdown with all Vermont town names
2. Implemented event-driven callback function for town selection
3. Displayed detailed town information including attributes and geometry
4. Calculated geographic properties (area, centroid, bounding box)
5. Stored selected town data in global variables for use in subsequent steps

💡 **Key Concepts:**
- **ipywidgets** provides interactive UI components for Jupyter
- **Event-driven programming**: Functions trigger automatically on user actions
- **Callback functions**: Handle user interactions and update content dynamically
- **Geometry properties**: `.area`, `.bounds`, `.centroid` from Shapely
- **Unit conversions**: Converting between m², km², and acres

🎯 **Best Practices Demonstrated:**
- Type hints in function signatures for clarity
- Docstrings explaining function purpose
- Error handling for edge cases (no data found)
- User-friendly formatting with visual separators
- Multiple unit representations for accessibility

🔜 **Next Steps:**
In the next section, we'll visualize the selected town on an interactive map with the bedrock geology layer!

---



### Understanding the Code Above

Let's break down what's happening in the interactive selector:

**1. Global Variables**
```python
selected_town_data = None
selected_town_name = None
```
These store the currently selected town so other cells can access it. This is a simple way to share state in notebooks.

**2. Callback Function**
```python
def on_town_selected(town_name: str) -> None:
```
This function runs every time a user selects a town. It:
- Filters the GeoDataFrame to get the selected town's data
- Calculates geographic properties (area, centroid, bounds)
- Displays formatted information

**3. Area Calculations**
```python
area_sq_m = town.geometry.area
area_sq_km = area_sq_m / 1_000_000
area_acres = area_sq_m / 4046.86
```
Since our CRS uses meters, `.area` returns square meters. We convert to km² and acres for readability.

**4. The `interact()` Function**
```python
interact(on_town_selected, town_name=town_dropdown)
```
This is the magic of ipywidgets! It:
- Creates the UI automatically
- Calls `on_town_selected()` whenever the dropdown changes
- Passes the selected value as the `town_name` parameter

**Try It Out!**
Select different towns from the dropdown above. Notice how the information updates immediately!



---

## Step 3: Interactive Town Selector

Now we'll create an interactive dropdown widget that lets users select a town and view its information. This demonstrates:
- Using `ipywidgets` for interactive UI components
- Event-driven programming in Jupyter notebooks
- Filtering GeoDataFrames based on user input
- Dynamic content updates

### Why Interactive Widgets?

Interactive widgets transform static notebooks into dynamic tools:
- **User-friendly**: No need to edit code to change parameters
- **Educational**: Great for exploration and "what-if" scenarios
- **Presentation-ready**: Professional appearance for demos and workshops
- **Reusable**: Easy for others to adapt for their own data

---

## Key Takeaways - Interactive Mapping

✅ **What we accomplished:**
1. Created an interactive web map with Folium
2. Transformed coordinates from Vermont State Plane to WGS84 for web display
3. Added multiple basemap options (OpenStreetMap, Satellite, Topographic)
4. Integrated VT ANR bedrock geology as a tile layer
5. Styled and added town boundary as a GeoJSON overlay
6. Implemented dynamic zoom levels based on town size
7. Added layer controls for interactive toggling
8. Placed a marker at the town center with popup

💡 **Key Concepts:**
- **CRS Transformation**: `.to_crs()` converts between coordinate systems
- **Tile Services**: Load map data dynamically as you pan/zoom
- **Layer Types**: Base layers (backgrounds) vs. overlay layers (data on top)
- **GeoJSON Styling**: Custom colors, opacity, and borders for vector features
- **Folium/Leaflet**: Python wrapper for creating Leaflet.js maps

🎯 **Mapping Best Practices:**
- Always convert to WGS84 (EPSG:4326) for web maps
- Provide multiple basemap options for context
- Use semi-transparent overlays so basemap shows through
- Add layer controls for user exploration
- Calculate appropriate zoom levels automatically
- Include scale bars and attributions

🔜 **Next Steps:**
In the next section, we'll query the geology data for the selected town and perform spatial analysis!

---



### Understanding the Map Code

Let's break down the key components of our mapping function:

**1. Coordinate System Transformation**
```python
town_wgs84 = town_data.to_crs(WGS84)
```
Web maps require WGS84 (lat/lon), but our data is in Vermont State Plane (meters). GeoPandas handles the conversion automatically.

**2. Dynamic Zoom Level**
```python
max_range = max(lat_range, lon_range)
if max_range > 0.5:
    zoom_start = 10
```
We calculate an appropriate zoom level based on town size. Larger towns need a lower zoom (zoomed out more) to fit in view.

**3. Multiple Basemaps**
We add three basemap options:
- **OpenStreetMap**: Default, good for streets and features
- **Satellite Imagery**: Aerial photos from Esri
- **Topographic**: Shows elevation and terrain

**4. Geology Tile Layer**
```python
geology_tile_url = f"{GEOLOGY_MAPSERVICE_URL}/tile/{{z}}/{{y}}/{{x}}"
```
The `{z}/{y}/{x}` placeholders are filled in by Leaflet as you pan/zoom. This allows the map to load only the tiles currently in view.

**5. GeoJSON Overlay**
```python
folium.GeoJson(town_wgs84, style_function=style_function)
```
We add the town boundary as a vector overlay with custom styling (red outline, transparent fill).

**6. Layer Controls**
```python
folium.LayerControl(position='topright', collapsed=False)
```
This creates the UI that lets users toggle layers on/off.

### Try It Out!

1. Select different towns from the dropdown above
2. Re-run this cell to see the map for each town
3. Use the layer control to toggle between basemaps
4. Toggle the geology layer on/off to see the difference
5. Click the marker to see the popup



---

## Step 4: Interactive Map Visualization

Now we'll create an interactive map to visualize the selected town with the bedrock geology layer. This demonstrates:
- Creating interactive web maps with Folium
- Adding tile layers from map services
- Converting coordinate systems (CRS transformation)
- Styling GeoJSON features
- Zooming to specific extents
- Adding layer controls for interactivity

### Understanding Folium Maps

Folium creates interactive Leaflet.js maps in Python. Key concepts:
- **Base layers**: Background maps (street maps, satellite, terrain, etc.)
- **Tile layers**: Dynamic map services that load tiles as you pan/zoom
- **Vector overlays**: GeoJSON features drawn on top of tiles
- **Layer controls**: UI for toggling layers on/off
- **CRS considerations**: Web maps use WGS84 (EPSG:4326), but our data is in Vermont State Plane

### ArcGIS REST Tile Services

We'll add the geology layer as a tile service. ArcGIS tile URLs follow this pattern:
```
{baseurl}/tile/{z}/{y}/{x}
```
Where `z` is zoom level, `y` is row, `x` is column in the tile grid.