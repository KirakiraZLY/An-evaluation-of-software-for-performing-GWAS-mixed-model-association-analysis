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
  --bsize 500 \
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
  --covarFile ${dir}/covar1.covars \
  --phenoFile ${dir}/type_1_error_new/non_genetic_trait_quant_1.pheno \
  --bsize 500 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/type_1_error_new/data_regenie_whole_nongenetic_out_1_pred.list \
  --out ${dir}/type_1_error_new/data_regenie_whole_nongenetic_out_2
```
Output: data_regenie_whole_nongenetic_out_2.regenie