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
data_1 is the data of population 1, and there will also be data_2 ...   