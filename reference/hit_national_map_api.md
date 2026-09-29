# Hit the USGS 3DEP API and retrieve an elevation heightmap

This function retrieves a single tile of data from a single National Map
service and returns the raw response. End users are recommended to use
[get_tiles](https://docs.ropensci.org/terrainr/reference/get_tiles.md)
instead, as it does much more validation and provides a more friendly
interface. For a description of the datasets provided by the National
Map, see <https://apps.nationalmap.gov/services>

## Usage

``` r
hit_national_map_api(
  bbox,
  img_width,
  img_height,
  service,
  verbose = FALSE,
  ...
)
```

## Arguments

- bbox:

  An object from
  [sf::st_bbox](https://r-spatial.github.io/sf/reference/st_bbox.html).

- img_width:

  The number of pixels in the x direction to retrieve

- img_height:

  The number of pixels in the y direction to retrieve

- service:

  A string indicating what service API to use. For a full list of
  available services, see
  [get_tiles](https://docs.ropensci.org/terrainr/reference/get_tiles.md).
  Short codes are not accepted by this function.

- verbose:

  Logical: Print out the number of tries required to pull each tile?
  Default `FALSE`.

- ...:

  Additional arguments passed to the National Map API. These can be used
  to change default query parameters or as additional options for the
  National Map services. See below for more information.

## Value

A raw vector.

## Additional Arguments

The `...` argument can be used to pass additional arguments to the
National Map API or to edit the hard-coded defaults used by this
function. Some of the most useful options that can be changed include:

- `bboxSR`: The spatial reference of the bounding box given to this
  function. If not specified, assumed to be
  [4326](https://spatialreference.org/ref/epsg/4326/).

- `imageSR`: The spatial reference of the image downloaded. If not
  specified, assumed to be
  [4326](https://spatialreference.org/ref/epsg/4326/).

- layers: Which data layers to download. If the National Map API returns
  data without specifying layers, this argument isn't used by default.
  When the National Map requires this argument, the default value is 0.

- format: The image format to be downloaded. Defaults depend on the
  service being used and are set to be compatible with
  [get_tiles](https://docs.ropensci.org/terrainr/reference/get_tiles.md).

Pass these arguments to `hit_national_map_api` like you would any other
argument to substitute new values. Note that `...` values are never
validated before being used; passing invalid parameters to `...` will
cause data retrieval to fail.

## See also

[get_tiles](https://docs.ropensci.org/terrainr/reference/get_tiles.md)
for a friendlier interface to the National Map API.

Other data retrieval functions:
[`get_tiles()`](https://docs.ropensci.org/terrainr/reference/get_tiles.md)

## Examples

``` r
if (FALSE) { # \dontrun{
hit_national_map_api(
  bbox = list(
    c(lat = 44.10438, lng = -74.01231),
    c(lat = 44.17633, lng = -73.91224)
  ),
  img_width = 8000,
  img_height = 8000,
  service = "3DEPElevation"
)
} # }
```
