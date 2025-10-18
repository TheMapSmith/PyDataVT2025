# Implementation Plan: Vermont Geospatial Analysis Workshop

## Overview
This notebook will demonstrate a complete geospatial workflow using Vermont GIS data from the VCGI Open Data Portal and Vermont ANR map services. Attendees will learn to fetch data from REST endpoints, create interactive visualizations, perform spatial operations, and analyze results.

## Learning Objectives
- Fetch and cache GeoJSON data from ArcGIS REST endpoints
- Create interactive maps with Folium/ipyleaflet
- Perform spatial queries and filtering
- Execute geometry clipping operations with GeoPandas
- Visualize spatial analysis results with charts

## Data Sources
1. **Town Boundaries** (VCGI)
   - Source: VCGI OpenData Boundary Service
   - Format: GeoJSON via ArcGIS REST API
   - URL: https://services1.arcgis.com/BkFxaEFNwHqX3tAw/arcgis/rest/services/FS_VCGI_OPENDATA_Boundary_BNDHASH_poly_towns_SP_v1/FeatureServer/0/query?outFields=*&where=1%3D1&f=geojson

2. **Bedrock Geology Units** (VT ANR)
   - Source: Vermont Agency of Natural Resources
   - Format: GeoJSON via ArcGIS REST API query
   - Endpoint: https://anrmaps.vermont.gov/arcgis/rest/services/Open_Data/OPENDATA_ANR_GEOLOGIC_SP_NOCACHE_v2/MapServer/165

3. **Basemap**
   - Source: National Geographic/Esri
   - Format: Vector Tile Layer
   - URL: https://basemaps.arcgis.com/arcgis/rest/services/World_Basemap_v2/VectorTileServer

## Implementation Steps

### ✅ Step 1: Workshop Overview and Setup
**Status**: Done
- Create notebook introduction with learning objectives
- List required libraries and versions
- Explain the workflow and data sources
- Include cell for environment setup and imports

### Step 2: Data Fetching - Town Boundaries
**Status**: Done
- Fetch town boundaries GeoJSON from VCGI REST endpoint
- Implement caching mechanism (save to `data/towns.geojson`)
- Load data into GeoPandas GeoDataFrame
- Display basic statistics (number of towns, coordinate system info)
- Show sample of town names

### Step 3: Interactive Town Selector UI
**Status**: Done
- Create dropdown widget with town names
- Display selected town information
- Handle selection events

### Step 4: Initial Map Visualization
**Status**: Pending
- Create interactive map using Folium or ipyleaflet
- Add National Geographic basemap
- Add bedrock geology MapService as tile layer
- Zoom to selected town boundary
- Display town outline on map
- Add layer controls

### Step 5: Geometry Query Function
**Status**: Pending
- Create function to query geology endpoint with bounding box
- Parameters: geometry (bbox from map), geometryType, inSR, spatialRel, outFields, returnGeometry, format
- Example query params:
  - endpoint: `https://anrmaps.vermont.gov/arcgis/rest/services/Open_Data/OPENDATA_ANR_GEOLOGIC_SP_NOCACHE_v2/MapServer/165/query`
  - geometry: `433198.0667214097,220634.09819474153,456466.88127535547,232619.96152487292`
  - geometryType: `esriGeometryEnvelope`
  - inSR: `32145` (Vermont State Plane)
  - spatialRel: `esriSpatialRelIntersects`
  - outFields: `*`
  - returnGeometry: `true`
  - f: `geojson`
- Implement caching by town name
- Return GeoDataFrame

### Step 6: Export Map Extent Button
**Status**: Pending
- Create button widget to trigger geometry query
- Get current map extent/bounds
- Convert bounds to appropriate coordinate system (EPSG:32145)
- Call query function with map extent
- Cache results locally (`data/geology_{townname}.geojson`)
- Display confirmation message with record count

### Step 7: Geometry Clipping
**Status**: Pending
- Clip queried geology polygons to selected town boundary
- Handle coordinate system transformations if needed
- Explain spatial overlay operations
- Show before/after geometry counts
- Display clipped data statistics

### Step 8: Enhanced Map with Clipped Data
**Status**: Pending
- Add clipped geology layer to map (not MapService)
- Style by geologic unit attributes
- Keep background MapService for context
- Add legend

### Step 9: Interactive Features
**Status**: Pending
- Add hover tooltips showing unit attributes
- Add click events to display full attribute information
- Create popup or side panel for detailed data
- Demonstrate GeoJSON-based interactivity advantages

### Step 10: Data Analysis and Visualization
**Status**: Pending
- Calculate area by geologic unit in clipped dataset
- Create summary table with unit names and areas
- Generate pie chart showing distribution
- Add bar chart for alternative visualization
- Explain area calculation considerations (projection, units)

### Step 11: Summary and Extensions
**Status**: Pending
- Recap workflow and key concepts
- Suggest extensions:
  - Query other layers from ANR services
  - Perform additional spatial analyses
  - Export to different formats
  - Create custom styling
  - Automate for multiple towns
- Provide resources for further learning

## Technical Considerations

### Libraries Required
- `geopandas` - Vector data manipulation
- `shapely` - Geometric operations
- `folium` or `ipyleaflet` - Interactive mapping
- `requests` - HTTP requests for REST APIs
- `ipywidgets` - Interactive UI components
- `matplotlib` - Static visualizations
- `pandas` - Data analysis
- `pyproj` - Coordinate transformations

### Data Management
- Create `data/` directory for cached files
- Cache town boundaries after first fetch
- Cache geology queries by town name
- Add appropriate `.gitignore` entries for large data files

### Coordinate Systems
- Vermont State Plane: EPSG:32145 (NAD83 / Vermont)
- WGS84: EPSG:4326 (for web maps)
- Handle transformations between systems as needed

### Error Handling
- Check for successful API responses
- Validate geometries
- Handle missing or null values
- Provide informative error messages

## Success Metrics
- Notebook runs top-to-bottom without errors
- All interactive components function correctly
- Maps display properly with correct styling
- Cached data reduces redundant API calls
- Educational content is clear and well-explained
- Code is well-commented and follows best practices

---

*This plan will be executed incrementally, with each step documented in PROMPT_HISTORY.md*
