# Plan a cross between named parents

For any pair of parents in a \[hbr_advanced_decision()\] result — not
only the top-ranked crosses — reports which haplotype blocks are fixed,
segregating, split between the parents (a recombinant is needed) or
missing, the exact probability that a doubled-haploid progeny carries
every segregating target haplotype, the F2 probabilities, and the number
of plants needed to recover at least one carrier with the requested
confidence.

## Usage

``` r
hbr_cross_plan(
  x,
  parent_a,
  parent_b = NULL,
  mating = c("DH", "RIL"),
  conf = 0.95
)
```

## Arguments

- x:

  A result of \[hbr_advanced_decision()\] that was run with a genetic
  map (so \`x\$target\` is populated).

- parent_a:

  Line IDs. When \`parent_b\` is \`NULL\`, all pairs among \`parent_a\`
  are planned.

- parent_b:

  Optional line IDs, same length as \`parent_a\`.

- mating:

  \`"DH"\` or \`"RIL"\` (RIL by selfing) for the linked probability.

- conf:

  Confidence for the number of plants. Default \`0.95\`.

## Value

A data.frame with one row per cross, columns \`parent_a\`, \`parent_b\`,
\`mid_index\`, \`n_blocks_fixed\`, \`n_blocks_segregating\`,
\`n_blocks_split\`, \`n_blocks_incomplete\`, \`n_blocks_covered\`,
\`n_blocks_target\`, \`p_pyramid_DH\` or \`p_pyramid_RIL\`,
\`p_pyramid_F2_hom\`, \`plants_needed\`, and, when available,
\`sd_index\` and \`uc\`.

## Details

The DH probability is computed at the gene level with Haldane's map
function, so linkage in coupling or repulsion enters exactly. F2
probabilities ignore linkage and count one locus per segregating block
or per differing gene of a split block. Plant numbers solve \`1 - (1 -
p)^N \>= conf\` (Sedcole 1977). The mid-parent index uses the result's
multi-trait index (larger is better in the pipeline's direction).
Usefulness and progeny SD are reported only for pairs that were computed
in the result.

## See also

\[hbr_advanced_decision()\], \[hbr_pyramid_probability()\],
\[hbr_population_size()\].

## Examples

``` r
# A minimal hgsi_advanced stub, sufficient for planning only
res <- structure(list(
  ids    = c("A", "B", "C"),
  index  = c(1.0, 0.8, 0.6),
  crosses = data.frame(parent_a = "A", parent_b = "B",
                       uc = 1.5, sd_index = 0.4),
  target = list(
    carry = matrix(c(TRUE, FALSE, TRUE, FALSE, TRUE, TRUE),
                   nrow = 3, ncol = 2,
                   dimnames = list(c("A", "B", "C"),
                                   c("GENE01", "GENE02"))),
    block = c(1L, 1L),
    units = data.frame(gene = c("GENE01", "GENE02"),
                       chr  = c("1", "1"),
                       cm   = c(10, 10.5),
                       stringsAsFactors = FALSE))),
  class = "hgsi_advanced")
hbr_cross_plan(res, "A", "B")
#>                parent_a parent_b mid_index n_blocks_fixed n_blocks_segregating
#> n_blocks_fixed        A        B       0.9              0                    0
#>                n_blocks_split n_blocks_incomplete n_blocks_covered
#> n_blocks_fixed              1                   0                1
#>                n_blocks_target p_pyramid_DH p_pyramid_F2_hom plants_needed
#> n_blocks_fixed               1  0.002487542           0.0625          1203
#>                sd_index  uc
#> n_blocks_fixed      0.4 1.5
hbr_cross_plan(res, c("A", "B"), c("B", "C"))
#>   parent_a parent_b mid_index n_blocks_fixed n_blocks_segregating
#> 1        A        B       0.9              0                    0
#> 2        B        C       0.7              0                    1
#>   n_blocks_split n_blocks_incomplete n_blocks_covered n_blocks_target
#> 1              1                   0                1               1
#> 2              0                   0                1               1
#>   p_pyramid_DH p_pyramid_F2_hom plants_needed sd_index  uc
#> 1  0.002487542           0.0625          1203      0.4 1.5
#> 2  0.500000000           0.2500             5       NA  NA
```
