# Add a uniform buffer around a bounding box for geographic coordinates

add_bbox_buffer calculates the great circle distance both corners of
your bounding box are from the centroid and extends those by a set
distance. Due to using Haversine/great circle distance,
latitude/longitude calculations will not be exact.

set_bbox_side_length is a thin wrapper around add_bbox_buffer which sets
all sides of the bounding box to (approximately) a specified length.

Both of these functions are intended to be used with geographic
coordinate systems (data using longitude and latitude for position). For
projected coordinate systems, a more sane approach is to use
[sf::st_buffer](https://r-spatial.github.io/sf/reference/geos_unary.html)
to add a buffer, or combine
[sf::st_centroid](https://r-spatial.github.io/sf/reference/geos_unary.html)
with the buffer to set a specific side length.

## Usage

``` r
add_bbox_buffer(data, distance, distance_unit = "meters", error_crs = NULL)

# S3 method for class 'sf'
add_bbox_buffer(data, distance, distance_unit = "meters", error_crs = NULL)

# S3 method for class 'Raster'
add_bbox_buffer(data, distance, distance_unit = "meters", error_crs = NULL)

# S3 method for class 'SpatRaster'
add_bbox_buffer(data, distance, distance_unit = "meters", error_crs = NULL)

set_bbox_side_length(
  data,
  distance,
  distance_unit = "meters",
  error_crs = NULL
)

# S3 method for class 'sf'
set_bbox_side_length(
  data,
  distance,
  distance_unit = "meters",
  error_crs = NULL
)

# S3 method for class 'Raster'
set_bbox_side_length(
  data,
  distance,
  distance_unit = "meters",
  error_crs = NULL
)

# S3 method for class 'SpatRaster'
set_bbox_side_length(
  data,
  distance,
  distance_unit = "meters",
  error_crs = NULL
)
```

## Arguments

- data:

  The original data to add a buffer around. Must be either an `sf` or
  `SpatRaster` object.

- distance:

  The distance to add or to set side lengths equal to.

- distance_unit:

  The units of the distance to add to the buffer, passed to
  [units::as_units](https://r-quantities.github.io/units/reference/units.html).

- error_crs:

  Logical: Should this function error if `data` has no CRS? If `TRUE`,
  function errors; if `FALSE`, function quietly assumes EPSG:4326. If
  `NULL`, the default, function assumes EPSG:4326 with a warning.

## Value

An `sfc` object (from
[sf::st_as_sfc](https://r-spatial.github.io/sf/reference/st_as_sfc.html)).

## See also

Other utilities:
[`calc_haversine_distance()`](https://docs.ropensci.org/terrainr/reference/calc_haversine_distance.md),
[`deg_to_rad()`](https://docs.ropensci.org/terrainr/reference/deg_to_rad.md),
[`get_centroid()`](https://docs.ropensci.org/terrainr/reference/get_centroid.md),
[`rad_to_deg()`](https://docs.ropensci.org/terrainr/reference/rad_to_deg.md)

## Examples

``` r

df <- data.frame(
  lat = c(44.04905, 44.17609),
  lng = c(-74.01188, -73.83493)
)

df_sf <- sf::st_as_sf(df, coords = c("lng", "lat"))
df_sf <- sf::st_set_crs(df_sf, 4326)

add_bbox_buffer(df_sf, 10)
#> Geometry set for 1 feature 
#> Geometry type: POLYGON
#> Dimension:     XY
#> Bounding box:  xmin: -74.01197 ymin: 44.04899 xmax: -73.83484 ymax: 44.17615
#> Geodetic CRS:  WGS 84
#> POLYGON ((-74.01197 44.04899, -73.83484 44.0489...

df <- data.frame(
  lat = c(44.04905, 44.17609),
  lng = c(-74.01188, -73.83493)
)

df_sf <- sf::st_as_sf(df, coords = c("lng", "lat"))
df_sf <- sf::st_set_crs(df_sf, 4326)

set_bbox_side_length(df_sf, 4000)
#> Geometry set for 1 feature 
#> Geometry type: POLYGON
#> Dimension:     XY
#> Bounding box:  xmin: -73.94855 ymin: 44.09461 xmax: -73.89844 ymax: 44.13059
#> Geodetic CRS:  WGS 84
#> POLYGON ((-73.94855 44.09461, -73.89844 44.0946...
```
