# Package index

## Data Retrieval Functions

- [`get_tiles()`](https://docs.ropensci.org/terrainr/reference/get_tiles.md)
  : A user-friendly way to get USGS National Map data tiles for an area
- [`hit_national_map_api()`](https://docs.ropensci.org/terrainr/reference/hit_national_map_api.md)
  : Hit the USGS 3DEP API and retrieve an elevation heightmap

## Data Manipulation Functions

- [`merge_rasters()`](https://docs.ropensci.org/terrainr/reference/merge_rasters.md)
  : Merge multiple raster files into a single raster
- [`georeference_overlay()`](https://docs.ropensci.org/terrainr/reference/georeference_overlay.md)
  : Georeference image overlays based on a reference raster

## Visualization Functions

- [`geom_spatial_rgb()`](https://docs.ropensci.org/terrainr/reference/geom_spatial_rgb.md)
  [`stat_spatial_rgb()`](https://docs.ropensci.org/terrainr/reference/geom_spatial_rgb.md)
  : Plot RGB rasters in ggplot2
- [`raster_to_raw_tiles()`](https://docs.ropensci.org/terrainr/reference/raster_to_raw_tiles.md)
  : Crop a raster and convert the output tiles into new formats.
- [`make_manifest()`](https://docs.ropensci.org/terrainr/reference/unity_crops.md)
  [`transform_elevation()`](https://docs.ropensci.org/terrainr/reference/unity_crops.md)
  [`transform_overlay()`](https://docs.ropensci.org/terrainr/reference/unity_crops.md)
  : Transform rasters and write manifest file for import into Unity
- [`make_unity()`](https://docs.ropensci.org/terrainr/reference/make_unity.md)
  : Initialize terrain inside of a Unity project.
- [`vector_to_overlay()`](https://docs.ropensci.org/terrainr/reference/vector_to_overlay.md)
  : Turn spatial vector data into an image overlay
- [`combine_overlays()`](https://docs.ropensci.org/terrainr/reference/combine_overlays.md)
  : Combine multiple image overlays into a single file

## Utility Functions

- [`add_bbox_buffer()`](https://docs.ropensci.org/terrainr/reference/addbuff.md)
  [`set_bbox_side_length()`](https://docs.ropensci.org/terrainr/reference/addbuff.md)
  : Add a uniform buffer around a bounding box for geographic
  coordinates
