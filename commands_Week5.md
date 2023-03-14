# Commands for Master's thesis
## Week 5
三月七号 - 三月十五号   
## Urate, Meta-analysis
No significant loci found by Regenie.

## Bolt, height
### Chinese
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_Chinese --phenoFile=${dir}/MAMA/height1.pheno --phenoCol=Phenotype --covarFile=${dir}/MAMA/covar_PC.covars --qCovarCol=PC{1:20} --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Height/data_Chinese_bolt_height
```
### AsianSWC
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_SWC --phenoFile=${dir}/MAMA/height1.pheno --phenoCol=Phenotype --covarFile=${dir}/MAMA/covar_PC.covars --qCovarCol=PC{1:20} --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Height/data_AsianSWC_bolt_height
```
### White
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_White --phenoFile=${dir}/MAMA/height1.pheno --phenoCol=Phenotype --covarFile=${dir}/MAMA/covar_PC.covars --qCovarCol=PC{1:20} --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Height/data_White_bolt_height
```
### Black
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_Black --phenoFile=${dir}/MAMA/height1.pheno --phenoCol=Phenotype --covarFile=${dir}/MAMA/covar_PC.covars --qCovarCol=PC{1:20} --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Height/data_Black_bolt_height
```
### Mixed
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_Mixed --phenoFile=${dir}/MAMA/height1.pheno --phenoCol=Phenotype --covarFile=${dir}/MAMA/covar_PC.covars --qCovarCol=PC{1:20} --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Height/data_Mixed_bolt_height
```




# Testing Reversely
I have results from Regenie + urate and Bolt + height now. I am curious about the analysis reversed.   
数据bed bim fam都是用的MAMA/Bolt_Height里面的。   
## Bolt + Urate  
### Chinese
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_Chinese --phenoFile=${dir}/MAMA/urate_1.pheno --phenoCol=Phenotype --covarFile=${dir}/MAMA/covar_PC.covars --qCovarCol=PC{1:20} --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Urate/data_Chinese_bolt_urate
```
### AsianSWC
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_AsianSWC --phenoFile=${dir}/MAMA/urate_1.pheno --phenoCol=Phenotype --covarFile=${dir}/MAMA/covar_PC.covars --qCovarCol=PC{1:20} --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Urate/data_AsianSWC_bolt_urate
```
### White
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_White --phenoFile=${dir}/MAMA/urate_1.pheno --phenoCol=Phenotype --covarFile=${dir}/MAMA/covar_PC.covars --qCovarCol=PC{1:20} --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Urate/data_White_bolt_urate
```
### Black
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_Black --phenoFile=${dir}/MAMA/urate_1.pheno --phenoCol=Phenotype --covarFile=${dir}/MAMA/covar_PC.covars --qCovarCol=PC{1:20} --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Urate/data_Black_bolt_urate
```
### Mixed
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_Mixed --phenoFile=${dir}/MAMA/urate_1.pheno --phenoCol=Phenotype --covarFile=${dir}/MAMA/covar_PC.covars --qCovarCol=PC{1:20} --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Urate/data_Mixed_bolt_urate
```


## Regenie + Height
### AsianSWC
Phenotype: height.pheno   
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/MAMA/Bolt_Height/data_AsianSWC \
  --phenoFile ${dir}/MAMA/height1.pheno \
  --bsize 100 \
  --out ${dir}/MAMA/Regenie_Height/data_Regenie_AsianSWC_height_1
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen:  ${dir}/software/plink2 --bfile  ${dir}/MAMA/Bolt_Height/data_AsianSWC --export bgen-1.2 --out  ${dir}/MAMA/Bolt_Height/data_AsianSWC   
**Output**: data_Regenie_AsianSWC_height_1_pred.list
2. 
```python
  regenie \
  --step 2 \
  --bgen $${dir}/MAMA/Bolt_Height/data_AsianSWC.bgen \
  --covarFile ${dir}/MAMA/covar_PC.covars \
  --covarCol PC{1:20} \
  --phenoFile ${dir}/MAMA/height1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ${dir}/MAMA/Regenie_Height/data_Regenie_AsianSWC_height_1_pred.list \
  --out ${dir}/MAMA/Regenie_Height/data_regenie_AsianSWC_height_out_firth_2
```
Output: data_regenie_AsianSWC_height_out_firth_2_Phenotype.regenie

### Chinese
Phenotype: height.pheno   
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/MAMA/Bolt_Height/data_Chinese \
  --phenoFile ${dir}/MAMA/height1.pheno \
  --bsize 100 \
  --out ${dir}/MAMA/Regenie_Height/data_Regenie_Chinese_height_1
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen:  ${dir}/software/plink2 --bfile  ${dir}/MAMA/Bolt_Height/data_Chinese --export bgen-1.2 --out  ${dir}/MAMA/Bolt_Height/data_Chinese   
**Output**: data_Regenie_Chinese_height_1_pred.list
2. 
```python
  regenie \
  --step 2 \
  --bgen $${dir}/MAMA/Bolt_Height/data_Chinese.bgen \
  --covarFile ${dir}/MAMA/covar_PC.covars \
  --covarCol PC{1:20} \
  --phenoFile ${dir}/MAMA/height1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ${dir}/MAMA/Regenie_Height/data_Regenie_Chinese_height_1_pred.list \
  --out ${dir}/MAMA/Regenie_Height/data_regenie_Chinese_height_out_firth_2
```
Output: data_regenie_Chinese_height_out_firth_2_Phenotype.regenie

### White
Phenotype: height.pheno   
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/MAMA/Bolt_Height/data_White \
  --phenoFile ${dir}/MAMA/height1.pheno \
  --bsize 100 \
  --out ${dir}/MAMA/Regenie_Height/data_Regenie_White_height_1
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen:  ${dir}/software/plink2 --bfile  ${dir}/MAMA/Bolt_Height/data_White --export bgen-1.2 --out  ${dir}/MAMA/Bolt_Height/data_White   
**Output**: data_Regenie_White_height_1_pred.list
2. 
```python
  regenie \
  --step 2 \
  --bgen $${dir}/MAMA/Bolt_Height/data_White.bgen \
  --covarFile ${dir}/MAMA/covar_PC.covars \
  --covarCol PC{1:20} \
  --phenoFile ${dir}/MAMA/height1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ${dir}/MAMA/Regenie_Height/data_Regenie_White_height_1_pred.list \
  --out ${dir}/MAMA/Regenie_Height/data_regenie_White_height_out_firth_2
```
Output: data_regenie_White_height_out_firth_2_Phenotype.regenie

### Black
Phenotype: height.pheno   
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/MAMA/Bolt_Height/data_Black \
  --phenoFile ${dir}/MAMA/height1.pheno \
  --bsize 100 \
  --out ${dir}/MAMA/Regenie_Height/data_Regenie_Black_height_1
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen:  ${dir}/software/plink2 --bfile  ${dir}/MAMA/Bolt_Height/data_Black --export bgen-1.2 --out  ${dir}/MAMA/Bolt_Height/data_Black   
**Output**: data_Regenie_Black_height_1_pred.list
2. 
```python
  regenie \
  --step 2 \
  --bgen $${dir}/MAMA/Bolt_Height/data_Black.bgen \
  --covarFile ${dir}/MAMA/covar_PC.covars \
  --covarCol PC{1:20} \
  --phenoFile ${dir}/MAMA/height1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ${dir}/MAMA/Regenie_Height/data_Regenie_Black_height_1_pred.list \
  --out ${dir}/MAMA/Regenie_Height/data_regenie_Black_height_out_firth_2
```
Output: data_regenie_Black_height_out_firth_2_Phenotype.regenie

### Mixed
Phenotype: height.pheno   
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/MAMA/Bolt_Height/data_Mixed \
  --phenoFile ${dir}/MAMA/height1.pheno \
  --bsize 100 \
  --out ${dir}/MAMA/Regenie_Height/data_Regenie_Mixed_height_1
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen:  ${dir}/software/plink2 --bfile  ${dir}/MAMA/Bolt_Height/data_Mixed --export bgen-1.2 --out  ${dir}/MAMA/Bolt_Height/data_Mixed   
**Output**: data_Regenie_Mixed_height_1_pred.list
2. 
```python
  regenie \
  --step 2 \
  --bgen $${dir}/MAMA/Bolt_Height/data_Mixed.bgen \
  --covarFile ${dir}/MAMA/covar_PC.covars \
  --covarCol PC{1:20} \
  --phenoFile ${dir}/MAMA/height1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ${dir}/MAMA/Regenie_Height/data_Regenie_Mixed_height_1_pred.list \
  --out ${dir}/MAMA/Regenie_Height/data_regenie_Mixed_height_out_firth_2
```
Output: data_regenie_Mixed_height_out_firth_2_Phenotype.regenie



## PRS tutorial
https://choishingwan.github.io/PRS-Tutorial/target/   
### Standard GWAS QC
**MAF**: Removes all SNPs with minor allele frequency less than 0.01. Genotyping errors typically have a larger influence on SNPs with low MAF.    
**hwe**: Removes SNPs with low P-value from the Hardy-Weinberg Equilibrium Fisher's exact or chi-squared test. SNPs with significant P-values from the HWE test are more likely affected by genotyping error or the effects of natural selection.    
**geno**: Excludes SNPs that are missing in a high fraction of subjects.   
**mind**: Excludes individuals who have a high rate of genotype missingness, since this may indicate problems in the DNA sample or processing.   
### Prune
Very high or low heterozygosity rates in individuals could be due to DNA contamination or to high levels of inbreeding. Therefore, samples with extreme heterozygosity are typically removed prior to downstream analyses.   
1. We perform **prune** to remove highly correlated SNPs.   
**keep**: Informs Plink that we only want to use samples in .fam file in this analysis.   
**extract**: Use SNPs in .snplist file.   
**indep-pairwise**: 200 50 0.25, **200**: to perform pruning with a window size of 200 variants, **50**: sliding across hte genome with step size of 50 variants at a time. **0.25**: filter out any SNPs with LD r2 higher than 0.25.   
Output: .prune.in and .prune.out   
2. Heterozygosity rates can be computed using plink.   
This will generate the .het file. F列是coefficient，估计的是heterozygosity.   
**然后打开R**， remove individuals with F coefficients that are more than 3 standard deviation units from the mean.   
### Mismatching SNPs
1. Load the bim file, the summary statistic and the QC SNP list into R.