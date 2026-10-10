# Plot publication-quality haplotype figures for a list of genes

Builds a four-panel figure per gene (gene model, haplotype network,
haplotype summary table, trait distribution) and saves each figure in
the requested formats. \`gene_list\` may be a character vector of gene
IDs, a path to a summary CSV, a directory containing the pipeline
outputs, or an in-memory \`data.table\`.

## Usage

``` r
hbr_plot_gene_list(
  gene_list,
  output_dir = NULL,
  summary_csv = NULL,
  per_gene_dir = NULL,
  result = NULL,
  reference = NULL,
  gff3_path = NULL,
  trait_col = "NT",
  trait_label = NULL,
  n_gene = NULL,
  sort_by = c("Cohens_d", "Superior_Mean"),
  panels = c("gene_model", "haplotype_network", "haplotype_table", "trait_boxplot"),
  palette = "haplobreed",
  theme = "haplobreed",
  table_style = c("color_coded", "row_highlight"),
  include_nt = FALSE,
  include_aa = FALSE,
  aa_full_names = TRUE,
  width = 12,
  height = 14,
  formats = c("pdf", "png"),
  combined_pdf = TRUE,
  figures_dir = "figures",
  verbose = TRUE
)
```

## Arguments

- gene_list:

  IDs, CSV path, directory path, or data.frame.

- output_dir:

  Directory holding per-gene files.

- summary_csv:

  Optional path to the summary CSV.

- per_gene_dir:

  Override for the directory holding per-gene files.

- result:

  Optional in-memory \[haplobreed_analysis()\] output.

- reference:

  Optional \`hbr_reference\` object.

- gff3_path:

  Optional GFF3 path; parsed once and cached for the session.

- trait_col:

  Trait column name.

- trait_label:

  Human-readable trait label.

- n_gene:

  Keep at most this many genes.

- sort_by:

  Character vector of columns to rank by.

- panels:

  Panels to draw.

- palette:

  One of \[hbr_palette_names()\].

- theme:

  One of \[hbr_theme_names()\].

- table_style:

  \`"color_coded"\` or \`"row_highlight"\`.

- include_nt, include_aa:

  Include NT / AA sequence columns.

- aa_full_names:

  Use three-letter amino-acid codes.

- width, height:

  Figure dimensions in inches.

- formats:

  Output formats.

- combined_pdf:

  Also write a multi-page PDF.

- figures_dir:

  Subdirectory of \`output_dir\` for figures.

- verbose:

  Print progress.

## Value

Invisibly, a list with \`plots\`, \`files\`, \`missing_genes\`,
\`combined_pdf\`.
