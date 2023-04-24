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
${dir}/software/plink --bfile ${dir}/data_1Wan --geno 0.1 --mind 0.1 --maf 0.05 --mac 1000 --make-bed --out ${dir}/data_1Wan
```

## 1 Wan .bgen
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink2 --bfile ${dir}/data_1Wan --export bgen-1.2 --out ${dir}/data_1Wan
```

### For 10K individuals, using fastGWA
前两步  只用进行一次
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/gcta \
--bfile ${dir}/data_1Wan \
--autosome --maf 0.01 \
--make-grm --out ${dir}/data_1Wan_gcta_1 \
--thread-num 4

${dir}/software/gcta \
--grm ${dir}/data_1Wan_gcta_1 --make-bK-sparse 0.05 \
--out ${dir}/data_1Wan_gcta_2  \
--thread-num 4
```

```python
${dir}/software/gcta --bfile ${dir}/data_1Wan \
--grm-sparse ${dir}/data_1Wan_gcta_2 \
--fastGWA-mlm \
--pheno ${dir}/type_1_error/Multi_Traits/Trait_13_to_24/Trait_$i.pheno \
--qcovar ${dir}/covar_1Wan_PC.covars \
--out type_1_error/Multi_Traits/Trait_13_to_24/Result_Trait$i/Result_fastGWA_Trait$i \
--thread-num 10
```