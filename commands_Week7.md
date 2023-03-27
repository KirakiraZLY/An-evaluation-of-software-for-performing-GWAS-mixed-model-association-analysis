# Week 7
2023/3/27 - 2023/3/30

### Bolt non-genetic inf only
To check the time effiency.   
It is an approximation method using 30 pseudorandom SNPs to get mean value.  

In the analysis below, I tested nongenetic traits on 66688 individuals with 300K SNPs.   
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/type_1_error/non_genetic_trait_quant_1.pheno --phenoCol=Phenotype --lmmInfOnly  --LDscoresUseChip --statsFile=${dir}/type_1_error/data_bolt_inf_whole_nongenetic_result.Bolt
```
Location: type_1_error   
Script: ${dir}/scriptsbolt_ukbb_nongenetic_infOnly_1   
Result: Total elapsed time for Bolt-lmm-inf = 7812.38 sec   