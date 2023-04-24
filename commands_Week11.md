# Week 11

## Low MAC list --extract
70K
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink \
  --bfile ${dir}/data_qc \
  --mac 100 \
  --write-snplist \
  --out ${dir}/snps_pass_data_qc
```