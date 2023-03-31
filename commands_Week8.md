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

```python
${dir}/software/ldak5.XXX \
  --make-phenos ${dir}/Power/h2_01/trait_quant_h2_01_1 \
  --bfile ${dir}/data_qc \
  --ignore-weights YES \
  --power -1 \
  --her 0.1 \
  --num-phenos 1 \
  --num-causals 1000 \
  --causals ${dir}/Power/snp_power_test_list.txt
```