# Week 13

## fastGWA for dataWhite
```python
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 32G
#SBATCH -t 4:0:0
#SBATCH -c 10
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"

${dir}/software/gcta \
--bfile ${dir}/data_White \
--autosome --maf 0.01 \
--make-grm --out ${dir}/data_White_gcta_1 \
--thread-num 10

${dir}/software/gcta \
--grm ${dir}/data_White_gcta_1 --make-bK-sparse 0.05 \
--out ${dir}/data_White_gcta_2  \
--thread-num 10

" > ${dir}/scripts/data_White_fastGWA_STEP1and2

# I am doing blabla
cd ${dir}/scripts/
sbatch data_White_fastGWA_STEP1and2
```
