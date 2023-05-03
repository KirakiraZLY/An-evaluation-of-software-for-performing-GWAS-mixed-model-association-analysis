# Week 12

## LDAK run Height
result in ${dir}/ukbb_whole_height_result/
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 2:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"

source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/ldak5.XXX --pheno ${dir}/height.pheno  --covar ${dir}/covar_PC.covars --max-threads 4  --bfile ${dir}/data_qc --linear ${dir}/ukbb_whole_height_result/data_ldak_height

" > ${dir}/scripts/Real_Traits/Height/data_ldak_height

# I am doing blabla
cd ${dir}/scripts/Real_Traits/Height/
sbatch data_ldak_height
```
## META result check, height