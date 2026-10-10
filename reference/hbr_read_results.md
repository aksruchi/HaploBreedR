# Read HaploBreedR Pipeline Results from Disk

Ingests completed single-trait or multi-trait pipeline output
directories into memory as classed objects for visualization or genomic
selection.

## Usage

``` r
hbr_read_results(path = NULL, traits = NULL)
```

## Arguments

- path:

  Character. Path to a single trait output directory.

- traits:

  Optional named character vector of output directories for multi-trait
  loading.

## Value

An object of class `hbr_run` (single trait) or `hbr_run_list`
(multi-trait).

## Examples

``` r
toy <- system.file("extdata", "test_data", package = "HaploBreedR")
if (nzchar(toy) && dir.exists(toy)) {
  res <- try(hbr_read_results(path = toy))
}
```
