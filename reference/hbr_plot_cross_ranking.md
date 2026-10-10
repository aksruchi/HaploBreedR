# Plot cross ranking by usefulness vs mid-parent index

Visualises how the ranking of recommended crosses changes when progeny
variance is accounted for. Each point is one cross; the x-axis is the
rank by mid-parent index alone, the y-axis is the rank by usefulness
(Schnell and Utz, 1975). Points on the diagonal are crosses whose
recommendation is identical under the two criteria; points off the
diagonal are crosses whose rank depends on progeny variance. The most
displaced cross is optionally highlighted and labelled.

## Usage

``` r
hbr_plot_cross_ranking(
  x,
  top_n = 20L,
  highlight = c("auto"),
  label_size = 3,
  palette = "haplobreed",
  theme = "haplobreed",
  output_dir = NULL,
  file_name = "cross_ranking",
  width = 6,
  height = 6,
  formats = c("pdf", "png"),
  verbose = TRUE
)
```

## Arguments

- x:

  Either an \`hgsi_advanced\` object (from \[hbr_advanced_decision()\])
  or a data.frame with columns \`parent_a\`, \`parent_b\`,
  \`mid_index\`, and \`uc\`.

- top_n:

  Number of top crosses to display. Crosses are ordered by \`uc\`.
  Default \`20L\`.

- highlight:

  A cross to annotate. Either a length-2 character vector \`c(parent_a,
  parent_b)\`, or \`"auto"\` to highlight the cross with the largest
  absolute rank displacement (default).

- label_size:

  Text size for the highlight label.

- palette:

  One of \[hbr_palette_names()\].

- theme:

  One of \[hbr_theme_names()\].

- output_dir:

  Directory for the figure. \`NULL\` returns the plot without writing
  anything.

- file_name:

  Base name for the output file (without extension).

- width, height:

  Figure dimensions in inches.

- formats:

  Character vector of output formats. Any of \`"pdf"\`, \`"png"\`,
  \`"tiff"\`, \`"svg"\`.

- verbose:

  Print progress.

## Value

Invisibly, a list with \`plot\` (the ggplot object) and \`files\` (the
paths written, or \`character(0)\` if \`output_dir\` is \`NULL\`). The
\`plot\` element can be assigned and modified further with ggplot2.

## Details

Use this to document that the genetic map is doing real work in the
cross-design step, or to justify why a cross with a lower mid-parent
index is nonetheless recommended.

## Examples

``` r
toy <- system.file("extdata", "toy", package = "HaploBreedR")
crosses <- data.frame(
  parent_a  = sprintf("IRIS_%04d", 1:20),
  parent_b  = sprintf("IRIS_%04d", 21:40),
  mid_index = runif(20, 5, 12),
  uc        = runif(20, 5, 15))
hbr_plot_cross_ranking(crosses, top_n = 20)
#>   19 of 20 top crosses reordered (max |shift| = 17)
```
