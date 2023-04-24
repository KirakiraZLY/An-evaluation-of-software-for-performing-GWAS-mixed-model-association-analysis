# Week 11

## Low MAC list --extract
7Wan
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink \
  --bfile ${dir}/data_qc \
  --mac 100 \
  --write-snplist \
  --out ${dir}/snps_pass_data_qc
```

1Wan
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink \
  --bfile ${dir}/data_1Wan \
  --mac 100 \
  --write-snplist \
  --out ${dir}/snps_pass_1Wan
```

## 1 Wan QC
```python
${dir}/software/plink --bfile ${dir}/data_1Wan --geno 0.1 --mind 0.1 --maf 0.05 --mac 100 --make-bed --out ${dir}/data_1Wan
```