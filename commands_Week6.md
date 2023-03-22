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