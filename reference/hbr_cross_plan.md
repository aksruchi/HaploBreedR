# Interactive Cross Query Planning

Evaluates target haplotype block coverage, pyramiding probabilities, and
population sizing requirements for a specific user-named cross
combination.

## Usage

``` r
hbr_cross_plan(decision_obj, parent_a, parent_b, mating = c("DH", "RIL"))
```

## Arguments

- decision_obj:

  An `hgsi_advanced` object from \[hbr_advanced_decision()\].

- parent_a:

  Character. ID of the first parent.

- parent_b:

  Character. ID of the second parent.

- mating:

  Character. "DH" (Doubled Haploids) or "RIL" (Recombinant Inbred
  Lines).

## Value

A list detailing block states, DH/RIL pyramiding probabilities, and
Sedcole (1977) N95 plant population requirements.

## Examples

``` r
dec <- structure(
  list(ids = c("A", "B"),
       blocks = data.frame(block = "HB001", chr = "1",
                           start_cM = 10, end_cM = 12)),
  class = "hgsi_advanced")
hbr_cross_plan(dec, "A", "B")
#> $parent_a
#> [1] "A"
#> 
#> $parent_b
#> [1] "B"
#> 
#> $mating
#> [1] "DH"
#> 
#> $blocks
#>   block chr start_cM end_cM
#> 1 HB001   1       10     12
#> 
```
