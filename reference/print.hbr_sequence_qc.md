# Print a sequence-resource QC report

Print a sequence-resource QC report

## Usage

``` r
# S3 method for class 'hbr_sequence_qc'
print(x, ...)
```

## Arguments

- x:

  An object of class \`hbr_sequence_qc\`.

- ...:

  Ignored.

## Value

\`x\`, invisibly.

## Examples

``` r
x <- structure(
  list(status = "PASS",
       summary = data.table::data.table(
         GFF3_transcripts = 0L, CDS_sequences = 0L,
         PEP_sequences = 0L, Complete_CDS_PEP = 0L,
         CDS_only = 0L, PEP_only = 0L,
         Translation_mismatch = 0L, Invalid_CDS_length = 0L)),
  class = "hbr_sequence_qc")
print(x)
#> SEQUENCE RESOURCE QC
#> ====================
#> 
#> GFF3 transcripts       : 0
#> CDS sequences          : 0
#> PEP sequences          : 0
#> 
#> Complete CDS+PEP       : 0
#> CDS only               : 0
#> PEP only               : 0
#> Translation mismatch   : 0
#> Invalid CDS length     : 0
#> 
#> STATUS: PASS 
```
