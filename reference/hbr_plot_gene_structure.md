# Plot gene structure for one or more genes

Draws UTRs, exons, intron chevrons (strand-aware), and optional
functional-variant markers for one or more genes. When \`facet_rows =
FALSE\` and more than one gene is requested, a combined- axis facet
figure is also written.

## Usage

``` r
hbr_plot_gene_structure(
  gene_list,
  reference = NULL,
  gff3_path = NULL,
  annotation_source = c("MSU7", "RAPDB", "CUSTOM"),
  cdna_path = NULL,
  cds_path = NULL,
  pep_path = NULL,
  genome_fasta_path = NULL,
  output_dir = NULL,
  figures_dir = "figures",
  n_gene = NULL,
  sort_by = c("Cohens_d", "Superior_Mean"),
  fun_variants = NULL,
  variant_panel_dir = NULL,
  show_variants = TRUE,
  variant_shape_by_region = TRUE,
  aa_full_names = TRUE,
  facet_rows = TRUE,
  palette = "haplobreed",
  theme = "scientific",
  width = 10,
  height = 4,
  formats = c("pdf", "png"),
  combined_pdf = TRUE,
  verbose = TRUE
)
```

## Arguments

- gene_list:

  Gene IDs, path to a summary CSV, directory, or data.frame.

- reference:

  A \`hbr_reference\` object.

- gff3_path:

  Path to a GFF3 file. Parsed once and cached.

- annotation_source:

  \`"MSU7"\`, \`"RAPDB"\`, or \`"CUSTOM"\`.

- cdna_path, cds_path, pep_path, genome_fasta_path:

  Optional FASTA paths.

- output_dir:

  Directory for figures.

- figures_dir:

  Subdirectory of \`output_dir\`.

- n_gene:

  Keep at most this many genes.

- sort_by:

  Character vector of columns to rank by.

- fun_variants:

  Optional named list or data.frame.

- variant_panel_dir:

  Directory with per-gene functional SNP files.

- show_variants:

  Draw functional-variant markers.

- variant_shape_by_region:

  Shape by region.

- aa_full_names:

  Expand \`R65G\` to \`Arg65Gly\`.

- facet_rows:

  One gene per row or all on a single axis.

- palette:

  One of \[hbr_palette_names()\].

- theme:

  One of \[hbr_theme_names()\].

- width, height:

  Figure dimensions in inches.

- formats:

  Output formats.

- combined_pdf:

  Also write a multi-page PDF.

- verbose:

  Print progress.

## Value

Invisibly, a list with \`plots\`, \`files\`, \`combined_pdf\`,
\`missing_genes\`.

## Examples

``` r
toy <- system.file("extdata", "toy", package = "HaploBreedR")
hbr_plot_gene_structure(
  gene_list         = "gene1",
  gff3_path         = file.path(toy, "toy.gff3"),
  genome_fasta_path = file.path(toy, "toy.fa"),
  output_dir        = tempdir(),
  formats           = "pdf",
  verbose           = FALSE)
#> Loading reference: toy.gff3 / CUSTOM 
#>   GFF3: /home/runner/work/_temp/Library/HaploBreedR/extdata/toy/toy.gff3 
#>   Note: no genome_fasta supplied -- chromosome lengths are approximated from the GFF3's
#>   own maximum feature coordinate per chromosome.
#>   Genes: 1 | Transcripts: 1 | CDS features: 1 | UTR features: 2 
#>   Sequence-resource QC: NO SEQUENCE DATA 
#> Warning: for 'Chr 1  •  1–2 kb (1.5 kb)  •  + strand' in 'mbcsToSbcs': . substituted for • (U+2022)
#> Warning: for 'Chr 1  •  1–2 kb (1.5 kb)  •  + strand' in 'mbcsToSbcs': - substituted for – (U+2013)
#> Warning: for 'Chr 1  •  1–2 kb (1.5 kb)  •  + strand' in 'mbcsToSbcs': . substituted for • (U+2022)
```
