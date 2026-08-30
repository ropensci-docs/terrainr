# Plot RGB rasters in ggplot2

`geom_spatial_rgb` and `stat_spatial_rgb` allow users to plot three-band
RGB rasters in ggplot2, using these layers as background base maps for
other spatial plotting. Note that unlike
[ggplot2::geom_sf](https://ggplot2.tidyverse.org/reference/ggsf.html),
this function does *not* force
[ggplot2::coord_sf](https://ggplot2.tidyverse.org/reference/ggsf.html);
for accurate mapping, add
[ggplot2::coord_sf](https://ggplot2.tidyverse.org/reference/ggsf.html)
with a `crs` value matching your input raster as a layer.

## Usage

``` r
geom_spatial_rgb(
  mapping = NULL,
  data = NULL,
  stat = "spatialRGB",
  position = "identity",
  ...,
  hjust = 0.5,
  vjust = 0.5,
  interpolate = FALSE,
  na.rm = FALSE,
  show.legend = NA,
  inherit.aes = TRUE,
  scale = NULL
)

stat_spatial_rgb(
  mapping = NULL,
  data = NULL,
  geom = "raster",
  position = "identity",
  na.rm = FALSE,
  show.legend = FALSE,
  inherit.aes = TRUE,
  scale = NULL,
  ...
)
```

## Arguments

- mapping:

  Set of aesthetic mappings created by
  [`aes()`](https://ggplot2.tidyverse.org/reference/aes.html). If
  specified and `inherit.aes = TRUE` (the default), it is combined with
  the default mapping at the top level of the plot. You must supply
  `mapping` if there is no plot mapping.

- data:

  The data to be displayed in this layer. In addition to the three
  options described in
  [ggplot2::geom_raster](https://ggplot2.tidyverse.org/reference/geom_tile.html),
  there are two additional methods:

  If a `SpatRaster` object (see
  [terra::rast](https://rspatial.github.io/terra/reference/rast.html)),
  this function will coerce the raster to a data frame and assume the
  raster bands are in RGB order (while allowing for, but ignoring, a
  fourth alpha band).

  If a length-1 character vector, this function will attempt to load the
  object via
  [terra::rast](https://rspatial.github.io/terra/reference/rast.html).

- stat:

  The statistical transformation to use on the data for this layer. When
  using a `geom_*()` function to construct a layer, the `stat` argument
  can be used the override the default coupling between geoms and stats.
  The `stat` argument accepts the following:

  - A `Stat` ggproto subclass, for example `StatCount`.

  - A string naming the stat. To give the stat as a string, strip the
    function name of the `stat_` prefix. For example, to use
    [`stat_count()`](https://ggplot2.tidyverse.org/reference/geom_bar.html),
    give the stat as `"count"`.

  - For more information and other ways to specify the stat, see the
    [layer
    stat](https://ggplot2.tidyverse.org/reference/layer_stats.html)
    documentation.

- position:

  A position adjustment to use on the data for this layer. This can be
  used in various ways, including to prevent overplotting and improving
  the display. The `position` argument accepts the following:

  - The result of calling a position function, such as
    [`position_jitter()`](https://ggplot2.tidyverse.org/reference/position_jitter.html).
    This method allows for passing extra arguments to the position.

  - A string naming the position adjustment. To give the position as a
    string, strip the function name of the `position_` prefix. For
    example, to use
    [`position_jitter()`](https://ggplot2.tidyverse.org/reference/position_jitter.html),
    give the position as `"jitter"`.

  - For more information and other ways to specify the position, see the
    [layer
    position](https://ggplot2.tidyverse.org/reference/layer_positions.html)
    documentation.

- ...:

  Other arguments passed on to
  [`layer()`](https://ggplot2.tidyverse.org/reference/layer.html)'s
  `params` argument. These arguments broadly fall into one of 4
  categories below. Notably, further arguments to the `position`
  argument, or aesthetics that are required can *not* be passed through
  `...`. Unknown arguments that are not part of the 4 categories below
  are ignored.

  - Static aesthetics that are not mapped to a scale, but are at a fixed
    value and apply to the layer as a whole. For example,
    `colour = "red"` or `linewidth = 3`. The geom's documentation has an
    **Aesthetics** section that lists the available options. The
    'required' aesthetics cannot be passed on to the `params`. Please
    note that while passing unmapped aesthetics as vectors is
    technically possible, the order and required length is not
    guaranteed to be parallel to the input data.

  - When constructing a layer using a `stat_*()` function, the `...`
    argument can be used to pass on parameters to the `geom` part of the
    layer. An example of this is
    `stat_density(geom = "area", outline.type = "both")`. The geom's
    documentation lists which parameters it can accept.

  - Inversely, when constructing a layer using a `geom_*()` function,
    the `...` argument can be used to pass on parameters to the `stat`
    part of the layer. An example of this is
    `geom_area(stat = "density", adjust = 0.5)`. The stat's
    documentation lists which parameters it can accept.

  - The `key_glyph` argument of
    [`layer()`](https://ggplot2.tidyverse.org/reference/layer.html) may
    also be passed on through `...`. This can be one of the functions
    described as [key
    glyphs](https://ggplot2.tidyverse.org/reference/draw_key.html), to
    change the display of the layer in the legend.

- hjust, vjust:

  horizontal and vertical justification of the grob. Each justification
  value should be a number between 0 and 1. Defaults to 0.5 for both,
  centering each pixel over its data location.

- interpolate:

  If `TRUE` interpolate linearly, if `FALSE` (the default) don't
  interpolate.

- na.rm:

  If `FALSE`, the default, missing values are removed with a warning. If
  `TRUE`, missing values are silently removed.

- show.legend:

  logical. Should this layer be included in the legends? `NA`, the
  default, includes if any aesthetics are mapped. `FALSE` never
  includes, and `TRUE` always includes. It can also be a named logical
  vector to finely select the aesthetics to display.

- inherit.aes:

  If `FALSE`, overrides the default aesthetics, rather than combining
  with them. This is most useful for helper functions that define both
  data and aesthetics and shouldn't inherit behaviour from the default
  plot specification, e.g.
  [`borders()`](https://ggplot2.tidyverse.org/reference/annotation_borders.html).

- scale:

  Integer. Maximum (possible) value in the three channels. If `NULL`,
  attempts to infer proper values from data – if all RGB values are \<=
  1 then 1, \<= 255 then 255, and otherwise 65535.

- geom:

  The geometric object to use to display the data for this layer. When
  using a `stat_*()` function to construct a layer, the `geom` argument
  can be used to override the default coupling between stats and geoms.
  The `geom` argument accepts the following:

  - A `Geom` ggproto subclass, for example `GeomPoint`.

  - A string naming the geom. To give the geom as a string, strip the
    function name of the `geom_` prefix. For example, to use
    [`geom_point()`](https://ggplot2.tidyverse.org/reference/geom_point.html),
    give the geom as `"point"`.

  - For more information and other ways to specify the geom, see the
    [layer
    geom](https://ggplot2.tidyverse.org/reference/layer_geoms.html)
    documentation.

## See also

Other visualization functions:
[`combine_overlays()`](https://docs.ropensci.org/terrainr/reference/combine_overlays.md),
[`raster_to_raw_tiles()`](https://docs.ropensci.org/terrainr/reference/raster_to_raw_tiles.md),
[`vector_to_overlay()`](https://docs.ropensci.org/terrainr/reference/vector_to_overlay.md)

## Examples

``` r
if (FALSE) { # \dontrun{

simulated_data <- data.frame(
  id = seq(1, 100, 1),
  lat = runif(100, 44.04905, 44.17609),
  lng = runif(100, -74.01188, -73.83493)
)

simulated_data <- sf::st_as_sf(simulated_data, coords = c("lng", "lat"))
simulated_data <- sf::st_set_crs(simulated_data, 4326)

output_tiles <- get_tiles(simulated_data,
  services = c("ortho"),
  resolution = 120
)

merged_ortho <- tempfile(fileext = ".tif")
merge_rasters(output_tiles[["ortho"]], merged_ortho)

merged_stack <- terra::rast(merged_ortho)

library(ggplot2)

ggplot() +
  geom_spatial_rgb(
    data = merged_ortho,
    mapping = aes(
      x = x,
      y = y,
      r = red,
      g = green,
      b = blue
    )
  ) +
  geom_sf(data = simulated_data) +
  coord_sf(crs = 4326)

ggplot() +
  geom_spatial_rgb(
    data = merged_stack,
    mapping = aes(
      x = x,
      y = y,
      r = red,
      g = green,
      b = blue
    )
  ) +
  geom_sf(data = simulated_data) +
  coord_sf(crs = 4326)
} # }
```
