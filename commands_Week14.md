# Week 14

## MR MEGA
### BOLT
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/MR-MEGA_v0.2/MR-MEGA -i mr_mega_Bolt.in -o mr_mega_out_Bolt --name_pos BP --name_chr CHR  --name_beta BETA  --name_se SE  --name_ea ALLELE1  --name_eaf A1FREQ  --name_nea ALLELE0  --pc 3
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
--name_pos Basepair --name_chr Chromosome  --name_beta BETA  --name_se SE  --name_ea ALLELE1  --name_eaf A1FREQ  --name_nea ALLELE0  
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
  --phenoFile ${dir}/height1.pheno \
  --covarFile ${dir}/covar_PC.covars \
  --covarCol PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --out ${dir}/Real_Traits/Height/data_qc_regenie_height_s1  


regenie \
  --step 2 \
  --bgen ${dir}/data_qc.bgen \
  --phenoFile ${dir}/height1.pheno \
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

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/height1.pheno  --covarFile=${dir}/covar_PC.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/Height/data_qc_Bolt_height

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

${dir}/software/ldak5.XXX --pheno ${dir}/height.pheno  --covar ${dir}/covar_PC.covars --max-threads 4  --bfile ${dir}/data_qc --linear ${dir}/Real_Traits/Height/data_qc_ldak_height

" > ${dir}/scripts/Real_Traits/Height/data_qc_ldak_height

# I am doing blabla
cd ${dir}/scripts/Real_Traits/Height/
sbatch data_qc_ldak_height
```