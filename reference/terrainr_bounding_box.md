# Construct a terrainr_bounding_box object

In order to simplify code, most `terrainr` functions expect a set S4
class representation of coordinate pairs and bounding boxes. If the
provided data is not in the expected S4 format, these functions are used
to cast the data into the target class.

## Usage

``` r
terrainr_bounding_box(bl, tr, coord_units = "degrees")
```

## Arguments

- bl, tr:

  The bottom left (`bl`) and top right (`tr`) corners of the bounding
  box, either as a
  [terrainr_coordinate_pair](https://docs.ropensci.org/terrainr/reference/terrainr_coordinate_pair.md)
  object or a coordinate pair. If the coordinate pair is not named, it
  is assumed to be in (lat, lng) format; if it is named, the function
  will attempt to properly identify coordinates.

- coord_units:

  Arguments passed to
  [terrainr_coordinate_pair](https://docs.ropensci.org/terrainr/reference/terrainr_coordinate_pair.md).
  If `bl` and `tr` are already
  [terrainr_coordinate_pair](https://docs.ropensci.org/terrainr/reference/terrainr_coordinate_pair.md)
  objects, these arguments are not used.

## Value

An object of class terrainr_bounding_box.
