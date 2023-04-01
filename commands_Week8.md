# Week 8
2023/3/31 - 2023/4/6

## Test Mixed Model on different parameters
### Simulate phenotypes based on different parameters
Quantitative/ Binary   
Number of Causal: 1000, 10000   
h2: 0.1, 0.5, 0.9   
heritability model: GCTA, LDAK   
Number of individuals: 10K, 70K   
Replicate Phenotypes: 5 phenotypes   

High number of causal SNPs will have high polygenicity, and decrease the effect size of each SNP.   

${dir}/type_1_error/Multi_Traits/

Trait name labels:   
qt: quantitative   
Wan: 10K individuals, 7Wan: 70K individuals.   
GCTA: power -1, ignore weight   
h01: h2 = 0.1; h05, h09   
K: 1000 causal snps; 10K 10K causal snps.   

### 1. qt, 7 Wan, GCTA -1, h2=0.1, 5 Phenos, 1K causal

```python
${dir}/software/ldak5.XXX \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_qt_7Wan_GCTA_h01_K_1 \
  --bfile ${dir}/data_qc \
  --ignore-weights YES \
  --power -1 \
  --her 0.1 \
  --num-phenos 5 \
  --num-causals 1000 \
  --extract ${dir}/type_1_error/Multi_Traits/list_snps_1_to_12.txt
```

### 2. qt, 7 Wan, GCTA, h2=0.5, 5 Phenos, 1K causal

```python
${dir}/software/ldak5.XXX \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_qt_7Wan_GCTA_h05_K_1 \
  --bfile ${dir}/data_qc \
  --ignore-weights YES \
  --power -1 \
  --her 0.5 \
  --num-phenos 5 \
  --num-causals 1000 \
  --extract ${dir}/type_1_error/Multi_Traits/list_snps_1_to_12.txt
```

### 3. qt, 7 Wan, GCTA, h2=0.9, 5 Phenos, 1K causal

```python
${dir}/software/ldak5.XXX \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_qt_7Wan_GCTA_h09_K_1 \
  --bfile ${dir}/data_qc \
  --ignore-weights YES \
  --power -1 \
  --her 0.9 \
  --num-phenos 5 \
  --num-causals 1000 \
  --extract ${dir}/type_1_error/Multi_Traits/list_snps_1_to_12.txt
```

### Submitted
Pheno: ${dir}/type_1_error/Multi_Traits
Result: ${dir}/type_1_error/Multi_Traits/Result*/


## Run software on these three phenos
### 1
### Regenie
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/type_1_error/Multi_Traits/Trait_qt_7Wan_GCTA_h01_K_1_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:20} \
  --bsize 1000 \
  --out ${dir}/type_1_error/Multi_Traits/Result_Trait_qt_7Wan_GCTA_h01_K_1/Result_regenie_qt_7Wan_GCTA_h01_K_1_s1 
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen: ./software/plink2 --bfile data_qc --export bgen-1.2 --out data_qc   
**Output**: data_regenie_whole_h201Power_out_1_s1.list
2. 
```python
  regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --covarFile ${dir}/covar_PC.covars \
  --phenoFile ${dir}/type_1_error/Multi_Traits/Trait_qt_7Wan_GCTA_h01_K_1_label.pheno \
  --covarCol PC{1:20} \
  --bsize 1000 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/type_1_error/Multi_Traits/Result_Trait_qt_7Wan_GCTA_h01_K_1_label/Result_regenie_qt_7Wan_GCTA_h01_K_1_s1.list \
  --out ${dir}/type_1_error/Multi_Traits/Result_Trait_qt_7Wan_GCTA_h01_K_1/Result_regenie_qt_7Wan_GCTA_h01_K_1_s2
```
Output: Result_regenie_qt_7Wan_GCTA_h01_K_1_s2.regenie

### Bolt
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/type_1_error/Multi_Traits/Trait_qt_7Wan_GCTA_h01_K_1_label.pheno  --phenoCol=Phenotype --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:20}  --lmmForceNonInf --LDscoresUseChip  --statsFile=${dir}/type_1_error/Multi_Traits/Result_Trait_qt_7Wan_GCTA_h01_K_1/Result_bolt_qt_7Wan_GCTA_h01_K_1.Bolt
```

### Bolt-inf
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc \
--phenoFile=${dir}/Power/h2_01/trait_quant_h2_01_1_label.pheno  --phenoCol=Phenotype --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:20} \ 
 --lmmInfOnly --LDscoresUseChip \ 
 --statsFile=${dir}/Power/h2_01/data_bolt_inf_whole_Power01_out.Bolt
```

### Plink
assoc test   
```python
${dir}/software/plink \
--bfile ${dir}/data_qc \
--linear \
--covar ${dir}/covar_PC_withoutLabel.covars \
--pheno ${dir}/Power/h2_01/trait_quant_h2_01_1.pheno --allow-no-sex \
--out ${dir}/Power/h2_01/data_plink_Power01_finalresult 
```

### LDAK
Quant   
```python
${dir}/software/ldak5.XXX \
--pheno ${dir}/Power/h2_01/trait_quant_h2_01_1.pheno \
--covar ${dir}/covar_PC_withoutLabel.covars \
--bfile ${dir}/data_qc \
--linear ${dir}/Power/h2_01/data_ldak_whole_Power01_result
```