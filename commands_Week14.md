# Week 14

## MR MEGA
### BOLT
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/MR-MEGA_v0.2/MR-MEGA -i ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/T1/mr_mega_Bolt.in -o ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/T1/mr_mega_out_Bolt.out --name_pos BP --name_chr CHR  --name_beta BETA  --name_se SE  --name_ea ALLELE1  --name_eaf A1FREQ  --name_nea ALLELE0  --pc 3 --name_marker SNP  --qt --name_n SampleSize
```
### mr-mega.in
```python
Result_Bolt_AsianSWC_P1.Bolt
Result_Bolt_Black_P1.Bolt
Result_Bolt_Chinese_P1.Bolt
Result_Bolt_Mixed_P1.Bolt
Result_Bolt_White_P1.Bolt
```

```
Result_Bolt_AsianSWC_P2.Bolt
Result_Bolt_Black_P2.Bolt
Result_Bolt_Chinese_P2.Bolt
Result_Bolt_Mixed_P2.Bolt
Result_Bolt_White_P2.Bolt
```

```
Result_Bolt_AsianSWC_P3.Bolt
Result_Bolt_Black_P3.Bolt
Result_Bolt_Chinese_P3.Bolt
Result_Bolt_Mixed_P3.Bolt
Result_Bolt_White_P3.Bolt
```

```
Result_Bolt_AsianSWC_P4.Bolt
Result_Bolt_Black_P4.Bolt
Result_Bolt_Chinese_P4.Bolt
Result_Bolt_Mixed_P4.Bolt
Result_Bolt_White_P4.Bolt
```

```
Result_Bolt_AsianSWC_P5.Bolt
Result_Bolt_Black_P5.Bolt
Result_Bolt_Chinese_P5.Bolt
Result_Bolt_Mixed_P5.Bolt
Result_Bolt_White_P5.Bolt
```

### LDAK
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/MR-MEGA_v0.2/MR-MEGA -i mr_mega_Regenie.in -o mr_mega_out_Regenie —pc 3 \
--name_pos Basepair --name_chr Chromosome  --name_marker  Predictor  --name_beta BETA  --name_se SE  --name_ea ALLELE1  --name_eaf A1FREQ  --name_nea ALLELE0  --qt
```

```python
Result_LDAK_AsianSWC_P1.assoc
Result_LDAK_Black_P1.assoc
Result_LDAK_Chinese_P1.assoc
Result_LDAK_Mixed_P1.assoc
Result_LDAK_White_P1.assoc
```


```
Result_LDAK_AsianSWC_P2.assoc
Result_LDAK_Black_P2.assoc
Result_LDAK_Chinese_P2.assoc
Result_LDAK_Mixed_P2.assoc
Result_LDAK_White_P2.assoc
```


```
Result_LDAK_AsianSWC_P3.assoc
Result_LDAK_Black_P3.assoc
Result_LDAK_Chinese_P3.assoc
Result_LDAK_Mixed_P3.assoc
Result_LDAK_White_P3.assoc
```


```
Result_LDAK_AsianSWC_P4.assoc
Result_LDAK_Black_P4.assoc
Result_LDAK_Chinese_P4.assoc
Result_LDAK_Mixed_P4.assoc
Result_LDAK_White_P4.assoc
```

```
Result_LDAK_AsianSWC_P5.assoc
Result_LDAK_Black_P5.assoc
Result_LDAK_Chinese_P5.assoc
Result_LDAK_Mixed_P5.assoc
Result_LDAK_White_P5.assoc
```




# Real Traits
## Height
### Regenie Height
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 4:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred

source /home/lezh/miniconda3/etc/profile.d/conda.sh
conda activate regenie_env

regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/Phenotype_UKBB/height_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --out ${dir}/Real_Traits/Height/data_qc_regenie_height_s1  


regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --phenoFile ${dir}/Phenotype_UKBB/height_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/Real_Traits/Height/data_qc_regenie_height_s1_pred.list \
  --out ${dir}/Real_Traits/Height/data_qc_regenie_height_s2

" > ${dir}/scripts/Real_Traits/Height/data_qc_regenie_height


# I am doing blabla
cd ${dir}/scripts/Real_Traits/Height/
sbatch data_qc_regenie_height

```
### Bolt Height
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 8:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"


source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/Phenotype_UKBB/height_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/Height/data_qc_Bolt_height

" > ${dir}/scripts/Real_Traits/Height/data_qc_Bolt_height


# I am doing blabla
cd ${dir}/scripts/Real_Traits/Height/

sbatch data_qc_Bolt_height
```


### LDAK run Height
result in ${dir}/Real_Traits/Height
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 2:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"

source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/ldak5.XXX --pheno ${dir}/Phenotype_UKBB/height.pheno  --covar ${dir}/covar_PC.covars --max-threads 4  --bfile ${dir}/data_qc --linear ${dir}/Real_Traits/Height/data_qc_ldak_height

" > ${dir}/scripts/Real_Traits/Height/data_qc_ldak_height

# I am doing blabla
cd ${dir}/scripts/Real_Traits/Height/
sbatch data_qc_ldak_height
```



## bmi
### Regenie bmi
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 4:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred

source /home/lezh/miniconda3/etc/profile.d/conda.sh
conda activate regenie_env

regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/Phenotype_UKBB/bmi_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --out ${dir}/Real_Traits/bmi/data_qc_regenie_bmi_s1  


regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --phenoFile ${dir}/Phenotype_UKBB/bmi_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/Real_Traits/bmi/data_qc_regenie_bmi_s1_pred.list \
  --out ${dir}/Real_Traits/bmi/data_qc_regenie_bmi_s2

" > ${dir}/scripts/Real_Traits/bmi/data_qc_regenie_bmi


# I am doing blabla
cd ${dir}/scripts/Real_Traits/bmi/
sbatch data_qc_regenie_bmi

```
### Bolt bmi
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 8:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"


source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/Phenotype_UKBB/bmi_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/bmi/data_qc_Bolt_bmi

" > ${dir}/scripts/Real_Traits/bmi/data_qc_Bolt_bmi


# I am doing blabla
cd ${dir}/scripts/Real_Traits/bmi/

sbatch data_qc_Bolt_bmi
```


### LDAK run bmi
result in ${dir}/Real_Traits/bmi
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 2:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"

source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/ldak5.XXX --pheno ${dir}/Phenotype_UKBB/bmi.pheno  --covar ${dir}/covar_PC.covars --max-threads 4  --bfile ${dir}/data_qc --linear ${dir}/Real_Traits/bmi/data_qc_ldak_bmi

" > ${dir}/scripts/Real_Traits/bmi/data_qc_ldak_bmi

# I am doing blabla
cd ${dir}/scripts/Real_Traits/bmi/
sbatch data_qc_ldak_bmi
```




## alkaline
### Regenie alkaline
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 4:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred

source /home/lezh/miniconda3/etc/profile.d/conda.sh
conda activate regenie_env

regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/Phenotype_UKBB/alkaline_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --out ${dir}/Real_Traits/alkaline/data_qc_regenie_alkaline_s1  


regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --phenoFile ${dir}/Phenotype_UKBB/alkaline_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/Real_Traits/alkaline/data_qc_regenie_alkaline_s1_pred.list \
  --out ${dir}/Real_Traits/alkaline/data_qc_regenie_alkaline_s2

" > ${dir}/scripts/Real_Traits/alkaline/data_qc_regenie_alkaline


# I am doing blabla
cd ${dir}/scripts/Real_Traits/alkaline/
sbatch data_qc_regenie_alkaline

```
### Bolt alkaline
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 8:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"


source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/Phenotype_UKBB/alkaline_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/alkaline/data_qc_Bolt_alkaline

" > ${dir}/scripts/Real_Traits/alkaline/data_qc_Bolt_alkaline


# I am doing blabla
cd ${dir}/scripts/Real_Traits/alkaline/

sbatch data_qc_Bolt_alkaline
```


### LDAK run alkaline
result in ${dir}/Real_Traits/alkaline
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 2:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"

source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/ldak5.XXX --pheno ${dir}/Phenotype_UKBB/alkaline.pheno  --covar ${dir}/covar_PC.covars --max-threads 4  --bfile ${dir}/data_qc --linear ${dir}/Real_Traits/alkaline/data_qc_ldak_alkaline

" > ${dir}/scripts/Real_Traits/alkaline/data_qc_ldak_alkaline

# I am doing blabla
cd ${dir}/scripts/Real_Traits/alkaline/
sbatch data_qc_ldak_alkaline
```



## urate
### Regenie urate
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 4:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred

source /home/lezh/miniconda3/etc/profile.d/conda.sh
conda activate regenie_env

regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/Phenotype_UKBB/urate_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --out ${dir}/Real_Traits/urate/data_qc_regenie_urate_s1  


regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --phenoFile ${dir}/Phenotype_UKBB/urate_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/Real_Traits/urate/data_qc_regenie_urate_s1_pred.list \
  --out ${dir}/Real_Traits/urate/data_qc_regenie_urate_s2

" > ${dir}/scripts/Real_Traits/urate/data_qc_regenie_urate


# I am doing blabla
cd ${dir}/scripts/Real_Traits/urate/
sbatch data_qc_regenie_urate

```
### Bolt urate
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 8:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"


source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/Phenotype_UKBB/urate_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/urate/data_qc_Bolt_urate

" > ${dir}/scripts/Real_Traits/urate/data_qc_Bolt_urate


# I am doing blabla
cd ${dir}/scripts/Real_Traits/urate/

sbatch data_qc_Bolt_urate
```


### LDAK run urate
result in ${dir}/Real_Traits/urate
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 2:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"

source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/ldak5.XXX --pheno ${dir}/Phenotype_UKBB/urate.pheno  --covar ${dir}/covar_PC.covars --max-threads 4  --bfile ${dir}/data_qc --linear ${dir}/Real_Traits/urate/data_qc_ldak_urate

" > ${dir}/scripts/Real_Traits/urate/data_qc_ldak_urate

# I am doing blabla
cd ${dir}/scripts/Real_Traits/urate/
sbatch data_qc_ldak_urate
```


## bilirubin
### Regenie bilirubin
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 4:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred

source /home/lezh/miniconda3/etc/profile.d/conda.sh
conda activate regenie_env

regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/Phenotype_UKBB/bilirubin_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --out ${dir}/Real_Traits/bilirubin/data_qc_regenie_bilirubin_s1  


regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --phenoFile ${dir}/Phenotype_UKBB/bilirubin_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/Real_Traits/bilirubin/data_qc_regenie_bilirubin_s1_pred.list \
  --out ${dir}/Real_Traits/bilirubin/data_qc_regenie_bilirubin_s2

" > ${dir}/scripts/Real_Traits/bilirubin/data_qc_regenie_bilirubin


# I am doing blabla
cd ${dir}/scripts/Real_Traits/bilirubin/
sbatch data_qc_regenie_bilirubin

```
### Bolt bilirubin
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 8:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"


source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/Phenotype_UKBB/bilirubin_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/bilirubin/data_qc_Bolt_bilirubin

" > ${dir}/scripts/Real_Traits/bilirubin/data_qc_Bolt_bilirubin


# I am doing blabla
cd ${dir}/scripts/Real_Traits/bilirubin/

sbatch data_qc_Bolt_bilirubin
```


### LDAK run bilirubin
result in ${dir}/Real_Traits/bilirubin
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 2:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"

source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/ldak5.XXX --pheno ${dir}/Phenotype_UKBB/bilirubin.pheno  --covar ${dir}/covar_PC.covars --max-threads 4  --bfile ${dir}/data_qc --linear ${dir}/Real_Traits/bilirubin/data_qc_ldak_bilirubin

" > ${dir}/scripts/Real_Traits/bilirubin/data_qc_ldak_bilirubin

# I am doing blabla
cd ${dir}/scripts/Real_Traits/bilirubin/
sbatch data_qc_ldak_bilirubin
```


## cholesterol
### Regenie cholesterol
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 4:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred

source /home/lezh/miniconda3/etc/profile.d/conda.sh
conda activate regenie_env

regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/Phenotype_UKBB/cholesterol_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --out ${dir}/Real_Traits/cholesterol/data_qc_regenie_cholesterol_s1  


regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --phenoFile ${dir}/Phenotype_UKBB/cholesterol_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/Real_Traits/cholesterol/data_qc_regenie_cholesterol_s1_pred.list \
  --out ${dir}/Real_Traits/cholesterol/data_qc_regenie_cholesterol_s2

" > ${dir}/scripts/Real_Traits/cholesterol/data_qc_regenie_cholesterol


# I am doing blabla
cd ${dir}/scripts/Real_Traits/cholesterol/
sbatch data_qc_regenie_cholesterol

```
### Bolt cholesterol
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 8:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"


source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/Phenotype_UKBB/cholesterol_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/cholesterol/data_qc_Bolt_cholesterol

" > ${dir}/scripts/Real_Traits/cholesterol/data_qc_Bolt_cholesterol


# I am doing blabla
cd ${dir}/scripts/Real_Traits/cholesterol/

sbatch data_qc_Bolt_cholesterol
```


### LDAK run cholesterol
result in ${dir}/Real_Traits/cholesterol
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 2:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"

source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/ldak5.XXX --pheno ${dir}/Phenotype_UKBB/cholesterol.pheno  --covar ${dir}/covar_PC.covars --max-threads 4  --bfile ${dir}/data_qc --linear ${dir}/Real_Traits/cholesterol/data_qc_ldak_cholesterol

" > ${dir}/scripts/Real_Traits/cholesterol/data_qc_ldak_cholesterol

# I am doing blabla
cd ${dir}/scripts/Real_Traits/cholesterol/
sbatch data_qc_ldak_cholesterol
```



## hba1c
### Regenie hba1c
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 4:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred

source /home/lezh/miniconda3/etc/profile.d/conda.sh
conda activate regenie_env

regenie \
  --step 1 \
  --bed ${dir}/data_qc \
  --phenoFile ${dir}/Phenotype_UKBB/hba1c_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --out ${dir}/Real_Traits/hba1c/data_qc_regenie_hba1c_s1  


regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --phenoFile ${dir}/Phenotype_UKBB/hba1c_label.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/Real_Traits/hba1c/data_qc_regenie_hba1c_s1_pred.list \
  --out ${dir}/Real_Traits/hba1c/data_qc_regenie_hba1c_s2

" > ${dir}/scripts/Real_Traits/hba1c/data_qc_regenie_hba1c


# I am doing blabla
cd ${dir}/scripts/Real_Traits/hba1c/
sbatch data_qc_regenie_hba1c

```
### Bolt hba1c
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 8:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"


source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/Phenotype_UKBB/hba1c_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/hba1c/data_qc_Bolt_hba1c

" > ${dir}/scripts/Real_Traits/hba1c/data_qc_Bolt_hba1c


# I am doing blabla
cd ${dir}/scripts/Real_Traits/hba1c/

sbatch data_qc_Bolt_hba1c
```


### LDAK run hba1c
result in ${dir}/Real_Traits/hba1c
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 2:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"

source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/ldak5.XXX --pheno ${dir}/Phenotype_UKBB/hba1c.pheno  --covar ${dir}/covar_PC.covars --max-threads 4  --bfile ${dir}/data_qc --linear ${dir}/Real_Traits/hba1c/data_qc_ldak_hba1c

" > ${dir}/scripts/Real_Traits/hba1c/data_qc_ldak_hba1c

# I am doing blabla
cd ${dir}/scripts/Real_Traits/hba1c/
sbatch data_qc_ldak_hba1c
```


# White -> .bgen
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink2 --bfile ${dir}/data_White --export bgen-1.2 --out ${dir}/data_White
```



# Meta-analysis
## Metal
```python
./metal metal_BOLT_P1.txt 
./metal metal_BOLT_P2.txt 
./metal metal_BOLT_P3.txt 
./metal metal_BOLT_P4.txt 
./metal metal_BOLT_P5.txt 

./metal metal_LDAK_P1.txt 
./metal metal_LDAK_P2.txt 
./metal metal_LDAK_P3.txt 
./metal metal_LDAK_P4.txt 
./metal metal_LDAK_P5.txt 

```


## MR MEGA
### BOLT
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/MR-MEGA_v0.2/MR-MEGA -i ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/T1/mr_mega_Bolt.in -o ${dir}/type_1_error/Multi_Traits/META_ANALYSIS/T1/mr_mega_out_Bolt.out --name_pos BP --name_chr CHR  --name_beta BETA  --name_se SE  --name_ea ALLELE1  --name_eaf A1FREQ  --name_nea ALLELE0  --pc 3 --name_marker SNP  --qt --name_n SampleSize
```
### mr-mega.in
```python
Result_Bolt_AsianSWC_P1.Bolt
Result_Bolt_Black_P1.Bolt
Result_Bolt_Chinese_P1.Bolt
Result_Bolt_Mixed_P1.Bolt
Result_Bolt_White_P1.Bolt
```

```
Result_Bolt_AsianSWC_P2.Bolt
Result_Bolt_Black_P2.Bolt
Result_Bolt_Chinese_P2.Bolt
Result_Bolt_Mixed_P2.Bolt
Result_Bolt_White_P2.Bolt
```

```
Result_Bolt_AsianSWC_P3.Bolt
Result_Bolt_Black_P3.Bolt
Result_Bolt_Chinese_P3.Bolt
Result_Bolt_Mixed_P3.Bolt
Result_Bolt_White_P3.Bolt
```

```
Result_Bolt_AsianSWC_P4.Bolt
Result_Bolt_Black_P4.Bolt
Result_Bolt_Chinese_P4.Bolt
Result_Bolt_Mixed_P4.Bolt
Result_Bolt_White_P4.Bolt
```

```
Result_Bolt_AsianSWC_P5.Bolt
Result_Bolt_Black_P5.Bolt
Result_Bolt_Chinese_P5.Bolt
Result_Bolt_Mixed_P5.Bolt
Result_Bolt_White_P5.Bolt
```
