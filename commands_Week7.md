# Week 7

### Bolt non-genetic inf only
To check the time effiency.   
It is an approximation method using 30 pseudorandom SNPs to get mean value.   
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/type_1_error/non_genetic_trait_quant_1.pheno --phenoCol=Phenotype --lmmInfOnly  --LDscoresUseChip --statsFile=${dir}/type_1_error/data_bolt_inf_whole_nongenetic_result.Bolt
```
Location: type_1_error