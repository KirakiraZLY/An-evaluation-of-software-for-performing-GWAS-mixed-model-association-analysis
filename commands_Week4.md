# Commands for Master's thesis
## Week 4
3.3 - 3.9   

## Regenie UKBB_whole_height adding PC
Only Step 2 is needed.   
```python
  regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --covarFile ${dir}/covar1.covars \
  --phenoFile ${dir}/height1.pheno \
  --covarCol PC{1:4}
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ${dir}/ukbb_whole_height_result/data_regenie_out_pred.list \
  --out ${dir}/ukbb_whole_height_result/data_regenie_out_firth
```

## UKBB_MAMA
Multi-ancestry Meta Analysis   
1. Get real ethnicity.   
2. PCA comparason: real and K-means.   
   K-means performs well, and can predict on Missed Ethnicity, and wrong self-identification.   
   In other word, I can use the K-means to make division on data_qc.fam file.   

Plot comparison see in: Week_4 section of latex.   
Accuracy = 0.95.   
3. Extract files out: data_Mixed.fam data_Asian.fam data_Black.fam data_White.fam   


## Ancestry Inference
### Extract .bed and .fam into a single population
In the folder: ./MAMA
```python
${dir}/software/plink --bfile ${dir}/MAMA/data_qc --noweb --keep ${dir}/MAMA/data_Asian.fam --recode --make-bed --out ${dir}/MAMA/data_Asian
```
Jobinfo: ${dir}/script/MAMA/Plink_Extract_*   

## Regenie
### Asian as example
Phenotype: urate.pheno   
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/MAMA/data_Asian \
  --phenoFile ${dir}/MAMA/urate_1.pheno \
  --bsize 100 \
  --out ${dir}/MAMA/data_Regenie_Asian_urate_1
```
  Since .pheno file needs FID and IID, I copied it and renamed urate_1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个urate_1.pheno文件并更改格式)   
Convert .bed to .bgen:  ${dir}/software/plink2 --bfile  ${dir}/MAMA/data_Asian --export bgen-1.2 --out  ${dir}/MAMA/data_Asian   
**Output**: data_Regenie_Asian_urate_1_pred.list
2. 
```python
  regenie \
  --step 2 \
  --bgen $${dir}/MAMA/data_Asian.bgen \
  --covarFile ${dir}/MAMA/covar1.covars \
  --covarCol PC{1:4}
  --phenoFile ${dir}/MAMA/urate_1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ${dir}/MAMA/data_Regenie_Asian_urate_1_pred.list \
  --out ${dir}/MAMA/data_regenie_Asian_urate_out_firth_2
```
Output: data_regenie_Asian_urate_out_firth_2_Phenotype.regenie

### White
Phenotype: urate.pheno   
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/MAMA/data_White \
  --phenoFile ${dir}/MAMA/urate_1.pheno \
  --bsize 100 \
  --out ${dir}/MAMA/data_Regenie_White_urate_1
```
  Since .pheno file needs FID and IID, I copied it and renamed urate_1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个urate_1.pheno文件并更改格式)   
Convert .bed to .bgen:  ${dir}/software/plink2 --bfile  ${dir}/MAMA/data_White --export bgen-1.2 --out  ${dir}/MAMA/data_White   
**Output**: data_Regenie_White_urate_1_pred.list
2. 
```python
  regenie \
  --step 2 \
  --bgen $${dir}/MAMA/data_White.bgen \
  --covarFile ${dir}/MAMA/covar1.covars \
  --covarCol PC{1:4}
  --phenoFile ${dir}/MAMA/urate_1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ${dir}/MAMA/data_Regenie_White_urate_1_pred.list \
  --out ${dir}/MAMA/data_regenie_White_urate_out_firth_2
```
Output: data_regenie_White_urate_out_firth_2_Phenotype.regenie