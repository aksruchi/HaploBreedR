# Parse gene features from a GFF3 into a data.table

Reads a GFF3 file, extracts \`gene\`-type features, decodes the
\`ID\`/\`gene_id\`/\`locus_tag\`, \`Name\`, and
\`Note\`/\`description\`/ \`product\` attributes, standardizes
chromosome names via \[hbr_standardize_chr()\], and returns a
deduplicated gene table.

## Usage

``` r
hbr_read_gff3_genes(gff3, verbose = TRUE)
```

## Arguments

- gff3:

  Path to a GFF3 file.

- verbose:

  Print progress.

## Value

A \`data.table\` with \`Gene_ID\`, \`Gene_Name\`, \`Gene_Function\`,
\`Gene_Chromosome\`, \`Gene_Start\`, \`Gene_End\`, \`Gene_Strand\`.
Empty if no gene features are present.

## Examples

``` r
regions <- data.table::data.table(
  LD_Region_ID = "R1",
  Chromosome   = "1",
  Region_Start = 1000L,
  Region_End   = 3000L)
genes <- data.table::data.table(
  Gene_ID         = "gene1",
  Gene_Chromosome = "1",
  Gene_Start      = 1000L,
  Gene_End        = 2500L,
  Gene_Strand     = "+")
hbr_annotate_regions_with_genes(regions, genes, verbose = FALSE)
#>    LD_Region_ID Chromosome Region_Start Region_End Gene_ID Gene_Name
#>          <char>     <char>        <int>      <int>  <char>    <char>
#> 1:           R1          1         1000       3000   gene1     gene1
#>    Gene_Function Gene_Chromosome Gene_Start Gene_End Gene_Strand
#>           <char>          <char>      <int>    <int>      <char>
#> 1:          <NA>               1       1000     2500           +
#>    Gene_Relationship Annotation_Status
#>               <char>            <char>
#> 1:    GENE_CONTAINED         Annotated
```
