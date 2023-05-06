# Week 13

## LDAK Weighting on each dataset 
```python
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 15:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"
source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir_LDAK} --bfile ${dir}/data_qc  --max-threads 4  --cut-weights ${dir}/data_qc_weighting 
${dir_LDAK} --bfile ${dir}/data_Black  --max-threads 4  --cut-weights ${dir}/data_Black_weighting
${dir_LDAK} --bfile ${dir}/data_1Wan  --max-threads 4  --cut-weights ${dir}/data_1Wan_weighting

${dir_LDAK} --bfile ${dir}/data_qc  --max-threads 4  --calc-weights-all ${dir}/data_qc_weighting
${dir_LDAK} --bfile ${dir}/data_Black  --max-threads 4  --calc-weights-all ${dir}/data_Black_weighting
${dir_LDAK} --bfile ${dir}/data_1Wan  --max-threads 4  --calc-weights-all ${dir}/data_1Wan_weighting

" > ${dir}/scripts/LDAK_Weighting_Step1and2

# I am doing blabla
cd ${dir}/scripts/
sbatch LDAK_Weighting_Step1and2
```