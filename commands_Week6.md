# Commands for Master's thesis
# Week 6
三月十六号 - 三月二十二号

## Regenie Modify
Stack size, without firth.   
### Type 1 error
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/type_1_error_new/non_genetic_trait_quant_1.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --bsize 500 \
  --lowmem \
  --out ${dir}/type_1_error_new/data_regenie_whole_nongenetic_out_1   
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)
Convert .bed to .bgen: ./software/plink2 --bfile data_qc --export bgen-1.2 --out data_qc   
**Output**: data_regenie_whole_nongenetic_out_1_pred.list
2. 
```python
  regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --covarFile ${dir}/covar_PC.covars \
  --phenoFile ${dir}/type_1_error_new/non_genetic_trait_quant_1.pheno \
  --bsize 500 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/type_1_error_new/data_regenie_whole_nongenetic_out_1_pred.list \
  --out ${dir}/type_1_error_new/data_regenie_whole_nongenetic_out_2
```
Output: data_regenie_whole_nongenetic_out_2.regenie


## PRSice2, Asian
### Step 1
See ./PRS/PRS_Real.Rmd, to build data.covariate file.   

### Step 2
To run PRSice2, to obtain PRS results.   
```python
Rscript ${dir}/PRS/PRSice2/PRSice.R \
    --prsice ${dir}/PRS/PRSice2/PRSice_linux \
    --base ${dir}/PRS/META_Regenie_Urate.TBL.Transformed \
    --target ${dir}/PRS/data_Asian \
    --binary-target F \
    --pheno ${dir}/PRS/urate_1.pheno \
    --cov ${dir}/PRS/data.covariate \
    --base-maf MAF:0.01 \
    --base-info INFO:0.8 \
    --stat OR \
    --or \
    --quantile 20 \
    --out ${dir}/PRS/PRSice2/Result_PRSice2_Asian_Urate
```


## Simulation traits: H2 0.1 - 0.9
H2 = 0.1 : 0.9   
Causal SNPs = 1000   
```python
  ${dir}/software/ldak5.XXX \
  --make-phenos ${dir}/h2_test/data_h2_1 \
  --bfile ${dir}/data_qc \
  --ignore-weights YES \
  --power -1 \
  --her 0.1 \
  --num-phenos 4 \
  --num-causals 1000
```   




## Regenie + Height(Redo, see Week 5)
### AsianSWC
Phenotype: height.pheno   
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/MAMA/Bolt_Height/data_AsianSWC \
  --phenoFile ${dir}/MAMA/height1.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:20} \
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
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:20} \
  --extract ${dir}/MAMA/Regenie_Height/Chinese_snps_pass.snplist \
  --bsize 100 \
  --out ${dir}/MAMA/Regenie_Height/data_Regenie_Chinese_height_1
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen:  ${dir}/software/plink2 --bfile  ${dir}/MAMA/Bolt_Height/data_Chinese --export bgen-1.2 --out  ${dir}/MAMA/Bolt_Height/data_Chinese   
**Output**: data_Regenie_Chinese_height_1_pred.list

In Step 1, **-residualizing and scaling genotypes...ERROR: !! Uh-oh, SNP rs6598892 has low variance (=0.000000)**. So I should remove SNPs below mac, while I actually have done it already.   
```python
  ${dir}/software/plink2 \
  --bfile data_Chinese \
  --mac 100 \
  --write-snplist \
  --out Chinese_snps_pass
```



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
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:20} \
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
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:20} \
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
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:20} \
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

## META
## PRS
cd ${dir}/PRS
1. I calculate PRS scores for the whole data, while it performed badly.
2. I calculate PRS scores by each ancestry, and I'll have 5 different files. Then I will combine them and see the result.
## Plink for PRS
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
    --clump ./PRS/PRS_META_Regenie_Height/METAANALYSIS_Regenie_5Ancestries_Height.tbl.Transformed \
    --clump-snp-field SNP \
    --clump-field P \
    --out ./PRS/PRS_META_Regenie_Height/Plink/data_Plink_regenie_height
```

SNP and P-value
```
awk 'NR!=1{print $3}' data_Plink_regenie_height.clumped >  data_Plink_regenie_height.valid.snp
awk '{print $1,$8}' METAANALYSIS_Regenie_5Ancestries_Height.tbl.Transformed > METAANALYSIS_Regenie_5Ancestries_Height.tbl.Transformed.pvalue
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
./software/plink \
    --bfile ./MAMA/Bolt_Height/data_AsianSWC \
    --score ./PRS/PRS_META_Regenie_Height/METAANALYSIS_Regenie_5Ancestries_Height.tbl.Transformed 3 4 10 header \
    --q-score-range ./PRS/PRS_META_Regenie_Height/Plink/range_list ./PRS/PRS_META_Regenie_Height/Plink/METAANALYSIS_Regenie_5Ancestries_Height.tbl.Transformed.pvalue \
    --extract ./PRS/PRS_META_Regenie_Height/Plink/data_Plink_regenie_height.valid.snp \
    --out ./PRS/PRS_META_Regenie_Height/Plink/PRS_AsianSWC_Regenie_Height
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