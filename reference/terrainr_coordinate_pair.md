# Construct a terrainr_coordinate_pair object.

In order to simplify code, most `terrainr` functions expect a set S4
class representation of coordinate pairs and bounding boxes. If the
provided data isn't in the expected S4 format, these functions are used
to cast the data into the target class.

## Usage

``` r
terrainr_coordinate_pair(coords, coord_units = c("degrees", "radians"))
```

## Arguments

- coords:

  A vector of length 2 containing a latitude and longitude. If unnamed,
  coordinates are assumed to be in (latitude, longitude) format; if
  named, the function will attempt to figure out which value represents
  which coordinate. Currently this function understands "lat",
  "latitude", and "y" as names for latitude and "lng", "long",
  "longitude", and "x" for longitude.

- coord_units:

  String indicating whether coordinates are in degrees or radians.
  Degrees stored in radians will be converted to degrees.

## Value

`terrainr_coordinate_pair` object

## See also

Other classes and related functions:
[`terrainr_coordinate_pair-class`](https://docs.ropensci.org/terrainr/reference/terrainr_coordinate_pair-class.md)
