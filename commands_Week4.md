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
