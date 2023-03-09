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
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_SWC --phenoFile=${dir}/MAMA/urate_1.pheno --phenoCol=Phenotype --covarFile=${dir}/MAMA/covar_PC.covars --qCovarCol=PC{1:20} --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Urate/data_AsianSWC_bolt_urate
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