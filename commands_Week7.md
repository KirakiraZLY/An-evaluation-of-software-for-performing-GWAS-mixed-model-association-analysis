# Week 7
2023/3/27 - 2023/3/30

### Bolt non-genetic inf only
To check the time effiency.   
It is an approximation method using 30 pseudorandom SNPs to get mean value.  

In the analysis below, I tested nongenetic traits on 66688 individuals with 300K SNPs.   
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/type_1_error/non_genetic_trait_quant_1.pheno --phenoCol=Phenotype \
--covarFile=${dir}/covar_PC.covars \ 
  --lmmInfOnly  --LDscoresUseChip --statsFile=${dir}/type_1_error/data_bolt_inf_whole_nongenetic_result.Bolt
```
Location: type_1_error   
Script: ${dir}/scriptsbolt_ukbb_nongenetic_infOnly_1   
It shows that the result from inf is not significantly different from Bolt-lmm.   

## Regenie by different Parameters
Performance and Time complexity
### Bsize = 500, J = 10
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/type_1_error/non_genetic_trait_quant_1.pheno \
  --bsize 100 \
  --out ${dir}/type_1_error_new/data_regenie_whole_nongenetic_B500J10_out_1   
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen: ./software/plink2 --bfile data_qc --export bgen-1.2 --out data_qc   
**Output**: data_regenie_whole_nongenetic_B500J10_out_1_pred.list
2. 
```python
  regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --covarFile ${dir}/covar1.covars \
  --phenoFile ${dir}/type_1_error/non_genetic_trait_quant_1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ${dir}/type_1_error/data_regenie_whole_nongenetic_out_1_pred.list \
  --out ${dir}/type_1_error/data_regenie_whole_nongenetic_out_2_firth
```
Output: data_regenie_whole_nongenetic_out_2_firth.regenie
Script: ${dir}/scripts/bolt_ukbb_nongenetic_infOnly_1   
Result: Total elapsed time for Bolt-lmm-inf = 7812.38 sec   

## Power test using simulated traits
### SNP list
See ${dir}/Power folder, snp_power_test_list.txt   
### h2 0.1, 0.5, 0.9 三个档
To simulate quantitative traits of UKBB 66688 individuals, with h2 = 0.1, causal = 1000.   
```python
  dir="/home/lezh/dsmwpred/zly"
  echo "#"'!'"/bin/bash
#SBATCH --mem 64G
#SBATCH -t 30:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"
source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/ldak5.XXX \
  --make-phenos ${dir}/Power/h2_01/trait_quant_h2_01_1 \
  --bfile ${dir}/data_qc \
  --ignore-weights YES \
  --power -1 \
  --her 0.1 \
  --num-phenos 1 \
  --num-causals 1000 \
  --causals ${dir}/Power/snp_power_test_list.txt

" > ${dir}/scripts/Power/h2_01/trait_quant_h2_01_log

cd ${dir}/scripts/Power/h2_01/
sbatch trait_quant_h2_01_log
```  

To simulate quantitative traits of UKBB 66688 individuals, with h2 = 0.5, causal = 1000.   
```python
dir="/home/lezh/dsmwpred/zly"
  echo "#"'!'"/bin/bash
#SBATCH --mem 64G
#SBATCH -t 30:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"
source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/ldak5.XXX \
  --make-phenos ${dir}/Power/h2_05/trait_quant_h2_05_1 \
  --bfile ${dir}/data_qc \
  --ignore-weights YES \
  --power -1 \
  --her 0.5 \
  --num-phenos 1 \
  --num-causals 1000 \
  --causals ${dir}/Power/snp_power_test_list.txt

" > ${dir}/scripts/Power/h2_05/trait_quant_h2_05_log

cd ${dir}/scripts/Power/h2_05/
sbatch trait_quant_h2_05_log
```  
To simulate quantitative traits of UKBB 66688 individuals, with h2 = 0.9, causal = 1000.   
```python
dir="/home/lezh/dsmwpred/zly"
  echo "#"'!'"/bin/bash
#SBATCH --mem 64G
#SBATCH -t 30:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"
source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/ldak5.XXX \
  --make-phenos ${dir}/Power/h2_09/trait_quant_h2_09_1 \
  --bfile ${dir}/data_qc \
  --ignore-weights YES \
  --power -1 \
  --her 0.9 \
  --num-phenos 1 \
  --num-causals 1000 \
  --causals ${dir}/Power/snp_power_test_list.txt

" > ${dir}/scripts/Power/h2_09/trait_quant_h2_09_log

cd ${dir}/scripts/Power/h2_09/
sbatch trait_quant_h2_09_log
```  


## Power test by different softwares
### h2 = 0.1
### Regenie
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/Power/h2_01/trait_quant_h2_01_1_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --bsize 1000 \
  --out ${dir}/Power/h2_01/data_regenie_whole_h201Power_out_1   
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen: ./software/plink2 --bfile data_qc --export bgen-1.2 --out data_qc   
**Output**: data_regenie_whole_h201Power_out_1.list
2. 
```python
  regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --covarFile ${dir}/covar_PC.covars \
  --phenoFile ${dir}/Power/h2_01/trait_quant_h2_01_1_label.pheno \
  --bsize 1000 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/Power/h2_01/data_regenie_whole_h201Power_out_1.list \
  --out ${dir}/Power/h2_01/data_regenie_whole_Power01_out_2
```
Output: data_regenie_whole_Power01_out_2.regenie

### Bolt
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc \
--phenoFile=${dir}/Power/h2_01/trait_quant_h2_01_1_label.pheno  --phenoCol=Phenotype --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:20} \ 
 --lmmForceNonInf --LDscoresUseChip \ 
 --statsFile=${dir}/Power/h2_01/data_bolt_whole_Power01_out.Bolt
```

### Bolt-inf
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc \
--phenoFile=${dir}/Power/h2_01/trait_quant_h2_01_1_label.pheno  --phenoCol=Phenotype --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:20} \ 
 --lmmInfOnly --LDscoresUseChip \ 
 --statsFile=${dir}/Power/h2_01/data_bolt_inf_whole_Power01_out.Bolt
```


### fastGWA
第一步和第二步是与phenotype无关的，就不操作，只操作第三步。   
3. I didn't use PCs
```python
${dir}/software/gcta \
--bfile ${dir}/data_qc \
--grm-sparse ${dir}/type_1_error/data_qc_nongenetic_gcta_grm_2 \
--fastGWA-mlm \
--qcovar ${dir}/covar_PC_withoutLabel.covars \
--pheno ${dir}/Power/h2_01/trait_quant_h2_01_1.pheno \
--thread-num 10 \
--out ${dir}/Power/h2_01/data_fastgwa_Power01_3_finalresult 
```

### Plink
assoc test   
```python
${dir}/software/plink \
--bfile ${dir}/data_qc \
--linear \
--covar ${dir}/covar_PC_withoutLabel.covars \
--pheno ${dir}/Power/h2_01/trait_quant_h2_01_1.pheno --allow-no-sex \
--out ${dir}/Power/h2_01/data_plink_Power01_finalresult 
```

### LDAK
Quant   
```python
${dir}/software/ldak5.XXX \
--pheno ${dir}/Power/h2_01/trait_quant_h2_01_1.pheno \
--covar ${dir}/covar_PC_withoutLabel.covars \
--bfile ${dir}/data_qc \
--linear ${dir}/Power/h2_01/data_ldak_whole_Power01_result
```

## h2 = 0.5
### Regenie
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/Power/h2_05/trait_quant_h2_05_1_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:20} \
  --bsize 1000 \
  --out ${dir}/Power/h2_05/data_regenie_whole_h205Power_out_1   
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen: ./software/plink2 --bfile data_qc --export bgen-1.2 --out data_qc   
**Output**: data_regenie_whole_h205Power_out_1.list
2. 
```python
  regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:20} \
  --phenoFile ${dir}/Power/h2_05/trait_quant_h2_05_1_label.pheno \
  --bsize 1000 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/Power/h2_05/data_regenie_whole_h205Power_out_1.list \
  --out ${dir}/type_1_error/h2_05/data_regenie_whole_Power05_out_2
```
Output: data_regenie_whole_Power05_out_2.regenie

### Bolt
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/Power/h2_05/trait_quant_h2_05_1_label.pheno  --phenoCol=Phenotype --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:20}   --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/Power/h2_05/data_bolt_whole_Power05_out.Bolt
```

### Bolt-inf
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/Power/h2_05/trait_quant_h2_05_1_label.pheno  --phenoCol=Phenotype --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:20} --lmmInfOnly --LDscoresUseChip --statsFile=${dir}/Power/h2_05/data_bolt_inf_whole_Power05_out.Bolt
```

### fastGWA
第一步和第二步是与phenotype无关的，就不操作，只操作第三步。   
```python
${dir}/software/gcta \
--bfile ${dir}/data_qc \
--grm-sparse ${dir}/type_1_error/data_qc_nongenetic_gcta_grm_2 \
--fastGWA-mlm \
--qcovar ${dir}/covar_PC_withoutLabel.covars \
--pheno ${dir}/Power/h2_05/trait_quant_h2_05_1.pheno \
--thread-num 10 \
--out ${dir}/Power/h2_05/data_fastgwa_Power05_3_finalresult 
```

### Plink
assoc test   
```python
${dir}/software/plink \
--bfile ${dir}/data_qc \
--linear \
--covar ${dir}/covar_PC_withoutLabel.covars \
--pheno ${dir}/Power/h2_05/trait_quant_h2_05_1.pheno --allow-no-sex \
--out ${dir}/Power/h2_05/data_plink_Power05_finalresult 
```

### LDAK
Quant   
```python
${dir}/software/ldak5.XXX \
--pheno ${dir}/Power/h2_05/trait_quant_h2_05_1.pheno \
--covar ${dir}/covar_PC_withoutLabel.covars \
--bfile ${dir}/data_qc \
--linear ${dir}/Power/h2_05/data_ldak_whole_Power05_result
```


## h2 = 0.9
### Regenie
1. 
```python
   regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/Power/h2_09/trait_quant_h2_09_1_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:20} \
  --bsize 1000 \
  --out ${dir}/Power/h2_09/data_regenie_whole_h209Power_out_1   
```
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen: ./software/plink2 --bfile data_qc --export bgen-1.2 --out data_qc   
**Output**: data_regenie_whole_h209Power_out_1.list
2. 
```python
  regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:20} \
  --phenoFile ${dir}/Power/h2_09/trait_quant_h2_09_1_label.pheno \
  --bsize 1000 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/Power/h2_09/data_regenie_whole_h209Power_out_1.list \
  --out ${dir}/type_1_error/h2_09/data_regenie_whole_Power09_out_2
```
Output: data_regenie_whole_Power09_out_2.regenie

### Bolt
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/Power/h2_09/trait_quant_h2_09_1_label.pheno  --phenoCol=Phenotype --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:20} --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/Power/h2_09/data_bolt_whole_Power09_out.Bolt
```

### Bolt-inf
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/Power/h2_09/trait_quant_h2_09_1_label.pheno  --phenoCol=Phenotype --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:20} --lmmInfOnly --LDscoresUseChip --statsFile=${dir}/Power/h2_09/data_bolt_inf_whole_Power09_out.Bolt
```

### fastGWA
第一步和第二步是与phenotype无关的，就不操作，只操作第三步。   
```python
${dir}/software/gcta \
--bfile ${dir}/data_qc \
--grm-sparse ${dir}/type_1_error/data_qc_nongenetic_gcta_grm_2 \
--fastGWA-mlm \
--qcovar ${dir}/covar_PC_withoutLabel.covars \
--pheno ${dir}/Power/h2_09/trait_quant_h2_09_1.pheno \
--thread-num 10 \
--out ${dir}/Power/h2_09/data_fastgwa_Power09_3_finalresult 
```

### Plink
assoc test   
```python
${dir}/software/plink \
--bfile ${dir}/data_qc \
--linear \
--covar ${dir}/covar_PC_withoutLabel.covars \
--pheno ${dir}/Power/h2_09/trait_quant_h2_09_1.pheno --allow-no-sex \
--out ${dir}/Power/h2_09/data_plink_Power09_finalresult 
```

### LDAK
Quant   
```python
${dir}/software/ldak5.XXX \
--pheno ${dir}/Power/h2_09/trait_quant_h2_09_1.pheno \
--covar ${dir}/covar_PC_withoutLabel.covars \
--bfile ${dir}/data_qc \
--linear ${dir}/Power/h2_09/data_ldak_whole_Power09_result
```