# Commands for Master's thesis
## Week 5
三月七号 - 三月十五号   
## Urate, Meta-analysis
No significant loci.   

## hba1c, Meta-analysis
## Regenie
### Asian
Phenotype: hba1c.pheno   
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
  --covarFile ${dir}/MAMA/covar_PC.covars \
  --covarCol PC{1:10} \
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
  --covarFile ${dir}/MAMA/covar_PC.covars \
  --covarCol PC{1:10} \
  --phenoFile ${dir}/MAMA/urate_1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ${dir}/MAMA/data_Regenie_White_urate_1_pred.list \
  --out ${dir}/MAMA/data_regenie_White_urate_out_firth_2
```
Output: data_regenie_White_urate_out_firth_2_Phenotype.regenie

### Black
Phenotype: urate.pheno   
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/MAMA/data_Black \
  --phenoFile ${dir}/MAMA/urate_1.pheno \
  --bsize 100 \
  --out ${dir}/MAMA/data_Regenie_Black_urate_1
```
  Since .pheno file needs FID and IID, I copied it and renamed urate_1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个urate_1.pheno文件并更改格式)   
Convert .bed to .bgen:  ${dir}/software/plink2 --bfile  ${dir}/MAMA/data_Black --export bgen-1.2 --out  ${dir}/MAMA/data_Black  
**Output**: data_Regenie_Black_urate_1_pred.list
2. 
```python
  regenie \
  --step 2 \
  --bgen $${dir}/MAMA/data_Black.bgen \
  --covarFile ${dir}/MAMA/covar_PC.covars \
  --covarCol PC{1:10} \
  --phenoFile ${dir}/MAMA/urate_1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ${dir}/MAMA/data_Regenie_Black_urate_1_pred.list \
  --out ${dir}/MAMA/data_regenie_Black_urate_out_firth_2
```
Output: data_regenie_Black_urate_out_firth_2_Phenotype.regenie

### Mixed
Phenotype: urate.pheno   
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/MAMA/data_Mixed \
  --phenoFile ${dir}/MAMA/urate_1.pheno \
  --bsize 100 \
  --out ${dir}/MAMA/data_Regenie_Mixed_urate_1
```
  Since .pheno file needs FID and IID, I copied it and renamed urate_1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个urate_1.pheno文件并更改格式)   
Convert .bed to .bgen:  ${dir}/software/plink2 --bfile  ${dir}/MAMA/data_Mixed --export bgen-1.2 --out  ${dir}/MAMA/data_Mixed  
**Output**: data_Regenie_Mixed_urate_1_pred.list
2. 
```python
  regenie \
  --step 2 \
  --bgen $${dir}/MAMA/data_Mixed.bgen \
  --covarFile ${dir}/MAMA/covar_PC.covars \
  --covarCol PC{1:10} \
  --phenoFile ${dir}/MAMA/urate_1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ${dir}/MAMA/data_Regenie_Mixed_urate_1_pred.list \
  --out ${dir}/MAMA/data_regenie_Mixed_urate_out_firth_2
```
Output: data_regenie_Mixed_urate_out_firth_2_Phenotype.regenie