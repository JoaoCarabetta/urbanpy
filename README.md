# Welcome to UrbanPy :city_sunrise:

**A library to download, process and visualize high resolution urban data in an easy and fast way.**

UrbanPy is an open source project to automate data extraction, measurement, and visualization of urban accessibility metrics.

# Functional goals

- [x] Download open source spatial data (Limits & Points of Interests)
- [x] Allow for the use of a grid system or administrative boundaries as spatial units 
- [x] Origin-destination matrix calculation by any mode using a routing API
- [x] Obtain travel time from spatial units to the closest facilities
- [x] Consolidate the results as tables and/or shapefiles (georeferenced datasets)
- [x] Visualise the results as maps

# UX goals

- [ ] Atomic functions (one purpose per function)
- [x] Use the power of Python Geospatial Ecosystem under the hood
- [ ] Allow to flexible processing pipelines (custom layer/metrics aggregations)
- [x] Clear documentation with usage and examples
- [x] Clear and replicable example notebooks

## Main modules

- download: Main functions for data download from Nominatin API, OverPass API and HDX population data
- geom: Spatial operations, grid partitioning, spatial filtering and street network statistics
- plotting: Visualization wrappers for plotly and pydeck
- routing: Distance matrix computations (may require your own API keys)
- utils: Data handling helpers

## Installation

```sh
$ pip install urbanpy
```

### Dependencies

* pandas
* geopandas
* shapely
* numpy
* requests
* h3
* numba
* matplotlib

It is important to note that for travel time computation, if needed, a method
is implements the Open Source Routing Machine (OSRM). This method pulls, extracts and
add graph weights to the downloaded network and runs the routing server. Make sure
to have docker installed for the library to work correctly. Urbanpy provides a
simple approximation with nearest neighbor search using a
BallTree and haversine distance, but the difference between
real travel time and the approximation may vary from city to city.  

Additionally, the use of spatial libraries like osmnx, geopandas and h3 require certain extra packages.
Specifically, for rtree (spatial indexing to allow spatial joins) libspatialindex is required.
OSMnx and Geopandas requiere GDAL as well. If not handled by installing geopandas's dependencies, installing
fiona, pyproj and shapely should satisfy the requirements.
H3 requires cc, make, and cmake in your $PATH when installing, otherwise installation will not be successful

# Examples

UrbanPy lets you download and visualize city boundaries extremely easy:
```python
import urbanpy as up

boundaries = up.download.download_osm(2, 'Lima, Peru')
boundaries.plot()
```

Since `boundaries` is a GeoDataFrame it can be easily plotted with the method `.plot()`. You can also generate hexagons to fill the city boundaries in a oneliner.

```python
hexs, hexs_centroids = up.geom.gen_hexagons(resolution=9, city=boundaries)
```

Also check our [example notebooks](/notebooks), and if you have examples or visualizations of your own, we encourage you to share contribute.

## License

UrbanPy is completely free and open source and licensed under the [Creative Commons 3.0](https://creativecommons.org/licenses/by-nc-nd/3.0/igo/) license.
