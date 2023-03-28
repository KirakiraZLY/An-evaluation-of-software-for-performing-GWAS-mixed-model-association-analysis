# Week 7

### Bolt non-genetic inf only
To check the time effiency.   
It is an approximation method using 30 pseudorandom SNPs to get mean value.   
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/type_1_error/non_genetic_trait_quant_1.pheno --phenoCol=Phenotype --lmmInfOnly  --LDscoresUseChip --statsFile=${dir}/type_1_error/data_bolt_inf_whole_nongenetic_result.Bolt
```
Location: type_1_error   
Script: ${dir}/scriptsbolt_ukbb_nongenetic_infOnly_1   

## Regenie by different Parameters
Performance and Time complexity
### Bsize = 500, J = 10
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/type_1_error/non_genetic_trait_quant_1.pheno \
  --bsize 100 \
  --out ${dir}/type_1_error_new/data_regenie_whole_nongenetic_B500J10_out_1   
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen: ./software/plink2 --bfile data_qc --export bgen-1.2 --out data_qc   
**Output**: data_regenie_whole_nongenetic_B500J10_out_1_pred.list
2. 
```python
  regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --covarFile ${dir}/covar1.covars \
  --phenoFile ${dir}/type_1_error/non_genetic_trait_quant_1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ${dir}/type_1_error/data_regenie_whole_nongenetic_out_1_pred.list \
  --out ${dir}/type_1_error/data_regenie_whole_nongenetic_out_2_firth
```
Output: data_regenie_whole_nongenetic_out_2_firth.regenie