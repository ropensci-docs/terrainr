# A user-friendly way to get USGS National Map data tiles for an area

This function splits the area contained within a bounding box into a set
of tiles, and retrieves data from the USGS National map for each tile.
As of version 0.5.0, the method for lists has been deprecated.

## Usage

``` r
get_tiles(
  data,
  output_prefix = tempfile(),
  side_length = NULL,
  resolution = 1,
  services = "elevation",
  verbose = FALSE,
  georeference = TRUE,
  projected = NULL,
  ...
)

# S3 method for class 'sf'
get_tiles(
  data,
  output_prefix = tempfile(),
  side_length = NULL,
  resolution = 1,
  services = "elevation",
  verbose = FALSE,
  georeference = TRUE,
  projected = NULL,
  ...
)

# S3 method for class 'sfc'
get_tiles(
  data,
  output_prefix = tempfile(),
  side_length = NULL,
  resolution = 1,
  services = "elevation",
  verbose = FALSE,
  georeference = TRUE,
  projected = NULL,
  ...
)

# S3 method for class 'Raster'
get_tiles(
  data,
  output_prefix = tempfile(),
  side_length = NULL,
  resolution = 1,
  services = "elevation",
  verbose = FALSE,
  georeference = TRUE,
  projected = NULL,
  ...
)

# S3 method for class 'SpatRaster'
get_tiles(
  data,
  output_prefix = tempfile(),
  side_length = NULL,
  resolution = 1,
  services = "elevation",
  verbose = FALSE,
  georeference = TRUE,
  projected = NULL,
  ...
)

# S3 method for class 'list'
get_tiles(
  data,
  output_prefix = tempfile(),
  side_length = NULL,
  resolution = 1,
  services = "elevation",
  verbose = FALSE,
  georeference = TRUE,
  projected = NULL,
  ...
)
```

## Arguments

- data:

  An `sf` or `SpatRaster` object; tiles will be downloaded for the full
  extent of the provided object.

- output_prefix:

  The file prefix to use when saving tiles.

- side_length:

  The length, in meters, of each side of tiles to download. If `NULL`,
  defaults to the maximum side length permitted by the least permissive
  service requested.

- resolution:

  How many meters are represented by each pixel? The default value of 1
  means that 1 pixel = 1 meter, while a value of 2 means that 1 pixel =
  2 meters, and so on.

- services:

  A character vector of services to download data from. Current options
  include "3DEPElevation", "USGSNAIPPlus", and "nhd". Users can also use
  short codes to download a specific type of data without specifying the
  source; current options for short codes include "elevation"
  (equivalent to "3DEPElevation"), "ortho" (equivalent to
  "USGSNAIPPlus), and "hydro" ("nhd"). Short codes are not guaranteed to
  refer to the same source across releases. Short codes are converted to
  their service name and then duplicates are removed, so any given
  source will only be queried once per tile.

- verbose:

  Logical: should tile retrieval functions run in verbose mode?

- georeference:

  Logical: should tiles be downloaded as PNGs without georeferencing, or
  should they be downloaded as georeferenced TIFF files? This option
  does nothing when only elevation data is being downloaded.

- projected:

  Logical: is `data` in a projected coordinate reference system? If
  `NULL`, the default, inferred from
  [sf::st_is_longlat](https://r-spatial.github.io/sf/reference/st_is_longlat.html).

- ...:

  Additional arguments passed to
  [hit_national_map_api](https://docs.ropensci.org/terrainr/reference/hit_national_map_api.md).
  These can be used to change default query parameters or as additional
  options for the National Map services. See below for more details.

## Value

A list of the same length as the number of unique services requested,
containing named vectors of where data files were saved to. Returned
invisibly.

## Available Datasources

The following services are currently available (with short codes in
parentheses where applicable). See links for API documentation.

- [3DEPElevation](https://elevation.nationalmap.gov/arcgis/rest/services/3DEPElevation/ImageServer)
  (short code: elevation)

- [USGSNAIPPlus](https://imagery.nationalmap.gov/arcgis/rest/services/USGSNAIPPlus/ImageServer/exportImage)
  (short code: ortho)

- [USGSNAIPImagery](https://imagery.nationalmap.gov/arcgis/rest/services/USGSNAIPImagery/ImageServer)

- [nhd](https://hydro.nationalmap.gov/arcgis/rest/services/nhd/MapServer)
  (short code: hydro)

- [govunits](https://carto.nationalmap.gov/arcgis/rest/services/govunits/MapServer)

- [contours](https://carto.nationalmap.gov/arcgis/rest/services/contours/MapServer)

- [geonames](https://carto.nationalmap.gov/arcgis/rest/services/geonames/MapServer)

- [NHDPlus_HR](https://hydro.nationalmap.gov/arcgis/rest/services/NHDPlus_HR/MapServer)

- [structures](https://carto.nationalmap.gov/arcgis/rest/services/structures/MapServer)

- [transportation](https://carto.nationalmap.gov/arcgis/rest/services/transportation/MapServer)

- [wbd](https://hydro.nationalmap.gov/arcgis/rest/services/wbd/MapServer)
  ("short code": watersheds)

- [ecosystems](https://www.usgs.gov/centers/geosciences-and-environmental-change-science-center/science/global-ecosystems)

- [USGSTopo](https://basemap.nationalmap.gov/arcgis/rest/services/USGSTopo/MapServer)

- [USGSShadedReliefOnly](https://basemap.nationalmap.gov/arcgis/rest/services/USGSShadedReliefOnly/MapServer)

- [USGSImageryOnly](https://basemap.nationalmap.gov/arcgis/rest/services/USGSImageryOnly/MapServer)

- [USGSHydroCached](https://basemap.nationalmap.gov/arcgis/rest/services/USGSHydroCached/MapServer)

## Additional Arguments

The `...` argument can be used to pass additional arguments to the
National Map API or to edit the hard-coded defaults used by this
function. More information on common arguments to change can be found in
[hit_national_map_api](https://docs.ropensci.org/terrainr/reference/hit_national_map_api.md).
Note that `...` can also be used to change the formats returned by the
server, but that doing so while using this function will likely cause
the function to error (or corrupt the output data). To download files in
different formats, use
[hit_national_map_api](https://docs.ropensci.org/terrainr/reference/hit_national_map_api.md).

## See also

Other data retrieval functions:
[`hit_national_map_api()`](https://docs.ropensci.org/terrainr/reference/hit_national_map_api.md)

## Examples

``` r
if (FALSE) { # \dontrun{
simulated_data <- data.frame(
  id = seq(1, 100, 1),
  lat = runif(100, 44.04905, 44.17609),
  lng = runif(100, -74.01188, -73.83493)
)

simulated_data <- sf::st_as_sf(simulated_data, coords = c("lng", "lat"))

get_tiles(simulated_data, tempfile())
} # }
```
