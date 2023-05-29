# Week 15

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