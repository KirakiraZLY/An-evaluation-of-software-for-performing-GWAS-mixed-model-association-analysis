# Commands for Master's thesis
## Week 3
2.24 - 3.1

### 2.24
1. Finished running: ukbb binary bolt, ./ukbb_binary_test
2. Manhattan and QQ plot of 1, bad result.

Command for 1 is:   
### Bolt lmm ukbb binary(--covarFile=covar1.covars --qCovarCol)
```python
./software/BOLT-LMM_v2.4/bolt --bfile=./ukbb_binary_test/data_qc --phenoFile=./ukbb_binary_test/data_binary_1.pheno --phenoCol=Phenotype --lmmForceNonInf --LDscoresUseChip --statsFile=./ukbb_binary_test/data_qc_bolt_binary --maxModelSnps 9000000
```
Since the number of SNPs is 6M here(>1M), adding --maxModelSnps option.


### Bolt lmm ukbb region_1, trait = height(--covarFile=covar1.covars --qCovarCol)
```python
./software/BOLT-LMM_v2.4/bolt --bfile=./ukbb_by_ancestry/data_region1 --phenoFile=./ukbb_by_ancestry/height1.pheno --phenoCol=Phenotype --lmmForceNonInf --LDscoresUseChip --statsFile=./ukbb_by_ancestry/data_region1_bolt_height
```
Since the number of SNPs is 6M here(>1M), adding --maxModelSnps option.


### fastGWA
https://yanglab.westlake.edu.cn/software/gcta/#fastGWA   
1. To generate a sparse GRM from SNP data:
  ```python
${dir}/software/gcta \
--bfile ${dir}/ukbb_by_ancestry/data_region1 \
--autosome --maf 0.01 \
--make-grm --out ${dir}/ukbb_by_ancestry/data_region1_gcta \
--thread-num 10
```   
2. Next Sparse GRM    
```python  
${dir}/software/gcta \
--grm ${dir}/ukbb_by_ancestry/data_region1_gcta --make-bK-sparse 0.05 \
--out ${dir}/ukbb_by_ancestry/data_region1_gcta_grm   
```   
3. I didn't use PCs
```python
${dir}/software/gcta \
 --bfile ${dir}/ukbb_by_ancestry/data_region1 \
 --grm-sparse ${dir}/ukbb_by_ancestry/data_region1_gcta_grm --fastGWA-mlm --pheno ${dir}/ukbb_by_ancestry/height.pheno --thread-num 10 --out ${dir}/ukbb_by_ancestry/data_region1_fastgwa_height    
```

# UKBB Whole Height
## fastGWA
1. To generate a sparse GRM from SNP data:
  ```python
${dir}/software/gcta \
--bfile ${dir}/data_qc \
--autosome --maf 0.01 \
--make-grm --out ${dir}/ukbb_whole_height_result/data_qc_gcta \
--thread-num 10
```   
2. Next Sparse GRM    
```python  
${dir}/software/gcta \
--grm ${dir}/ukbb_whole_height_result/data_qc_gcta --make-bK-sparse 0.05 \
--out ${dir}/ukbb_whole_height_result/data_qc_gcta_grm   
```   
3. I didn't use PCs
```python
${dir}/software/gcta --bfile ${dir}/data_qc --grm-sparse ${dir}/ukbb_whole_height_result/data_qc_gcta_grm --fastGWA-mlm --pheno ${dir}/height.pheno --thread-num 10 --out ${dir}/ukbb_whole_height_result/data_fastgwa_height_finalresult 
 ```

## Regenie
### Regenie
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile height1.pheno \
  --bsize 100 \
  --out ${dir}/ukbb_whole_height_result/data_regenie_out   
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen: ./software/plink2 --bfile data_qc --export bgen-1.2 --out data_qc   
**Output**: data_regenie_out_pred.list
2. 
```python
  regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --covarFile ${dir}/covar1.covars \
  --phenoFile ${dir}/height1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ${dir}/ukbb_whole_height_result/data_regenie_out_pred.list \
  --out ${dir}/ukbb_whole_height_result/data_regenie_out_firth
```
Output: data_regenie_out_firth_Phenotype.regenie
## Bolt
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/height1.pheno --phenoCol=Phenotype --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/ukbb_whole_height_result/data_bolt_height
```

## 2/27
### LDAK-GBAT
  Using LDAK to run for 60k ind.     
  Binary   
```python
${dir}/software/ldak5.XXX --logistic ${dir}/ukbb_binary_test/data_binary_ldak --pheno ${dir}/ukbb_binary_test/data_binary.pheno --covar ${dir}/covar.covars --bfile ${dir}/ukbb_binary_test/data_qc
```
Quant   
```python
${dir}/software/ldak5.XXX --linear ${dir}/ukbb_whole_height_result/data_ldak_height --pheno ${dir}/height.pheno --covar ${dir}/covar.covars --bfile ${dir}/data_qc
```
Find Independent Significant Loci
```python
${dir}/software/ldak5.XXX --thin-tops ${dir}/ukbb_whole_height_result/data_ldak_height_top --bfile ${dir}/data_qc --pvalues ${dir}/ukbb_whole_height_result/data_ldak_height.pvalues --cutoff 5e-8 --window-cm 1 --window-prune 0.05
```

### Type I error
1. To generate a set of data: complete non-genetic trait. 
   N(0,1), h2 = 0   
   doi:  10.1002/gepi.22168
```python
${dir}/software/ldak5.XXX --make-phenos ${dir}/type_1_error/non_genetic_trait_quant --bfile ${dir}/data_qc --ignore-weights YES --power 0 --her 0 --num-phenos 1 --num-causals 1
```
2. Generate successfully: into file ${dir}/type_1_error/non_genetic_trait_quant
3. Redo fastGWA, regenie, bolt, LDAK

## LDAK, non_genetic_trait_quant
Quant   
```python
${dir}/software/ldak5.XXX --linear ${dir}/type_1_error/data_ldak_whole_nongenetic_result --pheno ${dir}/type_1_error/non_genetic_trait_quant.pheno --covar ${dir}/covar.covars --bfile ${dir}/data_qc
```

# 2.28
## Duty
1. non_genetic_trait_quant in 4 different softwares.   
LDAK see above.   

## Bolt
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/type_1_error/non_genetic_trait_quant_1.pheno --phenoCol=Phenotype --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/type_1_error/data_bolt_whole_nongenetic_result
```