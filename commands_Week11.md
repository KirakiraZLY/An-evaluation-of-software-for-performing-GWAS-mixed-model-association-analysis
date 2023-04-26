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
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink --bfile ${dir}/data_1Wan --geno 0.1 --mind 0.1 --maf 0.05 --mac 100 --make-bed --out ${dir}/data_1Wan
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

Step 3
```python
${dir}/software/gcta --bfile ${dir}/data_1Wan \
--grm-sparse ${dir}/data_1Wan_gcta_2 \
--fastGWA-mlm \
--pheno ${dir}/type_1_error/Multi_Traits/Trait_13_to_24/Trait_$i.pheno \
--qcovar ${dir}/covar_1Wan_PC.covars \
--out type_1_error/Multi_Traits/Trait_13_to_24/Result_Trait$i/Result_fastGWA_Trait$i \
--thread-num 10
```





### For 70K individuals, using fastGWA
前两步  只用进行一次
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/gcta \
--bfile ${dir}/data_qc \
--autosome --maf 0.01 \
--make-grm --out ${dir}/data_qc_gcta_1 \
--thread-num 10

${dir}/software/gcta \
--grm ${dir}/data_qc_gcta_1 --make-bK-sparse 0.05 \
--out ${dir}/data_qc_gcta_2  \
--thread-num 10
```

Step 3
```python
${dir}/software/gcta --bfile ${dir}/data_qc \
--grm-sparse ${dir}/data_qc_gcta_2 \
--fastGWA-mlm \
--pheno ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_$i.pheno \
--qcovar ${dir}/covar_PC.covars \
--out type_1_error/Multi_Traits/Trait_25_to_48_Binary/Result_Trait$i/Result_fastGWA_Trait$i \
--thread-num 10
```


## fastGWA
Require to use 10 cores.   


## data_Black QC
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink --bfile ${dir}/MAMA/Bolt_Height/data_Black --geno 0.1 --mind 0.1 --maf 0.05 --mac 100 --make-bed --out ${dir}/data_Black
```

## data_Black .bgen
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink2 --bfile ${dir}/data_Black --export bgen-1.2 --out ${dir}/data_Black
```

##
Re-generate covar_Black_PC
For fastGWA, generate data_Black_gcta_1 and data_Black_gcta_2





# Meta-analysis
## 1. Copy 5 region data into folder
## 2. QC on 5 regions
### data_Black QC
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink --bfile ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_Black --geno 0.1 --mind 0.1 --maf 0.05 --mac 100 --make-bed --out ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_Black
```
### data_Black .bgen
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink2 --bfile ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_Black --export bgen-1.2 --out ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_Black
```
### data_White QC
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink --bfile ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_White --geno 0.1 --mind 0.1 --maf 0.05 --mac 100 --make-bed --out ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_White
```
### data_White .bgen
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink2 --bfile ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_White --export bgen-1.2 --out ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_White
```
### data_Chinese QC
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink --bfile ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_Chinese --geno 0.1 --mind 0.1 --maf 0.05 --mac 100 --make-bed --out ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_Chinese
```
### data_Chinese .bgen
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink2 --bfile ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_Chinese --export bgen-1.2 --out ${dir}/data_Black
```
### data_AsianSWC QC
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink --bfile ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_AsianSWC --geno 0.1 --mind 0.1 --maf 0.05 --mac 100 --make-bed --out ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_AsianSWC
```
### data_AsianSWC .bgen
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink2 --bfile ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_AsianSWC --export bgen-1.2 --out ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_AsianSWC
```
### data_Mixed QC
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink --bfile ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_Mixed --geno 0.1 --mind 0.1 --maf 0.05 --mac 100 --make-bed --out ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_Mixed
```
### data_Mixed .bgen
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink2 --bfile ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_Mixed --export bgen-1.2 --out ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/data_Mixed
```

## 3. Extract SNP_1_to_12
See in computer
## 4. Generate Phenotypes * 5

## 5. LDAK assoc test

## 6. METAL in each folder(metal_LDAK.txt)
