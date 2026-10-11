# HaploBreedR: haplotype-based breeding decisions

Identifies superior haplotypes at candidate genes from GWAS hits and
genotype data, tests haplotype-trait associations, applies effect-size
and permutation gates, and produces multi-trait breeding
recommendations.

## Optional parallel backend

When \`n_cores \> 1\`, the GRM builder uses \`future\` and
\`future.apply\` for parallel block computation. Install those packages
if you need multi-core GRM construction; otherwise the builder runs
sequentially.

## Function length

The package deliberately keeps several long orchestration functions
([`haplobreed_analysis()`](https://aksruchi.github.io/HaploBreedR/reference/haplobreed_analysis.md)
and
[`hbr_advanced_decision()`](https://aksruchi.github.io/HaploBreedR/reference/hbr_advanced_decision.md))
as single entry points. Splitting them would require passing dozens of
intermediate objects between helpers, which increases coupling without
improving readability. All internal helpers are shorter than 50 lines.

## See also

Useful links:

- <https://aksruchi.github.io/HaploBreedR>

- Report bugs at <https://github.com/aksruchi/HaploBreedR/issues>

## Author

**Maintainer**: Dr. Akansha Singh <akansha.iasbhu@gmail.com>
([ORCID](https://orcid.org/0000-0002-4916-7296))

Authors:

- Dr. Akansha Singh <akansha.iasbhu@gmail.com>
  ([ORCID](https://orcid.org/0000-0002-4916-7296))
