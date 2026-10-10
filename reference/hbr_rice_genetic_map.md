# Bundled rice genetic map anchors

Returns the Nagamura et al. (1997) rice linkage-map anchors (n ~ 1,450
RFLP markers with both physical and genetic positions; total map length
1,510 cM) that ship with the package. The engine interpolates these
anchors onto the physical positions of any PLINK \`.bim\` at run time,
so the same table is valid for any rice panel. Use the result as the
\`genetic_map\` argument of \[hbr_advanced_decision()\] when you want to
inspect it, subset it, or combine it with additional markers.

## Usage

``` r
hbr_rice_genetic_map()
```

## Value

A data.frame with columns \`chr\` (character), \`bp\` (numeric,
IRGSP-1.0 coordinates) and \`cm\` (numeric, Haldane/Kosambi-agnostic;
the engine uses Haldane's map function). The \`source\` attribute
records the reference and marker count.

## Examples

``` r
m <- hbr_rice_genetic_map()
head(m)
#>   chr        bp  cm
#> 1   1  148326.5 0.0
#> 2   1  198225.0 0.3
#> 3   1  577032.0 4.2
#> 4   1  649078.5 5.6
#> 5   1  921354.0 5.6
#> 6   1 1010335.0 5.6
attr(m, "source")
#> [1] "bundled rice genetic map (Nagamura et al. 1997, n = 1659 markers)"
```
