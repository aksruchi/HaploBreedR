# HaploBreedR

**Superior haplotype discovery and haplotype-guided genomic selection
for crop breeding.**

HaploBreedR is an end-to-end quantitative genomics and molecular
breeding suite. It identifies superior functional haplotypes from
nonsynonymous CDS and UTR variants under false discovery rate control,
fits two-kernel spectral REML genomic prediction models with the
pipeline’s superior haplotypes as a feature kernel, performs
haplotype-guided cross-usefulness prediction and linkage-aware
pyramiding optimization, and selects diverse parent sets with a
relatedness ceiling.

📊 **[One-page
infographic](https://aksruchi.github.io/HaploBreedR/infographic.html)**
([print
TIFF](https://aksruchi.github.io/HaploBreedR/reference/figures/HaploBreedR_infographic.tiff))
— the pipeline at a glance.

[![HaploBreedR pipeline
infographic](reference/figures/HaploBreedR_infographic.png)](https://aksruchi.github.io/HaploBreedR/infographic.html)  
*One-page infographic — the pipeline at a glance*

![Example per-gene haplotype summary
figure](reference/figures/LOC_Os01g24450_haplotype_figure.png)  
*Example per-gene figure produced by
`haplobreed_analysis(plot_style = “gene_list”)`*

## *A four-panel summary for a single superior gene: gene model, haplotype network, haplotype table, and trait distribution. Produced automatically by `haplobreed_analysis(plot_style = "gene_list")`.*

## Installation

\`\`\`r \# install.packages(“devtools”)
devtools::install_github(“aksruchi/HaploBreedR”)
