# Generate a unified input-QC report

Runs the three input-QC checks — sequence-resource QC
(\[hbr_validate_sequence_resources()\]), genotype-reference
compatibility (\[hbr_validate_genotype_reference()\]), and ID overlap
(\[hbr_validate_individual_ids()\], when phenotypes are supplied) — and
prints a single consolidated report. Optionally writes a plain- text
file and/or a full report set (TXT + three CSV tables) to \`out_dir\`.
Only the TXT and CSV files are written: the HTML duplicate was removed.

## Usage

``` r
hbr_generate_input_qc_report(
  reference,
  genotype,
  phenotype_data = NULL,
  pheno_id_col = "ID",
  out_file = NULL,
  out_dir = NULL,
  ...
)
```

## Arguments

- reference:

  A \`hbr_reference\` object.

- genotype:

  A \`hbr_genotype\` object.

- phenotype_data:

  Optional phenotype table.

- pheno_id_col:

  ID column in \`phenotype_data\`.

- out_file:

  Optional single text file path.

- out_dir:

  Optional directory for the full report set.

- ...:

  Passed to \[hbr_validate_genotype_reference()\].

## Value

Invisibly, a list with \`sequence_qc\`, \`compatibility\`,
\`id_report\`, \`overall_status\`, and \`files\`.

## Examples

``` r
if (interactive()) {
  toy <- system.file("extdata", "toy", package = "HaploBreedR")
  # A complete call needs an hbr_reference and hbr_genotype; see the
  # vignette for the construction used here.
}
```
