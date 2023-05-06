# Week 13

## LDAK Weighting on each dataset 
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

${dir_LDAK} --bfile ${dir}/data_qc  --max-threads 4  --cut-weights ${dir}/data_qc_weighting 

${dir_LDAK} --bfile ${dir}/data_qc  --max-threads 4  --calc-weights-all ${dir}/data_qc_weighting


" > ${dir}/scripts/LDAK_Weighting_Step1and2_qc

# I am doing blabla
cd ${dir}/scripts/
sbatch LDAK_Weighting_Step1and2_qc

dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 8:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"
source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir_LDAK} --bfile ${dir}/data_Black  --max-threads 4  --cut-weights ${dir}/data_Black_weighting

${dir_LDAK} --bfile ${dir}/data_Black  --max-threads 4  --calc-weights-all ${dir}/data_Black_weighting

" > ${dir}/scripts/LDAK_Weighting_Step1and2_Black

# I am doing blabla
cd ${dir}/scripts/
sbatch LDAK_Weighting_Step1and2_Black

dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 8:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"
source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir_LDAK} --bfile ${dir}/data_1Wan  --max-threads 4  --cut-weights ${dir}/data_1Wan_weighting

${dir_LDAK} --bfile ${dir}/data_1Wan  --max-threads 4  --calc-weights-all ${dir}/data_1Wan_weighting

" > ${dir}/scripts/LDAK_Weighting_Step1and2_1Wan

# I am doing blabla
cd ${dir}/scripts/
sbatch LDAK_Weighting_Step1and2_1Wan
```


## Trait 13 - 18 Generator: LDAK
```python
######################################
Simulate data 13-18: LDAK
######################################
#############
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 8:0:0
#SBATCH -c 8
#SBATCH -A dsmwpred

source /home/lezh/miniconda3/etc/profile.d/conda.sh


${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_13_to_24/Trait_13 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_weighting/weights.short \
  --power -0.25 \
  --her 0.1 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --extract ${dir}/snps_1_to_12_qc.txt


  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_13_to_24/Trait_14 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_weighting/weights.short \
  --power -0.25 \
  --her 0.5 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_13_to_24/Trait_15 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_weighting/weights.short \
  --power -0.25 \
  --her 0.9 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_13_to_24/Trait_16 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_weighting/weights.short \
  --power -0.25 \
  --her 0.1 \
  --num-phenos 5 \
  --num-causals 10000 \
  --max-threads 8 \
  --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_13_to_24/Trait_17 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_weighting/weights.short \
  --power -0.25 \
  --her 0.5 \
  --num-phenos 5 \
  --num-causals 10000 \
  --max-threads 8 \
  --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_13_to_24/Trait_18 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_weighting/weights.short \
  --power -0.25 \
  --her 0.9 \
  --num-phenos 5 \
  --num-causals 10000 \
  --max-threads 8 \
  --extract ${dir}/snps_1_to_12_qc.txt

  " > ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_13_to_24/Trait_qt_LDAK_13to18

# I am doing blabla
cd ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_13_to_24
sbatch Trait_qt_LDAK_13to18
```


## Trait 19 - 24: LDAK and 1Wan
```python 
######################################################################
Trait 19 - 24
######################################################################
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 4:0:0
#SBATCH -c 8
#SBATCH -A dsmwpred

source /home/lezh/miniconda3/etc/profile.d/conda.sh

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_13_to_24/Trait_19   --bfile ${dir}/data_1Wan   --weights ${dir}/data_1Wan_weighting/weights.short   --power -0.25   --her 0.1   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt
  
  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_13_to_24/Trait_20   --bfile ${dir}/data_1Wan    --weights ${dir}/data_1Wan_weighting/weights.short   --power -0.25   --her 0.5   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK}    --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_13_to_24/Trait_21   --bfile ${dir}/data_1Wan    --weights ${dir}/data_1Wan_weighting/weights.short   --power -0.25   --her 0.9   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK}    --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_13_to_24/Trait_22   --bfile ${dir}/data_1Wan    --weights ${dir}/data_1Wan_weighting/weights.short   --power -0.25   --her 0.1   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK}    --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_13_to_24/Trait_23   --bfile ${dir}/data_1Wan    --weights ${dir}/data_1Wan_weighting/weights.short   --power -0.25   --her 0.5   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK}    --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_13_to_24/Trait_24   --bfile ${dir}/data_1Wan    --weights ${dir}/data_1Wan_weighting/weights.short   --power -0.25   --her 0.9   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  " > ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_13_to_24/Trait_qt_LDAK_19to24

# I am doing blabla
cd ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_13_to_24
sbatch Trait_qt_LDAK_19to24
```