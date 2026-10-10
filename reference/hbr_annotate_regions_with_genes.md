# Annotate LD regions with genes

Overlaps a set of LD regions with a gene table and labels each
region-gene pair with a \`Gene_Relationship\` (\`GENE_CONTAINED\`,
\`OVERLAPS_LEFT\`, \`OVERLAPS_RIGHT\`, \`CONTAINS_REGION\`, or
\`OVERLAPS\`). Region list columns (e.g. \`GWAS_SNPs\`) are preserved
through the overlap. When \`keep_intergenic = TRUE\`, regions with no
overlapping gene are retained as \`INTERGENIC\`.

## Usage

``` r
hbr_annotate_regions_with_genes(
  regions,
  genes,
  chr_col = "Chromosome",
  start_col = "Region_Start",
  end_col = "Region_End",
  keep_intergenic = TRUE,
  verbose = TRUE
)
```

## Arguments

- regions:

  A \`data.table\` of LD regions.

- genes:

  Gene table with ID, chromosome, start, end, and strand columns (column
  names auto-detected).

- chr_col, start_col, end_col:

  Region coordinate column names.

- keep_intergenic:

  Keep regions with no overlapping gene.

- verbose:

  Print progress.

## Value

A \`data.table\` of region-gene overlaps, or \`NULL\`.

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
