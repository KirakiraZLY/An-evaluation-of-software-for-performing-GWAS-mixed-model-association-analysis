# Week 9

## Simulate Binary Traits: 25-48
### 25. bi, 7 Wan, GCTA -1, h2=0.1, 5 Phenos, 1K causal

```python
${dir}/software/ldak5.XXX \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_25_bi_7Wan_GCTA_h01_K \
  --bfile ${dir}/data_qc \
  --ignore-weights YES \
  --power -1 \
  --her 0.1 \
   --prevalence 0.5 \
  --num-phenos 5 \
  --num-causals 1000 \
  --extract ${dir}/type_1_error/Multi_Traits/snps_1_to_12_7Wan.txt
``` 


















# Run on 8 - 24 八到二十四
## 8 直接在 leyi_week9_software.txt上改
### Regenie
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/type_1_error/Multi_Traits/Trait_qt_7Wan_GCTA_h05_10K_5_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:20} \
  --bsize 1000 \
  --out ${dir}/type_1_error/Multi_Traits/Result_Trait_qt_7Wan_GCTA_h05_10K_5/Result_regenie_qt_7Wan_GCTA_h05_10K_5_s1  
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen: ./software/plink2 --bfile data_qc --export bgen-1.2 --out data_qc   
**Output**: data_regenie_whole_h201Power_out_1_s1_pred.list
2. 
```python
  regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --covarFile ${dir}/covar_PC.covars \
  --phenoFile ${dir}/type_1_error/Multi_Traits/Trait_qt_7Wan_GCTA_h09_K_3_label.pheno \
  --covarCol PC{1:20} \
  --bsize 1000 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/type_1_error/Multi_Traits/Result_Trait_qt_7Wan_GCTA_h01_K_1_label/Result_regenie_qt_7Wan_GCTA_h01_K_1_s1_pred.list \
  --out ${dir}/type_1_error/Multi_Traits/Result_Trait_qt_7Wan_GCTA_h09_K_3/Result_regenie_qt_7Wan_GCTA_h09_K_3_s2
```
Output: Result_regenie_qt_7Wan_GCTA_h09_K_3_s2.regenie

### Bolt
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/type_1_error/Multi_Traits/Trait_qt_7Wan_GCTA_h09_K_3_label.pheno  --phenoCol=Phenotype5  --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:20}  --lmmForceNonInf --LDscoresUseChip  --statsFile=${dir}/type_1_error/Multi_Traits/Result_Trait_qt_7Wan_GCTA_h09_K_3/Result_bolt_qt_7Wan_GCTA_h09_K_3_P1.Bolt --numThreads 8
```

### Bolt-inf
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/type_1_error/Multi_Traits/Trait_qt_7Wan_GCTA_h09_K_3_label.pheno  --phenoCol=Phenotype1 --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:20}  --lmmInfOnly --LDscoresUseChip --statsFile=${dir}/type_1_error/Multi_Traits/Result_Trait_qt_7Wan_GCTA_h09_K_3/Result_bolt_inf_qt_7Wan_GCTA_h09_K_3_P2.Bolt --numThreads 8
```

### Plink
assoc test  
跑过了已经 
```python
${dir}/software/plink --bfile ${dir}/data_qc --linear --covar ${dir}/covar_PC_withoutLabel.covars --pheno ${dir}/type_1_error/Multi_Traits/Trait_qt_7Wan_GCTA_h09_K_3.pheno --mpheno 1 --allow-no-sex --out ${dir}/type_1_error/Multi_Traits/Result_Trait_qt_7Wan_GCTA_h09_K_3/Result_plink_inf_qt_7Wan_GCTA_h09_K_3_P1 --threads 8
```

### LDAK
Quant   
```python
${dir}/software/ldak5.XXX --pheno ${dir}/type_1_error/Multi_Traits/Trait_qt_7Wan_GCTA_h09_K_3.pheno --mpheno 1 --covar ${dir}/covar_PC_withoutLabel.covars --bfile ${dir}/data_qc --linear ${dir}/type_1_error/Multi_Traits/Result_Trait_qt_7Wan_GCTA_h09_K_3/Result_ldak_inf_qt_7Wan_GCTA_h09_K_3_P1 --max-threads 8
```
