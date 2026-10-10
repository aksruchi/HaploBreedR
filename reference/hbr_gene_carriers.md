# Carrier status of the superior haplotype at a gene

Reads the per-gene \`\<gene\>\_individuals.csv\` written by
\[haplobreed_analysis()\] and returns, for every individual in the HGSI
result, whether they carry the pipeline's superior haplotype at that
gene. Used to colour per-individual figures by carrier status.

## Usage

``` r
hbr_gene_carriers(x, trait, gene, trait_dir = NULL, superior_haplotype = NULL)
```

## Arguments

- x:

  An \`hgsi_advanced\` object.

- trait:

  Trait label.

- gene:

  Gene ID.

- trait_dir:

  Path to the trait's pipeline output directory. If \`NULL\`, the helper
  looks in \`x\$trait_dirs\[\[trait\]\]\`.

- superior_haplotype:

  Optional. When \`NULL\` (default), the helper reads it from
  \`superior_genes_summary.csv\` in \`trait_dir\`.

## Value

A list with \`carrier\` (logical, length \`length(x\$ids)\`),
\`haplotype\` (character, the assigned haplotype per individual),
\`superior_haplotype\` (character), and \`gene\` and \`trait\`.

## Examples

``` r
toy <- system.file("extdata", "hgsi_toy", package = "HaploBreedR")
td  <- file.path(toy, "trait_YLD")
if (nzchar(toy) && dir.exists(td)) {
  x <- structure(
    list(ids = sprintf("L%03d", 1:150),
         traits = "YLD",
         trait_dirs = c(YLD = td)),
    class = "hgsi_advanced")
  res <- try(hbr_gene_carriers(
    x, trait = "YLD", gene = "GENE04", trait_dir = td))
}
#> Error : Could not determine superior_haplotype for gene 'GENE04'. Pass it explicitly.
```
