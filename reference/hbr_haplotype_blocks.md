# Standalone Haplotype Block Calling

Partitions a set of target loci into haplotype blocks by any of the
methods the pipeline uses: map-based recombination between the loci
(\`"recomb"\`), LD between their carrier indicators (\`"ld"\`), the
union of both (\`"either"\`), SNP-level methods around each target
cluster (\`"fourgamete"\`, \`"gabriel"\`), or the union of a map method
and an SNP method (\`"recomb+gabriel"\`, \`"recomb+fourgamete"\`).
Blocks never span chromosomes and never exceed \`max_span_cM\`.

## Usage

``` r
hbr_haplotype_blocks(
  plink_prefix = NULL,
  units,
  cm_snp = NULL,
  chr_snp = NULL,
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

Integer vector of block IDs per target locus, with attribute
\`"clusters"\` giving the SNP windows used by SNP-level methods (or
\`NULL\`).

## Examples

``` r
units <- data.frame(chr = c("1", "1", "1", "2", "2"),
                    cm  = c(10, 10.5, 50, 5, 5.2))
hbr_haplotype_blocks(method = "recomb", units = units)
#> [1] 1 1 2 3 3
```
