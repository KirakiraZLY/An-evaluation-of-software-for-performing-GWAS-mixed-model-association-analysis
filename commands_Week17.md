# Commands for Master's thesis
## Week 17

### Start by QC(genomeDK, Plink)
Filter out SNPs with genotype missingness >10%, samples with >10% missingness, MAF <5%, minor allele count(MAC) <100, 不做这个HWE p-value exceeding 1e-15.(MAF可以改成1%)   
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink --bfile ${dir}/data --geno 0.005 --mind 0.005 --maf 0.05 --mac 100 --make-bed --out ${dir}/data_qc_nomissing
```  
Output: data_qc   




# qc height
### Regenie height
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
  --bed ${dir}/data_qc_nomissing \
  --phenoFile ${dir}/Phenotype_UKBB/height_label.pheno \
  --covarFile ${dir}/covar_qc_nomissing_PC_10.covars \
  --covarColList Paternal,Sex,PC{1:10} \
  --bsize 1000 \
  --qt \
  --threads 4 \
  --out ${dir}/Real_Traits/height/data_qc_nomissing_regenie_height_s1  


regenie \
  --step 2 \
  --bgen ${dir}/data_qc_nomissing.bgen \
  --phenoFile ${dir}/Phenotype_UKBB/height_label.pheno \
  --covarFile ${dir}/covar_qc_nomissing_PC_10.covars \
  --covarColList Paternal,Sex,PC{1:10} \
  --bsize 1000 \
  --threads 4 \
  --qt \
  --pThresh 0.01 \
  --pred ${dir}/Real_Traits/height/data_qc_nomissing_regenie_height_s1_pred.list \
  --out ${dir}/Real_Traits/height/data_qc_nomissing_regenie_height_s2

" > ${dir}/scripts/Real_Traits/height/data_qc_nomissing_regenie_height


# I am doing blabla
cd ${dir}/scripts/Real_Traits/height/
sbatch data_qc_nomissing_regenie_height

```
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

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc_nomissing --phenoFile=${dir}/Phenotype_UKBB/height_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_qc_nomissing_PC_10.covars --qCovarCol=Paternal --qCovarCol=Sex --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/height/data_qc_nomissing_Bolt_height

" > ${dir}/scripts/Real_Traits/height/data_qc_nomissing_Bolt_height


# I am doing blabla
cd ${dir}/scripts/Real_Traits/height/

sbatch data_qc_nomissing_Bolt_height
```


### LDAK run height
result in ${dir}/Real_Traits/height
```python
dir="/home/lezh/dsmwpred/zly"
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 2:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"

source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir_LDAK} --pheno ${dir}/Phenotype_UKBB/height.pheno  --covar ${dir}/covar_qc_nomissing_PC_10_withoutLabel.covars --max-threads 4  --bfile ${dir}/data_qc_nomissing --linear ${dir}/Real_Traits/height/data_qc_nomissing_ldak_height

" > ${dir}/scripts/Real_Traits/height/data_qc_nomissing_ldak_height

# I am doing blabla
cd ${dir}/scripts/Real_Traits/height/
sbatch data_qc_nomissing_ldak_height
```


## Plink height
```python
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 8:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"

source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/plink --bfile ${dir}/data_qc_nomissing --linear hide-covar --covar ${dir}/covar_qc_nomissing_PC_10_withoutLabel.covars --pheno ${dir}/Phenotype_UKBB/height.pheno --allow-no-sex --out ${dir}/Real_Traits/height/data_qc_nomissing_plink_height

" > ${dir}/scripts/Real_Traits/height/data_qc_nomissing_plink_height

# I am doing blabla
cd ${dir}/scripts/Real_Traits/height/
sbatch data_qc_nomissing_plink_height
```


## Bolt-lmm-inf height
```python
##############################
Bolt-inf
##############################
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 10:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"


source /home/lezh/miniconda3/etc/profile.d/conda.sh


${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc_nomissing --phenoFile=${dir}/Phenotype_UKBB/height_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_qc_nomissing_PC_10.covars --qCovarCol=Paternal --qCovarCol=Sex --qCovarCol=PC{1:10}  --lmmInfOnly --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/height/data_qc_nomissing_Bolt_inf_height



" > ${dir}/scripts/Real_Traits/height/data_qc_nomissing_Bolt_inf_height


# I am doing blabla
cd ${dir}/scripts/Real_Traits/height/

sbatch data_qc_nomissing_Bolt_inf_height
```

