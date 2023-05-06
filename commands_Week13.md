# Week 13

## LDAK Weighting on each dataset 
```python
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 2:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"
source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir_LDAK} --bfile ${dir}/data_qc  --cut-weights ${dir}/sections_qc
${dir_LDAK} --bfile ${dir}/data_Black  --cut-weights ${dir}/sections_Black
${dir_LDAK} --bfile ${dir}/data_1Wan  --cut-weights ${dir}/sections_1Wan

${dir_LDAK} --bfile ${dir}/data_qc  --calc-weights-all ${dir}/sections_qc
${dir_LDAK} --bfile ${dir}/data_Black  --calc-weights-all ${dir}/sections_Black
${dir_LDAK} --bfile ${dir}/data_1Wan  --calc-weights-all ${dir}/sections_1Wan

" > ${dir}/scripts/LDAK_Weighting_Step1and2

# I am doing blabla
cd ${dir}/scripts/
sbatch LDAK_Weighting_Step1and2
```