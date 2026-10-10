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

  Character. PLINK file prefix. Required by the SNP-level methods
  (\`"fourgamete"\`, \`"gabriel"\`) and their combinations; ignored
  otherwise.

- units:

  Data.frame with columns \`chr\` and \`cm\`, and optionally \`snp_col\`
  (PLINK column index of the locus's own SNP, needed by \`"fourgamete"\`
  and \`"gabriel"\`).

- cm_snp:

  Numeric vector of genetic positions per SNP in the PLINK file.
  Required by the SNP-level methods.

- chr_snp:

  Character vector of chromosomes per SNP in the PLINK file. Required by
  the SNP-level methods.

- traits:

  Optional character vector (one per row of \`units\`) of the trait(s)
  each locus belongs to. When \`units\` already carries a \`traits\`
  column, that is used instead.

- method:

  Block method, one of \`"recomb"\`, \`"ld"\`, \`"either"\`,
  \`"fourgamete"\`, \`"gabriel"\`, \`"recomb+gabriel"\`,
  \`"recomb+fourgamete"\`.

- flank_cM:

  Numeric. Window (+/- cM) around each cluster of target loci from which
  SNPs are read, for SNP-level methods.

- max_snps:

  Integer. Maximum SNPs per cluster after thinning.

- max_span_cM:

  Numeric. Largest distance between the first and last locus of a block
  (cM). Chaining cannot build blocks longer than this.

- min_gamete:

  Numeric. Four-gamete frequency that counts as evidence of
  recombination (Haploview default 0.01).

- maf_min:

  Numeric. Minimum minor allele frequency for a SNP to enter the block
  search.

- rmax:

  Numeric. Maximum recombination fraction between neighbouring loci for
  \`"recomb"\` and \`"either"\` (default 0.01, about 1 cM).

- r2:

  Numeric. Minimum r^2 of carrier indicators to join neighbours under
  \`"ld"\` and \`"either"\`.

- ld_max_cM:

  Numeric. Largest distance over which LD may join neighbours (cM).

- r2_min:

  Numeric. Reserved for a future version; currently not wired into the
  SNP-level block callers (the four-gamete rule and the full Gabriel D'
  test are applied directly to every pair).

- gabriel_grid:

  Integer. Reserved for a future version; currently not wired into the
  SNP-level block callers.

- carry:

  Logical matrix individuals x target loci. Required by \`"ld"\` and
  \`"either"\`; ignored otherwise.

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
