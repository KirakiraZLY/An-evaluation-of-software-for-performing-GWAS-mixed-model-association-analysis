# Week 15

# BMI, quantitative
## PRS
1. Basic data: data_qc_Bolt_bmi   
   Target data: data_qc   
2. Clumping
   ```python
   dir="/home/lezh/dsmwpred/zly"
   ${dir}/software/plink \
    --bfile ${dir}/data_qc \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump ${dir}/Real_Traits/bmi/data_qc_Bolt_bmi \
    --clump-snp-field SNP \
    --clump-field P_BOLT_LMM \
    --out ${dir}/Real_Traits/PRS/data_qc
   ```
3. Extract the SNP ID and Generate PRS:
   ```python
    dir="/home/lezh/dsmwpred/zly"
   awk 'NR!=1{print $3}' ${dir}/Real_Traits/PRS/data_qc.clumped  >  ${dir}/Real_Traits/PRS/data_qc.valid.snp
   awk '{print $1,$12}' ${dir}/Real_Traits/bmi/data_qc_Bolt_bmi > ${dir}/Real_Traits/PRS/SNP.pvalue
   ```
4. P-value threshold
    ```python
    dir="/home/lezh/dsmwpred/zly"
    echo "0.001 0 0.001" > ${dir}/Real_Traits/PRS/range_list 
    echo "0.05 0 0.05" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.1 0 0.1" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.2 0 0.2" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.3 0 0.3" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.4 0 0.4" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.5 0 0.5" >> ${dir}/Real_Traits/PRS/range_list
    ```
5. PRS calculation
    ```python
    ${dir}/software/plink \
    --bfile ${dir}/data_qc \
    --score ${dir}/Real_Traits/bmi/data_qc_Bolt_bmi 1 5 9 header \
    --q-score-range ${dir}/Real_Traits/PRS/range_list ${dir}/Real_Traits/PRS/SNP.pvalue \
    --extract ${dir}/Real_Traits/PRS/data_qc.valid.snp \
    --out ${dir}/Real_Traits/PRS/data_qc
    ```
6. PCA
   ```python
   ${dir}/software/plink \
    --bfile ${dir}/data_qc \
    --indep-pairwise 200 50 0.25 \
    --out ${dir}/Real_Traits/PRS/data_qc
    # Then we calculate the first 6 PCs
    ${dir}/software/plink \
        --bfile ${dir}/data_qc \
        --extract ${dir}/Real_Traits/PRS/data_qc.prune.in \
        --pca 10 \
        --out ${dir}/Real_Traits/PRS/data_qc
    ```
7. Finding the "best-fit" PRS
        **In Rmd** 

    

## PRSice-2
```python
dir="/home/lezh/dsmwpred/zly"
Rscript ${dir}/PRS/PRSice2/PRSice.R \
    --prsice ${dir}/PRS/PRSice2/PRSice_linux \
    --base ${dir}/Real_Traits/bmi/data_qc_Bolt_bmi \
    --target ${dir}/data_qc \
    --binary-target F \
    --pheno ${dir}/bmi1.pheno \
    --cov ${dir}/covar_PC_10.covars \
    --base-maf MAF:0.05 \
    --base-info INFO:0.8 \
    --stat BETA \
    --beta \
    --out ${dir}/Real_Traits/PRS/data_qc_PRSice2
```










# Bilirubin, binary
## PRS
1. Basic data: data_qc_Bolt_bilirubin   
   Target data: data_qc   
2. Clumping
   ```python
   dir="/home/lezh/dsmwpred/zly"
   ${dir}/software/plink \
    --bfile ${dir}/data_qc \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump ${dir}/Real_Traits/bilirubin/data_qc_Bolt_bilirubin \
    --clump-snp-field SNP \
    --clump-field P_BOLT_LMM \
    --out ${dir}/Real_Traits/PRS/bilirubin_data_qc
   ```
3. Extract the SNP ID and Generate PRS:
   ```python
    dir="/home/lezh/dsmwpred/zly"
   awk 'NR!=1{print $3}' ${dir}/Real_Traits/PRS/bilirubin_data_qc.clumped  >  ${dir}/Real_Traits/PRS/bilirubin_data_qc.valid.snp
   awk '{print $1,$12}' ${dir}/Real_Traits/bilirubin/data_qc_Bolt_bilirubin > ${dir}/Real_Traits/PRS/bilirubin_SNP.pvalue
   ```
4. P-value threshold
    ```python
    dir="/home/lezh/dsmwpred/zly"
    echo "0.001 0 0.001" > ${dir}/Real_Traits/PRS/range_list 
    echo "0.05 0 0.05" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.1 0 0.1" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.2 0 0.2" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.3 0 0.3" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.4 0 0.4" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.5 0 0.5" >> ${dir}/Real_Traits/PRS/range_list
    ```
5. PRS calculation
    ```python
    ${dir}/software/plink \
    --bfile ${dir}/data_qc \
    --score ${dir}/Real_Traits/bilirubin/data_qc_Bolt_bilirubin 1 5 9 header \
    --q-score-range ${dir}/Real_Traits/PRS/range_list ${dir}/Real_Traits/PRS/bilirubin_SNP.pvalue \
    --extract ${dir}/Real_Traits/PRS/bilirubin_data_qc.valid.snp \
    --out ${dir}/Real_Traits/PRS/bilirubin_data_qc
    ```
6. PCA
   ```python

   dir="/home/lezh/dsmwpred/zly"
   echo "#"'!'"/bin/bash
    #SBATCH --mem 8G
    #SBATCH -t 1:0:0
    #SBATCH -A dsmwpred
    #SBATCH --constraint \"s05\"


    ${dir}/software/plink \
    --bfile ${dir}/data_qc \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump ${dir}/Real_Traits/bilirubin/data_qc_Bolt_bilirubin \
    --clump-snp-field SNP \
    --clump-field P_BOLT_LMM \
    --out ${dir}/Real_Traits/PRS/bilirubin_data_qc

    dir="/home/lezh/dsmwpred/zly"
   awk 'NR!=1{print $3}' ${dir}/Real_Traits/PRS/bilirubin_data_qc.clumped  >  ${dir}/Real_Traits/PRS/bilirubin_data_qc.valid.snp
   awk '{print $1,$12}' ${dir}/Real_Traits/bilirubin/data_qc_Bolt_bilirubin > ${dir}/Real_Traits/PRS/bilirubin_SNP.pvalue


   ${dir}/software/plink \
    --bfile ${dir}/data_qc \
    --score ${dir}/Real_Traits/bilirubin/data_qc_Bolt_bilirubin 1 5 9 header \
    --q-score-range ${dir}/Real_Traits/PRS/range_list ${dir}/Real_Traits/PRS/bilirubin_SNP.pvalue \
    --extract ${dir}/Real_Traits/PRS/bilirubin_data_qc.valid.snp \
    --out ${dir}/Real_Traits/PRS/bilirubin_data_qc


    ${dir}/software/plink \
        --bfile ${dir}/data_qc \
        --indep-pairwise 200 50 0.25 \
        --out ${dir}/Real_Traits/PRS/bilirubin_data_qc
        # Then we calculate the first 6 PCs
        ${dir}/software/plink \
            --bfile ${dir}/data_qc \
            --extract ${dir}/Real_Traits/PRS/bilirubin_data_qc.prune.in \
            --pca 10 \
            --out ${dir}/Real_Traits/PRS/bilirubin_data_qc


    " > ${dir}/scripts/Real_Traits/PRS/bilirubin_data_qc

    # I am doing blabla
    cd ${dir}/scripts/Real_Traits/PRS/
    sbatch bilirubin_data_qc
    ```
7. Finding the "best-fit" PRS
        **In Rmd** 




























# height, binary
## PRS
1. Basic data: data_qc_Bolt_height   
   Target data: data_qc   
2. Clumping
   ```python
   dir="/home/lezh/dsmwpred/zly"
   ${dir}/software/plink \
    --bfile ${dir}/data_qc \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump ${dir}/Real_Traits/height/data_qc_Bolt_height \
    --clump-snp-field SNP \
    --clump-field P_BOLT_LMM \
    --out ${dir}/Real_Traits/PRS/height_data_qc
   ```
3. Extract the SNP ID and Generate PRS:
   ```python
    dir="/home/lezh/dsmwpred/zly"
   awk 'NR!=1{print $3}' ${dir}/Real_Traits/PRS/height_data_qc.clumped  >  ${dir}/Real_Traits/PRS/height_data_qc.valid.snp
   awk '{print $1,$12}' ${dir}/Real_Traits/height/data_qc_Bolt_height > ${dir}/Real_Traits/PRS/height_SNP.pvalue
   ```
4. P-value threshold
    ```python
    dir="/home/lezh/dsmwpred/zly"
    echo "0.001 0 0.001" > ${dir}/Real_Traits/PRS/range_list 
    echo "0.05 0 0.05" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.1 0 0.1" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.2 0 0.2" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.3 0 0.3" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.4 0 0.4" >> ${dir}/Real_Traits/PRS/range_list
    echo "0.5 0 0.5" >> ${dir}/Real_Traits/PRS/range_list
    ```
5. PRS calculation
    ```python
    ${dir}/software/plink \
    --bfile ${dir}/data_qc \
    --score ${dir}/Real_Traits/height/data_qc_Bolt_height 1 5 9 header \
    --q-score-range ${dir}/Real_Traits/PRS/range_list ${dir}/Real_Traits/PRS/height_SNP.pvalue \
    --extract ${dir}/Real_Traits/PRS/height_data_qc.valid.snp \
    --out ${dir}/Real_Traits/PRS/height_data_qc
    ```
6. PCA
   ```python

   dir="/home/lezh/dsmwpred/zly"
   echo "#"'!'"/bin/bash
    #SBATCH --mem 8G
    #SBATCH -t 1:0:0
    #SBATCH -A dsmwpred
    #SBATCH --constraint \"s05\"


    ${dir}/software/plink \
    --bfile ${dir}/data_qc \
    --clump-p1 1 \
    --clump-r2 0.1 \
    --clump-kb 250 \
    --clump ${dir}/Real_Traits/height/data_qc_Bolt_height \
    --clump-snp-field SNP \
    --clump-field P_BOLT_LMM \
    --out ${dir}/Real_Traits/PRS/height_data_qc

    dir="/home/lezh/dsmwpred/zly"
   awk 'NR!=1{print $3}' ${dir}/Real_Traits/PRS/height_data_qc.clumped  >  ${dir}/Real_Traits/PRS/height_data_qc.valid.snp
   awk '{print $1,$12}' ${dir}/Real_Traits/height/data_qc_Bolt_height > ${dir}/Real_Traits/PRS/height_SNP.pvalue


   ${dir}/software/plink \
    --bfile ${dir}/data_qc \
    --score ${dir}/Real_Traits/height/data_qc_Bolt_height 1 5 9 header \
    --q-score-range ${dir}/Real_Traits/PRS/range_list ${dir}/Real_Traits/PRS/height_SNP.pvalue \
    --extract ${dir}/Real_Traits/PRS/height_data_qc.valid.snp \
    --out ${dir}/Real_Traits/PRS/height_data_qc


    ${dir}/software/plink \
        --bfile ${dir}/data_qc \
        --indep-pairwise 200 50 0.25 \
        --out ${dir}/Real_Traits/PRS/height_data_qc
        # Then we calculate the first 6 PCs
        ${dir}/software/plink \
            --bfile ${dir}/data_qc \
            --extract ${dir}/Real_Traits/PRS/height_data_qc.prune.in \
            --pca 10 \
            --out ${dir}/Real_Traits/PRS/height_data_qc


    " > ${dir}/scripts/Real_Traits/PRS/height_data_qc

    # I am doing blabla
    cd ${dir}/scripts/Real_Traits/PRS/
    sbatch height_data_qc
    ```
7. Finding the "best-fit" PRS
        **In Rmd** 