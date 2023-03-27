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

## Power test using simulated traits
### h2 0.1, 0.5, 0.9 三个档
To simulate quantitative traits of UKBB 66688 individuals, with h2 = 0.1, causal = 1000.   
```python
  dir="/home/lezh/dsmwpred/zly"
${dir}/software/ldak5.XXX \
  --make-phenos data_her01_causal1000 \
  --bfile data_qc \
  --prevalence 0.1 \
  --ignore-weights YES \
  --power -1 \
  --her 0.1 \
  --num-phenos 1 \
  --num-causals 1000
```  