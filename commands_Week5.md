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
### Sex Chromosomes
1. Plink step   
To generate a file with .sexcheck, containing the F-statistics for each individual. **EUR.QC.sexcheck**   
A male is typically when F-statistic is > 0.8, and female is F<0.2.   
2. Rstudio step   
To exclude others.
3. Relatedness by plink.   
Before calculating, individuals with first or second degree relative > 0.125 should be removed.   
4. Final QC   

### Calculating PRS

https://choishingwan.github.io/PRS-Tutorial/plink/
**Effect Size**: Require OR instead of Beta, doing logarithm.   
**Clumping**: LD   
```python
./plink \
    --bfile EUR.QC \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump Height.QC.Transformed \
    --clump-snp-field SNP \
    --clump-field P \
    --out EUR
```
p1: P value threshold for a SNP to be included as an index SNP, 1 means that all SNPs are included.   
r2: SNPs having r2 higher than 0.1 will be removed.   
kb: SNPs within 250k of index SNP are considered for clumping.   

```python
awk 'NR!=1{print $3}' EUR.clumped >  EUR.valid.snp
```

```python
awk '{print $3,$8}' Height.QC.Transformed > SNP.pvalue
```

```python
echo "0.001 0 0.001" > range_list 
echo "0.05 0 0.05" >> range_list
echo "0.1 0 0.1" >> range_list
echo "0.2 0 0.2" >> range_list
echo "0.3 0 0.3" >> range_list
echo "0.4 0 0.4" >> range_list
echo "0.5 0 0.5" >> range_list
```

We then calculate PRS:   
```python
./plink \
    --bfile EUR.QC \
    --score Height.QC.Transformed 3 4 12 header \
    --q-score-range range_list SNP.pvalue \
    --extract EUR.valid.snp \
    --out EUR
```

### Accounting for Population Stratification
Population Stratification is the principle source of confounding in GWAS. 一般我们把PCs incorporate into covariates来解释。   
```python
# First, we need to perform prunning
plink \
    --bfile EUR.QC \
    --indep-pairwise 200 50 0.25 \
    --out EUR
# Then we calculate the first 6 PCs
plink \
    --bfile EUR.QC \
    --extract EUR.prune.in \
    --pca 6 \
    --out EUR
```

### FIND best-fit PRS
In Rstudio


## PRS Regenie Meta Urate, Plink
As example, Using Plink
### Update effect size and convert file format
SEE in Rstudio: PRS_Real.rmd   
```R
dat <- read_table2(file = "META_Regenie_Urate.TBL", col_names = TRUE)
# names(dat) <- 

assoc_data <- read_table2("data_regenie_White_urate_out_firth_2_Phenotype_modified.regenie", col_names = TRUE)
# hist(assoc_data$P_BOLT_LMM)
assoc_data1 <- assoc_data[,c("CHROM","GENPOS","ID")]
names(assoc_data1) <- c("CHR","BP","SNP")
dat1 <- select(dat, -c(7,8,9,10,11))
names(dat1) <- c("SNP", "A1", "A2", "BETA", "SE", "P", "N")
dat1 <- merge(assoc_data1, dat1, by = "SNP")
write.table(dat1, "META_Regenie_Urate.TBL.Transformed", quote = F, row.names = F)
```

### Clumping
消除LD的影响。   
```python
./software/plink \
    --bfile data_qc \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump ./PRS/META_Regenie_Urate.TBL.Transformed \
    --clump-snp-field SNP \
    --clump-field P \
    --out ./PRS/data_regenie_urate
```

SNP and P-value
```
awk 'NR!=1{print $3}' data_regenie_urate.clumped >  data_regenie_urate.valid.snp
awk '{print $1,$8}' META_Regenie_Urate.TBL.Transformed > META_Regenie_Urate.TBL.Transformed.pvalue
```

```
echo "0.001 0 0.001" > range_list 
echo "0.05 0 0.05" >> range_list
echo "0.1 0 0.1" >> range_list
echo "0.2 0 0.2" >> range_list
echo "0.3 0 0.3" >> range_list
echo "0.4 0 0.4" >> range_list
echo "0.5 0 0.5" >> range_list
```

### Calculating PRS with Plink
```
./plink \
    --bfile data_Asian \
    --score META_Regenie_Urate.TBL.Transformed 3 4 10 header \
    --q-score-range range_list META_Regenie_Urate.TBL.Transformed.pvalue \
    --extract data_regenie_urate.valid.snp \
    --out PRS_Regenie_Urate
```
Columns 3, 4, 9 are: SNP ID, Effective Allele, BETA(effect size)

### Accounting for Population Stratification
```python
./plink \
    --bfile data_Asian \
    --maf 0.01 \
    --hwe 1e-6 \
    --geno 0.01 \
    --mind 0.01 \
    --write-snplist \
    --make-just-fam \
    --out data_Asian
```

```python
./plink \
    --bfile data_Asian \
    --keep data_Asian.fam \
    --extract data_Asian.snplist \
    --indep-pairwise 200 50 0.25 \
    --out data_Asian
```



```python
# First, we need to perform prunning
./plink \
    --bfile data_Asian \
    --indep-pairwise 200 50 0.25 \
    --out data_Asian
# Then we calculate the first 6 PCs
./plink \
    --bfile data_Asian \
    --extract data_Asian.prune.in \
    --pca 10 \
    --out data_Asian
```