# Haplotype block table from a set of target loci

Runs \[hbr_haplotype_blocks()\] and returns the block summary table
alongside the per-locus assignment. The table has one row per block with
the block id, chromosome, start and end position in cM, the number of
target loci in the block, the number of distinct genes (when \`units\`
has a \`gene\` column) and the concatenated gene and trait names.

## Usage

``` r
hbr_haplotype_block_table(
  plink_prefix = NULL,
  units,
  cm_snp = NULL,
  chr_snp = NULL,
  traits = NULL,
  method = c("recomb", "ld", "either", "fourgamete", "gabriel", "recomb+gabriel",
    "recomb+fourgamete"),
  flank_cM = 1,
  max_snps = 400L,
  max_span_cM = 5,
  min_gamete = 0.01,
  maf_min = 0.05,
  rmax = 0.01,
  r2 = 0.5,
  ld_max_cM = 3,
  r2_min = 0.25,
  gabriel_grid = 21L,
  carry = NULL
)
```

## Arguments

- plink_prefix:

  PLINK prefix, or an \`hbr_run\` object (in which case the run-level
  API is used). When the first positional argument is an \`hbr_run\`,
  this argument receives it.

- units:

  Low-level API: data.frame with \`chr\` and \`cm\` per target locus,
  and \`snp_col\` when using the SNP-level methods. Alternatively, an
  \`hbr_run\` object (in which case the run-level API is used).

- cm_snp, chr_snp:

  Low-level API: genetic positions and chromosomes of every SNP in the
  PLINK file.

- traits:

  Optional character vector (one per row of \`units\`) of the trait(s)
  each locus belongs to. When \`units\` already carries a \`traits\`
  column, that is used instead.

- method:

  One of the seven methods above.

- flank_cM, max_snps, min_gamete:

  SNP-level methods only: window around the genes, SNPs kept per
  cluster, and gamete frequency that counts as recombination.

- max_span_cM:

  Largest distance between the first and last locus of a block.

- maf_min:

  Minimum minor-allele frequency.

- rmax:

  Maximum Haldane recombination fraction between neighbours for
  \`"recomb"\`.

- r2:

  Minimum carrier-indicator r-squared for \`"ld"\`.

- ld_max_cM:

  Largest distance over which LD may join neighbours.

- r2_min, gabriel_grid, carry:

  Reserved for future versions; kept for backward compatibility with the
  low-level API.

## Value

A list with \`blocks\` (the summary table) and \`assignment\` (the block
id per target locus, in the same order as \`units\`).

## Examples

``` r
units <- data.frame(chr = c("1", "1", "1"),
                    cm  = c(10, 10.5, 11),
                    gene = c("g1", "g2", "g3"))
hbr_haplotype_block_table(method = "recomb", units = units)
#> $blocks
#>   block chr start_cM end_cM n_target_haplotypes n_genes    genes traits
#> 1 HB001   1       10     11                   3       3 g1;g2;g3     NA
#>   panel_freq
#> 1         NA
#> 
#> $assignment
#> [1] 1 1 1
#> 
```
