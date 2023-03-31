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