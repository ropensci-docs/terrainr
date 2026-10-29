# Find latitude and longitude for a certain distance and azimuth from a point.

Find latitude and longitude for a certain distance and azimuth from a
point.

## Usage

``` r
point_from_distance(
  coord_pair,
  distance,
  azimuth,
  distance_unit = "meters",
  azimuth_unit = c("degrees", "radians")
)
```

## Arguments

- coord_pair:

  A numeric vector of length 2 with names "lat" and "lng"

- distance:

  A distance (in meters) representing the distance away from the
  original point to apply

- azimuth:

  A azimuth (in units specified in `azimuth_unit`) representing the
  direction to apply the distance from the original point in

- distance_unit:

  A string passed to convert_distance indicating the units of the
  provided distance.

- azimuth_unit:

  A string (either `degrees` or `radians`) indicating the units of the
  `azimuth` argument

## Value

An object of class
[terrainr_coordinate_pair](https://docs.ropensci.org/terrainr/reference/terrainr_coordinate_pair.md).
