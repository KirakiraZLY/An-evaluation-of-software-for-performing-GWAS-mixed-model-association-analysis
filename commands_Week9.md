# Week 9

## Simulate Binary Traits: 25-48
### 25. bi, 7 Wan, GCTA -1, h2=0.1, 5 Phenos, 1K causal

```python
${dir}/software/ldak5.XXX \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_bi_7Wan_GCTA_h01_K_25 \
  --bfile ${dir}/data_qc \
  --ignore-weights YES \
  --power -1 \
  --her 0.1 \
   --prevalence 0 \
  --num-phenos 5 \
  --num-causals 1000 \
  --extract ${dir}/type_1_error/Multi_Traits/snps_1_to_12_7Wan.txt
```