# Week 7
2023/3/27 - 2023/3/30

### Bolt non-genetic inf only
To check the time effiency.   
It is an approximation method using 30 pseudorandom SNPs to get mean value.  

In the analysis below, I tested nongenetic traits on 66688 individuals with 300K SNPs.   
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/data_qc --phenoFile=${dir}/type_1_error/non_genetic_trait_quant_1.pheno --phenoCol=Phenotype --lmmInfOnly  --LDscoresUseChip --statsFile=${dir}/type_1_error/data_bolt_inf_whole_nongenetic_result.Bolt
```
Location: type_1_error   
Script: ${dir}/scripts/bolt_ukbb_nongenetic_infOnly_1   
Result: Total elapsed time for Bolt-lmm-inf = 7812.38 sec   

## Power test using simulated traits
### h2 0.1, 0.5, 0.9 三个档
To simulate quantitative traits of UKBB 66688 individuals, with h2 = 0.1, causal = 1000.   
```python
  dir="/home/lezh/dsmwpred/zly"
  echo "#"'!'"/bin/bash
#SBATCH --mem 64G
#SBATCH -t 30:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"
source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/ldak5.XXX \
  --make-phenos ${dir}/Power/h2_01/trait_quant_h2_01_1 \
  --bfile ${dir}/data_qc \
  --ignore-weights YES \
  --power -1 \
  --her 0.1 \
  --num-phenos 1 \
  --num-causals 1000

" > ${dir}/scripts/Power/h2_01/trait_quant_h2_01_log

cd ${dir}/scripts/Power/h2_01/
sbatch trait_quant_h2_01_log
```  

To simulate quantitative traits of UKBB 66688 individuals, with h2 = 0.5, causal = 1000.   
```python
dir="/home/lezh/dsmwpred/zly"
  echo "#"'!'"/bin/bash
#SBATCH --mem 64G
#SBATCH -t 30:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"
source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/ldak5.XXX \
  --make-phenos ${dir}/Power/h2_05/trait_quant_h2_05_1 \
  --bfile ${dir}/data_qc \
  --ignore-weights YES \
  --power -1 \
  --her 0.5 \
  --num-phenos 1 \
  --num-causals 1000

" > ${dir}/scripts/Power/h2_05/trait_quant_h2_05_log

cd ${dir}/scripts/Power/h2_05/
sbatch trait_quant_h2_05_log
```  
To simulate quantitative traits of UKBB 66688 individuals, with h2 = 0.9, causal = 1000.   
```python
dir="/home/lezh/dsmwpred/zly"
  echo "#"'!'"/bin/bash
#SBATCH --mem 64G
#SBATCH -t 30:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"
source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir}/software/ldak5.XXX \
  --make-phenos ${dir}/Power/h2_09/trait_quant_h2_09_1 \
  --bfile ${dir}/data_qc \
  --ignore-weights YES \
  --power -1 \
  --her 0.9 \
  --num-phenos 1 \
  --num-causals 1000

" > ${dir}/scripts/Power/h2_09/trait_quant_h2_09_log

cd ${dir}/scripts/Power/h2_09/
sbatch trait_quant_h2_09_log
```  