# Changelog

## HaploBreedR 0.99.1

### Initial submission

First release. The package accompanies the manuscript describing
haplotype-based breeding decisions in rice.

### Superior-haplotype discovery

- [`haplobreed_analysis()`](https://aksruchi.github.io/HaploBreedR/reference/haplobreed_analysis.md):
  single-trait pipeline from GWAS hits or a gene list to a superior
  haplotype per candidate gene. Builds LD decay and LD regions from the
  genotype, discovers functional variants (nonsynonymous CDS and UTR) in
  every tested gene, tests haplotype-trait associations (Student’s
  t-test / one-way ANOVA, optional PC correction, Tukey and Duncan
  post-hoc), and applies effect-size, permutation and false-discovery
  gates. Supports local, MSU7, RAP-DB and Ensembl Plants reference
  sources.

- [`hbr_generate_input_qc_report()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_generate_input_qc_report.md):
  unified input-QC report covering sequence-resource quality,
  genotype-reference compatibility and individual-ID overlap, written as
  a text report and three CSV tables.

- [`hbr_check_inputs()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_check_inputs.md):
  pre-flight validation of PLINK files, phenotype records, GFF3 features
  and sample-ID overlap before launching the full pipeline.

- [`hbr_go_enrichment()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_go_enrichment.md):
  GO over-representation per aspect (BP, MF, CC) against the tested-gene
  universe, with BH-FDR correction.

- [`hbr_regate()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_regate.md):
  re-applies the superior-haplotype gates (alpha, effect size, optional
  FDR, optional trait threshold) directly to a stored summary table for
  sensitivity analysis.

- [`hbr_read_results()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_read_results.md):
  ingests a completed per-trait output directory into a classed
  `hbr_run` object for downstream visualisation or genomic selection.

- [`hbr_gene_carriers()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_gene_carriers.md):
  extracts per-individual carrier status of the pipeline’s superior
  haplotype at a given gene, used to colour prediction-quality panels.

- `hbr_add_cross_annotation()` (internal): MSU7 ↔︎ RAP-DB gene-ID mapping
  from the RAP-DB release table; GO attachment via `org.Osativa.eg.db`
  when installed.

### Genomic prediction and breeding decisions

- [`hbr_advanced_decision()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_advanced_decision.md):
  multi-trait parent ranking and cross design from one or more
  [`haplobreed_analysis()`](https://aksruchi.github.io/HaploBreedR/reference/haplobreed_analysis.md)
  runs. Two-kernel genomic BLUP (VanRaden 2008; Kang et al. 2008) with
  the pipeline’s superior haplotypes as the feature kernel; honest
  nested cross-validation with in-fold discovery replay (M0 = GBLUP, M2
  = features chosen on all data, M3 = features re-discovered inside each
  training fold) and a paired comparison of the three (Nadeau and Bengio
  2003 corrected t-test plus a paired bootstrap over individuals).

- [`hbr_fit_models()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_fit_models.md):
  the phenotype-dependent half of the pipeline (loading, GRM, haplotype
  codes, gate replay, cross-validation, final models, multi-trait
  index). Returns an `hgsi_fit` object that can be saved once and
  reused.

- [`hbr_cross_design()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_cross_design.md):
  the second half of the pipeline. Consumes an `hgsi_fit` object, groups
  superior haplotypes into haplotype blocks, computes cross usefulness
  (Schnell and Utz 1975; Zhong and Jannink 2007), pyramiding
  probabilities and required population sizes (Sedcole 1977), and
  selects a diverse parent set by block coverage with a relatedness
  ceiling.

- Cross ranking by usefulness, block coverage, or a balanced mix;
  haplotype-pyramiding probabilities and DH / RIL / F2 population
  sizing.

- Exported modular building blocks:
  [`hbr_build_grm()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_build_grm.md),
  [`hbr_reml_two_kernel()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_reml_two_kernel.md),
  [`hbr_cross_usefulness()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_cross_usefulness.md),
  [`hbr_pyramid_probability()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_pyramid_probability.md),
  [`hbr_population_size()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_population_size.md),
  [`hbr_cross_plan()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_cross_plan.md),
  [`hbr_trait_conflicts()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_trait_conflicts.md).

### Haplotype blocks

- [`hbr_haplotype_blocks()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_haplotype_blocks.md):
  standalone block calling on any set of target loci. Supports the
  map-based rules (`"recomb"`, `"ld"`, `"either"`), the SNP-level
  methods (`"fourgamete"`, `"gabriel"`) and the two combinations
  (`"recomb+gabriel"`, `"recomb+fourgamete"`). Gabriel is implemented
  with the Gabriel et al. (2002) D′ confidence interval and vectorised
  pairwise gamete counting.

- [`hbr_haplotype_block_table()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_haplotype_block_table.md):
  the block summary table and the per-locus assignment in one call, for
  users who want the block table without the full pipeline.

### Genetic map

- [`hbr_rice_genetic_map()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_rice_genetic_map.md):
  the Nagamura et al. (1997) rice RFLP linkage-map anchors (n ≈ 1,650
  markers, total 1,510 cM) as a data frame with `chr`, `bp`, `cm`.
  Interpolated at run time onto the physical positions of any PLINK
  `.bim` with a monotone cubic Hermite spline.

- `hbr_rice_genetic_map_summary()`: one-row summary of the bundled
  anchors.

### Visualisation

- Publication-quality figures for haplotype structure, gene models, LD
  structure and cross design:
  [`hbr_plot_haplotype()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_plot_haplotype.md),
  [`hbr_plot_gene_list()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_plot_gene_list.md),
  [`hbr_plot_gene_structure()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_plot_gene_structure.md),
  [`hbr_plot_haplotype_network()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_plot_haplotype_network.md),
  `hbr_plot_ld_heatmap()`, `hbr_plot_superior_haplotype()`,
  [`hbr_plot_cross_ranking()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_plot_cross_ranking.md),
  [`hbr_plot_cv_forest()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_plot_cv_forest.md),
  `hbr_plot_cv_optimism()`, `hbr_plot_prediction_quality()`,
  `hbr_plot_selected_set_coverage()`, `hbr_plot_parent_profile()`,
  `hbr_plot_cross_landscape()`.

- S3 methods for the pipeline objects:
  [`plot()`](https://rdrr.io/r/graphics/plot.default.html) and
  [`summary()`](https://rdrr.io/r/base/summary.html) for `hbr_run` and
  `hgsi_advanced`; [`print()`](https://rdrr.io/r/base/print.html) and
  [`summary()`](https://rdrr.io/r/base/summary.html) for `hgsi_fit`;
  [`print()`](https://rdrr.io/r/base/print.html) for `hbr_reference`,
  `hbr_sequence_qc`, `hbr_compat_report`, `hbr_id_report` and
  `hbr_genotype`.

- Ten built-in colour palettes and ten ggplot2 themes; per-gene marker
  colours derived from the IUPAC allele set via `hbr_cell_colours()`.

### Manuscript tables and exported building blocks

- [`hbr_build_manuscript_tables()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_build_manuscript_tables.md):
  a multi-sheet Excel workbook from a pipeline run, with study summary,
  gene results, donor tables and breeding decisions.

### Reference layer

- [`hbr_crop_lookup()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_crop_lookup.md):
  built-in crop-to-species-to-assembly lookup for Ensembl Plants;
  refreshable against the live FTP listing.

- Local, MSU7, RAP-DB and Ensembl Plants reference sources; chromosome
  names standardised on every slot so they match the genotype convention
  applied by `hbr_normalize_genotype()`.

### Reproducibility and performance

- Every run writes `pipeline_summary.csv`, `phenotype_data_used.csv`,
  `functional_snps_all_tested_genes.csv`, `gene_attrition_log.csv` and
  `pipeline_result_for_breeding.rds`; the RDS carries the gate
  parameters and the exact phenotype table used, so downstream runs can
  be replayed without any external state.

- Genotype reads are streamed through `BEDMatrix`, so peak memory is one
  column block rather than the full genotype matrix; the RDS genotype
  packing is streamed from the same handle.

- [`hbr_advanced_decision()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_advanced_decision.md)
  records `provenance`, `warnings` and the evaluation label per trait
  (`honest_discovery_in_fold`, `conditional_on_gwas_candidates`,
  `conditional_on_discovered_set`, `approximate_replay`).

- `verbose` in every function selects a single-line-per-phase console
  summary; the detailed narration is available by passing
  `verbose = TRUE` where noted.
