# Week 16
# PRS

## White, 7 traits, Bolt-lmm
### Bolt height
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 8:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"


source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_White --phenoFile=${dir}/Phenotype_UKBB/height_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_White_PC_10.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/Height/data_White_Bolt_height

" > ${dir}/scripts/Real_Traits/Height/data_White_Bolt_height


# I am doing blabla
cd ${dir}/scripts/Real_Traits/Height/

sbatch data_White_Bolt_height
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

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_White --phenoFile=${dir}/Phenotype_UKBB/bmi_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_White_PC_10.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/bmi/data_White_Bolt_bmi

" > ${dir}/scripts/Real_Traits/bmi/data_White_Bolt_bmi


# I am doing blabla
cd ${dir}/scripts/Real_Traits/bmi/

sbatch data_White_Bolt_bmi
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

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_White --phenoFile=${dir}/Phenotype_UKBB/alkaline_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_White_PC_10.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/alkaline/data_White_Bolt_alkaline

" > ${dir}/scripts/Real_Traits/alkaline/data_White_Bolt_alkaline


# I am doing blabla
cd ${dir}/scripts/Real_Traits/alkaline/

sbatch data_White_Bolt_alkaline
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

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_White --phenoFile=${dir}/Phenotype_UKBB/urate_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_White_PC_10.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/urate/data_White_Bolt_urate

" > ${dir}/scripts/Real_Traits/urate/data_White_Bolt_urate


# I am doing blabla
cd ${dir}/scripts/Real_Traits/urate/

sbatch data_White_Bolt_urate
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

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_White --phenoFile=${dir}/Phenotype_UKBB/bilirubin_binary_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_White_PC_10.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/bilirubin/data_White_Bolt_bilirubin_Binary

" > ${dir}/scripts/Real_Traits/bilirubin/data_White_Bolt_bilirubin_Binary


# I am doing blabla
cd ${dir}/scripts/Real_Traits/bilirubin/

sbatch data_White_Bolt_bilirubin_Binary
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

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_White --phenoFile=${dir}/Phenotype_UKBB/cholesterol_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_White_PC_10.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/cholesterol/data_White_Bolt_cholesterol

" > ${dir}/scripts/Real_Traits/cholesterol/data_White_Bolt_cholesterol


# I am doing blabla
cd ${dir}/scripts/Real_Traits/cholesterol/

sbatch data_White_Bolt_cholesterol
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

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_White --phenoFile=${dir}/Phenotype_UKBB/hba1c_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_White_PC_10.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/hba1c/data_White_Bolt_hba1c

" > ${dir}/scripts/Real_Traits/hba1c/data_White_Bolt_hba1c


# I am doing blabla
cd ${dir}/scripts/Real_Traits/hba1c/

sbatch data_White_Bolt_hba1c
```

