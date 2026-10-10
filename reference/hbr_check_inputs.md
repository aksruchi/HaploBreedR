# Pre-flight Validation of Inputs

Validates PLINK files, phenotype records, GFF3 features, and sample ID
overlap before launching intensive discovery pipelines.

## Usage

``` r
hbr_check_inputs(
  plink_prefix,
  phenotype_data,
  trait_col,
  pheno_id_col = "ID",
  gff3 = NULL
)
```

## Arguments

- plink_prefix:

  Character. PLINK binary prefix.

- phenotype_data:

  data.frame of phenotypes.

- trait_col:

  Character. Target trait column name.

- pheno_id_col:

  Character. Individual ID column in phenotype_data.

- gff3:

  Optional path to GFF3 file.

## Value

A list of class `hbr_check` detailing compatibility status.

## Examples

``` r
if (interactive()) {
  pheno <- data.frame(ID = sprintf("IND%02d", 1:10), trait = rnorm(10))
  toy   <- system.file("extdata", "toy", package = "HaploBreedR")
  res   <- hbr_check_inputs(
    plink_prefix   = file.path(toy, "toy"),
    phenotype_data = pheno,
    trait_col      = "trait")
}
```
