# Initialize terrain inside of a Unity project.

Initialize terrain inside of a Unity project.

## Usage

``` r
make_unity(
  project,
  heightmap,
  overlay = NULL,
  side_length = 4097,
  scene_name = "terrainr_scene",
  action = TRUE,
  unity = find_unity()
)
```

## Arguments

- project:

  The directory path of the Unity project to create terrain inside.

- heightmap:

  The file path for the raster to transform into terrain.

- overlay:

  Optionally, a file path for an image overlay to layer on top of the
  terrain surface. Leave as NULL for no overlay.

- side_length:

  The side length, in map units, for the terrain tiles. Must be equal to
  2^x + 1, for any x between 5 and 12.

- scene_name:

  The name of the Unity scene to create the terrain in.

- action:

  Boolean: Execute the unifir "script" and create the Unity project? If
  FALSE, returns a non-executed script.

- unity:

  The location of the Unity executable to create projects with. By
  default, will be auto-detected by
  [unifir::find_unity](https://docs.ropensci.org/unifir/reference/find_unity.html)

## Value

An object of class "unifir_script", containing either an executed unifir
script (if action = TRUE) or a non-executed script object (if action =
FALSE).

## Examples

``` r
if (FALSE) { # \dontrun{
if (!isTRUE(as.logical(Sys.getenv("CI")))) {
  simulated_data <- data.frame(
    id = seq(1, 100, 1),
    lat = runif(100, 44.04905, 44.17609),
    lng = runif(100, -74.01188, -73.83493)
  )
  simulated_data <- sf::st_as_sf(simulated_data, coords = c("lng", "lat"))
  output_files <- get_tiles(simulated_data)
  temptiff <- tempfile(fileext = ".tif")
  merge_rasters(output_files["elevation"][[1]], temptiff)
  make_unity(file.path(tempdir(), "unity"), temptiff)
}
} # }
```
