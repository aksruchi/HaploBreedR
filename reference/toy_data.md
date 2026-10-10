# Tiny demonstration dataset for HaploBreedR

A minimal toy dataset shipped with the package so that examples, tests,
and the vignette can run without network access. It is not biologically
meaningful; it is sized only to exercise the code paths.

## Format

Files under \`inst/extdata/toy/\`. See \`inst/scripts/make_toy_data.R\`
for the generation script.

## Source

Simulated.

## Value

\`NULL\`, invisibly. The object is documentation-only; the files are
read with \`system.file("extdata", "toy", package = "HaploBreedR")\`.

## Details

Files live in \`system.file("extdata", "toy", package =
"HaploBreedR")\`:

- toy.raw, toy.bim, toy.fam:

  PLINK binary input for 10 individuals and 50 SNPs on one chromosome.

- toy_pheno.csv:

  Two columns, \`ID\` and \`trait\` (a continuous response).

- toy_gwas.csv:

  Three GWAS hits on chromosome 1.

- toy.gff3:

  A three-kilobase mock gene model with one transcript, CDS, and
  5'-/3'-UTRs.

- toy.fa:

  A placeholder genome FASTA to satisfy the reference validator.
