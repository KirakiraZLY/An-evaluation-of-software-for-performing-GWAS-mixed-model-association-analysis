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

${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_White --phenoFile=${dir}/Phenotype_UKBB/height_label.pheno  --phenoCol=Phenotype  --covarFile=${dir}/covar_White_PC_10.covars --qCovarCol=PC{1:10}  --lmmForceNonInf --LDscoresUseChip --numThreads 4  --statsFile=${dir}/Real_Traits/height/data_White_Bolt_height

" > ${dir}/scripts/Real_Traits/height/data_White_Bolt_height


# I am doing blabla
cd ${dir}/scripts/Real_Traits/height/

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




# New data
## Start by QC(genomeDK, Plink)
Filter out SNPs with genotype missingness >10%, samples with >10% missingness, MAF <5%, minor allele count(MAC) <100, 不做这个HWE p-value exceeding 1e-15.(MAF可以改成1%)   
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink --bfile ${dir}/newdata/data --geno 0.1 --mind 0.1 --maf 0.05 --make-bed --out ${dir}/newdata/new_data_qc
```
Output: data_qc   

## PCA
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink --bfile ${dir}/newdata/new_data_qc --recode vcf-iid --out ${dir}/newdata/new_data_qc_vcf
${dir}/software/plink --vcf ${dir}/newdata/new_data_qc_vcf.vcf --double-id --allow-extra-chr --set-missing-var-ids @:# --indep-pairwise 50 2 0.2 --out ${dir}/newdata/new_data_qc_vcf
${dir}/software/plink --vcf ${dir}/newdata/new_data_qc_vcf.vcf --double-id --allow-extra-chr --set-missing-var-ids @:# --extract ${dir}/newdata/new_data_qc_vcf.prune.in --pca --make-bed --out ${dir}/newdata/new_data_qc_vcf

```







# PRS
## BMI
1. Basic data: data_White_Bolt_bmi   
   Target data: new_data_qc   
2. Clumping + Threshold
   ```python
   dir="/home/lezh/dsmwpred/zly"

   echo "#"'!'"/bin/bash
    #SBATCH --mem 4G
    #SBATCH -t 10:0:0
    #SBATCH -c 8
    #SBATCH -A dsmwpred

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump ${dir}/Real_Traits/bmi/data_White_Bolt_bmi \
    --clump-snp-field SNP \
    --clump-field P_BOLT_LMM \
    --out ${dir}/Real_Traits/PRS/bmi/data_qc_bmi

   awk 'NR!=1{print $3}' ${dir}/Real_Traits/PRS/bmi/data_qc_bmi.clumped  >  ${dir}/Real_Traits/PRS/bmi/data_qc_bmi.valid.snp
   awk '{print $1,$12}' ${dir}/Real_Traits/bmi/data_White_Bolt_bmi > ${dir}/Real_Traits/PRS/bmi/data_qc_bmi_SNP.pvalue

    echo "0.001 0 0.001" > ${dir}/Real_Traits/PRS/bmi/data_qc_bmi_range_list 
    echo "0.05 0 0.05" >> ${dir}/Real_Traits/PRS/bmi/data_qc_bmi_range_list
    echo "0.1 0 0.1" >> ${dir}/Real_Traits/PRS/bmi/data_qc_bmi_range_list
    echo "0.2 0 0.2" >> ${dir}/Real_Traits/PRS/bmi/data_qc_bmi_range_list
    echo "0.3 0 0.3" >> ${dir}/Real_Traits/PRS/bmi/data_qc_bmi_range_list
    echo "0.4 0 0.4" >> ${dir}/Real_Traits/PRS/bmi/data_qc_bmi_range_list
    echo "0.5 0 0.5" >> ${dir}/Real_Traits/PRS/bmi/data_qc_bmi_range_list

    ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --score ${dir}/Real_Traits/bmi/data_White_Bolt_bmi 1 5 9 header \
    --q-score-range ${dir}/Real_Traits/PRS/bmi/data_qc_bmi_range_list ${dir}/Real_Traits/PRS/bmi/data_qc_bmi_SNP.pvalue \
    --extract ${dir}/Real_Traits/PRS/bmi/data_qc_bmi.valid.snp \
    --out ${dir}/Real_Traits/PRS/bmi/data_qc_bmi

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --indep-pairwise 200 50 0.25 \
    --out ${dir}/Real_Traits/PRS/bmi/data_qc_bmi
    # Then we calculate the first 10 PCs
    ${dir}/software/plink \
        --bfile ${dir}/newdata/new_data_qc \
        --extract ${dir}/Real_Traits/PRS/bmi/data_qc_bmi.prune.in \
        --pca 10 \
        --out ${dir}/Real_Traits/PRS/bmi/data_qc_bmi


    " > ${dir}/scripts/Real_Traits/PRS/bmi/data_qc_bmi

    # I am doing blabla
    cd ${dir}/scripts/Real_Traits/PRS/bmi/
    sbatch data_qc_bmi
    ```
3. Finding the "best-fit" PRS
        **In Rmd** 




## alkaline
1. Basic data: data_qc_Bolt_alkaline   
   Target data: new_data_qc   
2. Clumping + Threshold
   ```python
   dir="/home/lezh/dsmwpred/zly"

   echo "#"'!'"/bin/bash
    #SBATCH --mem 4G
    #SBATCH -t 10:0:0
    #SBATCH -c 8
    #SBATCH -A dsmwpred

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump ${dir}/Real_Traits/alkaline/data_qc_Bolt_alkaline \
    --clump-snp-field SNP \
    --clump-field P_BOLT_LMM \
    --out ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline

   awk 'NR!=1{print $3}' ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline.clumped  >  ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline.valid.snp
   awk '{print $1,$12}' ${dir}/Real_Traits/alkaline/data_qc_Bolt_alkaline > ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline_SNP.pvalue

    echo "0.001 0 0.001" > ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline_range_list 
    echo "0.05 0 0.05" >> ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline_range_list
    echo "0.1 0 0.1" >> ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline_range_list
    echo "0.2 0 0.2" >> ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline_range_list
    echo "0.3 0 0.3" >> ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline_range_list
    echo "0.4 0 0.4" >> ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline_range_list
    echo "0.5 0 0.5" >> ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline_range_list

    ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --score ${dir}/Real_Traits/alkaline/data_qc_Bolt_alkaline 1 5 9 header \
    --q-score-range ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline_range_list ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline_SNP.pvalue \
    --extract ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline.valid.snp \
    --out ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --indep-pairwise 200 50 0.25 \
    --out ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline
    # Then we calculate the first 10 PCs
    ${dir}/software/plink \
        --bfile ${dir}/newdata/new_data_qc \
        --extract ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline.prune.in \
        --pca 10 \
        --out ${dir}/Real_Traits/PRS/alkaline/data_qc_alkaline


    " > ${dir}/scripts/Real_Traits/PRS/alkaline/data_qc_alkaline

    # I am doing blabla
    cd ${dir}/scripts/Real_Traits/PRS/alkaline/
    sbatch data_qc_alkaline
    ```
3. Finding the "best-fit" PRS
        **In Rmd** 




## bilirubin
1. Basic data: data_qc_Bolt_bilirubin   
   Target data: new_data_qc   
2. Clumping + Threshold
   ```python
   dir="/home/lezh/dsmwpred/zly"

   echo "#"'!'"/bin/bash
    #SBATCH --mem 4G
    #SBATCH -t 10:0:0
    #SBATCH -c 8
    #SBATCH -A dsmwpred

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump ${dir}/Real_Traits/bilirubin/data_qc_Bolt_bilirubin \
    --clump-snp-field SNP \
    --clump-field P_BOLT_LMM \
    --out ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin

   awk 'NR!=1{print $3}' ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin.clumped  >  ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin.valid.snp
   awk '{print $1,$12}' ${dir}/Real_Traits/bilirubin/data_qc_Bolt_bilirubin > ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin_SNP.pvalue

    echo "0.001 0 0.001" > ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin_range_list 
    echo "0.05 0 0.05" >> ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin_range_list
    echo "0.1 0 0.1" >> ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin_range_list
    echo "0.2 0 0.2" >> ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin_range_list
    echo "0.3 0 0.3" >> ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin_range_list
    echo "0.4 0 0.4" >> ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin_range_list
    echo "0.5 0 0.5" >> ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin_range_list

    ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --score ${dir}/Real_Traits/bilirubin/data_qc_Bolt_bilirubin 1 5 9 header \
    --q-score-range ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin_range_list ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin_SNP.pvalue \
    --extract ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin.valid.snp \
    --out ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --indep-pairwise 200 50 0.25 \
    --out ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin
    # Then we calculate the first 10 PCs
    ${dir}/software/plink \
        --bfile ${dir}/newdata/new_data_qc \
        --extract ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin.prune.in \
        --pca 10 \
        --out ${dir}/Real_Traits/PRS/bilirubin/data_qc_bilirubin


    " > ${dir}/scripts/Real_Traits/PRS/bilirubin/data_qc_bilirubin

    # I am doing blabla
    cd ${dir}/scripts/Real_Traits/PRS/bilirubin/
    sbatch data_qc_bilirubin
    ```
3. Finding the "best-fit" PRS
        **In Rmd** 






## cholesterol
1. Basic data: data_qc_Bolt_cholesterol   
   Target data: new_data_qc   
2. Clumping + Threshold
   ```python
   dir="/home/lezh/dsmwpred/zly"

   echo "#"'!'"/bin/bash
    #SBATCH --mem 4G
    #SBATCH -t 10:0:0
    #SBATCH -c 8
    #SBATCH -A dsmwpred

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump ${dir}/Real_Traits/cholesterol/data_qc_Bolt_cholesterol \
    --clump-snp-field SNP \
    --clump-field P_BOLT_LMM \
    --out ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol

   awk 'NR!=1{print $3}' ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol.clumped  >  ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol.valid.snp
   awk '{print $1,$12}' ${dir}/Real_Traits/cholesterol/data_qc_Bolt_cholesterol > ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol_SNP.pvalue

    echo "0.001 0 0.001" > ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol_range_list 
    echo "0.05 0 0.05" >> ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol_range_list
    echo "0.1 0 0.1" >> ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol_range_list
    echo "0.2 0 0.2" >> ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol_range_list
    echo "0.3 0 0.3" >> ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol_range_list
    echo "0.4 0 0.4" >> ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol_range_list
    echo "0.5 0 0.5" >> ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol_range_list

    ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --score ${dir}/Real_Traits/cholesterol/data_qc_Bolt_cholesterol 1 5 9 header \
    --q-score-range ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol_range_list ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol_SNP.pvalue \
    --extract ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol.valid.snp \
    --out ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --indep-pairwise 200 50 0.25 \
    --out ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol
    # Then we calculate the first 10 PCs
    ${dir}/software/plink \
        --bfile ${dir}/newdata/new_data_qc \
        --extract ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol.prune.in \
        --pca 10 \
        --out ${dir}/Real_Traits/PRS/cholesterol/data_qc_cholesterol


    " > ${dir}/scripts/Real_Traits/PRS/cholesterol/data_qc_cholesterol

    # I am doing blabla
    cd ${dir}/scripts/Real_Traits/PRS/cholesterol/
    sbatch data_qc_cholesterol
    ```
3. Finding the "best-fit" PRS
        **In Rmd** 




## hba1c
1. Basic data: data_qc_Bolt_hba1c   
   Target data: new_data_qc   
2. Clumping + Threshold
   ```python
   dir="/home/lezh/dsmwpred/zly"

   echo "#"'!'"/bin/bash
    #SBATCH --mem 4G
    #SBATCH -t 10:0:0
    #SBATCH -c 8
    #SBATCH -A dsmwpred

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump ${dir}/Real_Traits/hba1c/data_qc_Bolt_hba1c \
    --clump-snp-field SNP \
    --clump-field P_BOLT_LMM \
    --out ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c

   awk 'NR!=1{print $3}' ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c.clumped  >  ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c.valid.snp
   awk '{print $1,$12}' ${dir}/Real_Traits/hba1c/data_qc_Bolt_hba1c > ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c_SNP.pvalue

    echo "0.001 0 0.001" > ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c_range_list 
    echo "0.05 0 0.05" >> ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c_range_list
    echo "0.1 0 0.1" >> ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c_range_list
    echo "0.2 0 0.2" >> ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c_range_list
    echo "0.3 0 0.3" >> ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c_range_list
    echo "0.4 0 0.4" >> ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c_range_list
    echo "0.5 0 0.5" >> ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c_range_list

    ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --score ${dir}/Real_Traits/hba1c/data_qc_Bolt_hba1c 1 5 9 header \
    --q-score-range ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c_range_list ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c_SNP.pvalue \
    --extract ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c.valid.snp \
    --out ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --indep-pairwise 200 50 0.25 \
    --out ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c
    # Then we calculate the first 10 PCs
    ${dir}/software/plink \
        --bfile ${dir}/newdata/new_data_qc \
        --extract ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c.prune.in \
        --pca 10 \
        --out ${dir}/Real_Traits/PRS/hba1c/data_qc_hba1c


    " > ${dir}/scripts/Real_Traits/PRS/hba1c/data_qc_hba1c

    # I am doing blabla
    cd ${dir}/scripts/Real_Traits/PRS/hba1c/
    sbatch data_qc_hba1c
    ```
3. Finding the "best-fit" PRS
        **In Rmd** 












## height
1. Basic data: data_qc_Bolt_height   
   Target data: new_data_qc   
2. Clumping + Threshold
   ```python
   dir="/home/lezh/dsmwpred/zly"

   echo "#"'!'"/bin/bash
    #SBATCH --mem 4G
    #SBATCH -t 10:0:0
    #SBATCH -c 8
    #SBATCH -A dsmwpred

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump ${dir}/Real_Traits/height/data_qc_Bolt_height \
    --clump-snp-field SNP \
    --clump-field P_BOLT_LMM \
    --out ${dir}/Real_Traits/PRS/height/data_qc_height

   awk 'NR!=1{print $3}' ${dir}/Real_Traits/PRS/height/data_qc_height.clumped  >  ${dir}/Real_Traits/PRS/height/data_qc_height.valid.snp
   awk '{print $1,$12}' ${dir}/Real_Traits/height/data_qc_Bolt_height > ${dir}/Real_Traits/PRS/height/data_qc_height_SNP.pvalue

    echo "0.001 0 0.001" > ${dir}/Real_Traits/PRS/height/data_qc_height_range_list 
    echo "0.05 0 0.05" >> ${dir}/Real_Traits/PRS/height/data_qc_height_range_list
    echo "0.1 0 0.1" >> ${dir}/Real_Traits/PRS/height/data_qc_height_range_list
    echo "0.2 0 0.2" >> ${dir}/Real_Traits/PRS/height/data_qc_height_range_list
    echo "0.3 0 0.3" >> ${dir}/Real_Traits/PRS/height/data_qc_height_range_list
    echo "0.4 0 0.4" >> ${dir}/Real_Traits/PRS/height/data_qc_height_range_list
    echo "0.5 0 0.5" >> ${dir}/Real_Traits/PRS/height/data_qc_height_range_list

    ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --score ${dir}/Real_Traits/height/data_qc_Bolt_height 1 5 9 header \
    --q-score-range ${dir}/Real_Traits/PRS/height/data_qc_height_range_list ${dir}/Real_Traits/PRS/height/data_qc_height_SNP.pvalue \
    --extract ${dir}/Real_Traits/PRS/height/data_qc_height.valid.snp \
    --out ${dir}/Real_Traits/PRS/height/data_qc_height

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --indep-pairwise 200 50 0.25 \
    --out ${dir}/Real_Traits/PRS/height/data_qc_height
    # Then we calculate the first 10 PCs
    ${dir}/software/plink \
        --bfile ${dir}/newdata/new_data_qc \
        --extract ${dir}/Real_Traits/PRS/height/data_qc_height.prune.in \
        --pca 10 \
        --out ${dir}/Real_Traits/PRS/height/data_qc_height


    " > ${dir}/scripts/Real_Traits/PRS/height/data_qc_height

    # I am doing blabla
    cd ${dir}/scripts/Real_Traits/PRS/height/
    sbatch data_qc_height
    ```
3. Finding the "best-fit" PRS
        **In Rmd** 








## urate
1. Basic data: data_qc_Bolt_urate   
   Target data: new_data_qc   
2. Clumping + Threshold
   ```python
   dir="/home/lezh/dsmwpred/zly"

   echo "#"'!'"/bin/bash
    #SBATCH --mem 4G
    #SBATCH -t 10:0:0
    #SBATCH -c 8
    #SBATCH -A dsmwpred

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump ${dir}/Real_Traits/urate/data_qc_Bolt_urate \
    --clump-snp-field SNP \
    --clump-field P_BOLT_LMM \
    --out ${dir}/Real_Traits/PRS/urate/data_qc_urate

   awk 'NR!=1{print $3}' ${dir}/Real_Traits/PRS/urate/data_qc_urate.clumped  >  ${dir}/Real_Traits/PRS/urate/data_qc_urate.valid.snp
   awk '{print $1,$12}' ${dir}/Real_Traits/urate/data_qc_Bolt_urate > ${dir}/Real_Traits/PRS/urate/data_qc_urate_SNP.pvalue

    echo "0.001 0 0.001" > ${dir}/Real_Traits/PRS/urate/data_qc_urate_range_list 
    echo "0.05 0 0.05" >> ${dir}/Real_Traits/PRS/urate/data_qc_urate_range_list
    echo "0.1 0 0.1" >> ${dir}/Real_Traits/PRS/urate/data_qc_urate_range_list
    echo "0.2 0 0.2" >> ${dir}/Real_Traits/PRS/urate/data_qc_urate_range_list
    echo "0.3 0 0.3" >> ${dir}/Real_Traits/PRS/urate/data_qc_urate_range_list
    echo "0.4 0 0.4" >> ${dir}/Real_Traits/PRS/urate/data_qc_urate_range_list
    echo "0.5 0 0.5" >> ${dir}/Real_Traits/PRS/urate/data_qc_urate_range_list

    ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --score ${dir}/Real_Traits/urate/data_qc_Bolt_urate 1 5 9 header \
    --q-score-range ${dir}/Real_Traits/PRS/urate/data_qc_urate_range_list ${dir}/Real_Traits/PRS/urate/data_qc_urate_SNP.pvalue \
    --extract ${dir}/Real_Traits/PRS/urate/data_qc_urate.valid.snp \
    --out ${dir}/Real_Traits/PRS/urate/data_qc_urate

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --indep-pairwise 200 50 0.25 \
    --out ${dir}/Real_Traits/PRS/urate/data_qc_urate
    # Then we calculate the first 10 PCs
    ${dir}/software/plink \
        --bfile ${dir}/newdata/new_data_qc \
        --extract ${dir}/Real_Traits/PRS/urate/data_qc_urate.prune.in \
        --pca 10 \
        --out ${dir}/Real_Traits/PRS/urate/data_qc_urate


    " > ${dir}/scripts/Real_Traits/PRS/urate/data_qc_urate

    # I am doing blabla
    cd ${dir}/scripts/Real_Traits/PRS/urate/
    sbatch data_qc_urate
    ```
3. Finding the "best-fit" PRS
        **In Rmd** 




# PRS, data_White_Bolt_height -> new_data_qc

## BMI
1. Basic data: data_White_Bolt_bmi   
   Target data: new_data_qc   
2. Clumping + Threshold
   ```python
   dir="/home/lezh/dsmwpred/zly"

   echo "#"'!'"/bin/bash
    #SBATCH --mem 4G
    #SBATCH -t 10:0:0
    #SBATCH -c 8
    #SBATCH -A dsmwpred

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump ${dir}/Real_Traits/bmi/data_White_Bolt_bmi \
    --clump-snp-field SNP \
    --clump-field P_BOLT_LMM \
    --out ${dir}/Real_Traits/PRS/bmi/data_White_bmi

   awk 'NR!=1{print $3}' ${dir}/Real_Traits/PRS/bmi/data_White_bmi.clumped  >  ${dir}/Real_Traits/PRS/bmi/data_White_bmi.valid.snp
   awk '{print $1,$12}' ${dir}/Real_Traits/bmi/data_White_Bolt_bmi > ${dir}/Real_Traits/PRS/bmi/data_White_bmi_SNP.pvalue

    echo "0.001 0 0.001" > ${dir}/Real_Traits/PRS/bmi/data_White_bmi_range_list 
    echo "0.05 0 0.05" >> ${dir}/Real_Traits/PRS/bmi/data_White_bmi_range_list
    echo "0.1 0 0.1" >> ${dir}/Real_Traits/PRS/bmi/data_White_bmi_range_list
    echo "0.2 0 0.2" >> ${dir}/Real_Traits/PRS/bmi/data_White_bmi_range_list
    echo "0.3 0 0.3" >> ${dir}/Real_Traits/PRS/bmi/data_White_bmi_range_list
    echo "0.4 0 0.4" >> ${dir}/Real_Traits/PRS/bmi/data_White_bmi_range_list
    echo "0.5 0 0.5" >> ${dir}/Real_Traits/PRS/bmi/data_White_bmi_range_list

    ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --score ${dir}/Real_Traits/bmi/data_White_Bolt_bmi 1 5 9 header \
    --q-score-range ${dir}/Real_Traits/PRS/bmi/data_White_bmi_range_list ${dir}/Real_Traits/PRS/bmi/data_White_bmi_SNP.pvalue \
    --extract ${dir}/Real_Traits/PRS/bmi/data_White_bmi.valid.snp \
    --out ${dir}/Real_Traits/PRS/bmi/data_White_bmi

   ${dir}/software/plink \
    --bfile ${dir}/newdata/new_data_qc \
    --indep-pairwise 200 50 0.25 \
    --out ${dir}/Real_Traits/PRS/bmi/data_White_bmi
    # Then we calculate the first 10 PCs
    ${dir}/software/plink \
        --bfile ${dir}/newdata/new_data_qc \
        --extract ${dir}/Real_Traits/PRS/bmi/data_White_bmi.prune.in \
        --pca 10 \
        --out ${dir}/Real_Traits/PRS/bmi/data_White_bmi


    " > ${dir}/scripts/Real_Traits/PRS/bmi/data_White_bmi

    # I am doing blabla
    cd ${dir}/scripts/Real_Traits/PRS/bmi/
    sbatch data_White_bmi
    ```
3. Finding the "best-fit" PRS
        **In Rmd** 