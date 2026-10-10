# Return \`n\` colours from a named palette

Return \`n\` colours from a named palette

## Usage

``` r
hbr_palette(name = "haplobreed", n = NULL)
```

## Arguments

- name:

  Palette name. See \[hbr_palette_names()\].

- n:

  Number of colours. If \`NULL\`, returns the whole palette. If \`n \>
  length(palette)\`, the palette is interpolated.

## Value

Character vector of hex colours.

## Examples

``` r
hbr_palette("okabe_ito", n = 4)
#> [1] "#E69F00" "#56B4E9" "#009E73" "#F0E442"
hbr_palette("haplobreed")
#> [1] "#D55E00" "#0072B2" "#009E73" "#CC79A7" "#F0E442" "#56B4E9" "#E69F00"
#> [8] "#999999"
```
