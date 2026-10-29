# Extract latitude and longitude from a provided object

This is an internal utility function to convert bounding boxes into
coordinate pairs.

## Usage

``` r
calc_haversine_distance(point_1, point_2)
```

## Arguments

- point_1, point_2:

  Coordinate pairs (as length-2 numeric vectors with the names "lat" and
  "lng") to calculate distance between.

## Value

A vector of length 1 containing distance between points

## See also

Other utilities:
[`addbuff`](https://docs.ropensci.org/terrainr/reference/addbuff.md),
[`deg_to_rad()`](https://docs.ropensci.org/terrainr/reference/deg_to_rad.md),
[`get_centroid()`](https://docs.ropensci.org/terrainr/reference/get_centroid.md),
[`rad_to_deg()`](https://docs.ropensci.org/terrainr/reference/rad_to_deg.md)
