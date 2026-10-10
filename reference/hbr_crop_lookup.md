# Common crops mapped to their Ensembl Plants species and assembly

Returns the crop-to-species-to-assembly lookup table. If a cached table
exists under \`tools::R_user_dir("haplobreed", "cache")\`, it is
returned; otherwise the built-in default from
\[\`.hbr_crop_lookup_default()\`\] is used.

## Usage

``` r
hbr_crop_lookup()
```

## Value

A \`data.table\` with columns \`crop\`, \`species\`, \`assembly\`.

## Examples

``` r
crop <- hbr_crop_lookup()
head(crop)
#>             crop           species                         assembly
#>           <char>            <char>                           <char>
#> 1: rice_japonica      oryza_sativa                        IRGSP-1.0
#> 2:   rice_indica      oryza_indica                         ASM465v1
#> 3:         maize          zea_mays         Zm-B73-REFERENCE-NAM-5.0
#> 4:         wheat triticum_aestivum                            IWGSC
#> 5:        barley   hordeum_vulgare MorexV3_pseudomolecules_assembly
#> 6:       sorghum   sorghum_bicolor           Sorghum_bicolor_NCBIv3
crop$crop
#>  [1] "rice_japonica"  "rice_indica"    "maize"          "wheat"         
#>  [5] "barley"         "sorghum"        "foxtail_millet" "brachypodium"  
#>  [9] "soybean"        "common_bean"    "peanut"         "potato"        
#> [13] "cassava"        "sugar_beet"     "brassica_rapa"  "grape"         
#> [17] "peach"          "sunflower"      "poplar"         "eucalyptus"    
#> [21] "arabidopsis"   
```
