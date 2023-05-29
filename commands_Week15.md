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