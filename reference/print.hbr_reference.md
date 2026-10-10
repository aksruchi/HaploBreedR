# Print an hbr_reference object

Print an hbr_reference object

## Usage

``` r
# S3 method for class 'hbr_reference'
print(x, ...)
```

## Arguments

- x:

  An object of class \`hbr_reference\`.

- ...:

  Ignored.

## Value

\`x\`, invisibly.

## Examples

``` r
ref <- structure(
  list(genome = "TOY", annotation = "CUSTOM",
       genes       = data.frame(gene_id = "g1"),
       transcripts = data.frame(gene_id = "g1",
                                transcript_id = "g1.1"),
       has_cds = FALSE, has_pep = FALSE, has_genome_fasta = FALSE,
       validation = list(status = "PASS")),
  class = "hbr_reference")
print(ref)
#> <hbr_reference> TOY / CUSTOM 
#>   Genes: 1  Transcripts: 1 
#>   CDS available: FALSE  PEP available: FALSE  Genome FASTA available: FALSE 
#>   Sequence-resource QC: PASS 
```
