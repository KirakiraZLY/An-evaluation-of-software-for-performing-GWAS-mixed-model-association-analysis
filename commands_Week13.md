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
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
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



## T19 - 24, Black
```python
######################################################################
Trait B19 - B24
######################################################################
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 4:0:0
#SBATCH -c 8
#SBATCH -A dsmwpred

source /home/lezh/miniconda3/etc/profile.d/conda.sh

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B19   --bfile ${dir}/data_Black   --weights ${dir}/data_Black_weighting/weights.short   --power -0.25   --her 0.1   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt
  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B20   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_weighting/weights.short   --power -0.25   --her 0.5   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B21   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_weighting/weights.short   --power -0.25   --her 0.9   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B22   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_weighting/weights.short   --power -0.25   --her 0.1   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B23   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_weighting/weights.short   --power -0.25   --her 0.5   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B24   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_weighting/weights.short   --power -0.25   --her 0.9   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  " > ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_B1_to_B24/Trait_B19toB24

# I am doing blabla
cd ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_B1_to_B24
sbatch Trait_B19toB24


```


## Trait 13-18, 5 softwares
**Submitted**  
**Waiting**    
## Trait 19-24, 6 softwares
**Submitted**   
**Waiting**   
## Trait 19-24_Black, 6 softwares
**Waiting for trait generator**   
## 5.6 Plan
Binary Traits(37 - 48 and Black)
1. Generator Traits
2. Softwares

## T 19 - 24 Black, LDAK
```python
######################################################################
Trait B19 - B24
######################################################################
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 4:0:0
#SBATCH -c 8
#SBATCH -A dsmwpred

source /home/lezh/miniconda3/etc/profile.d/conda.sh

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B19   --bfile ${dir}/data_Black   --weights ${dir}/data_Black_weighting/weights.short   --power -0.25   --her 0.1   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt
  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B20   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_weighting/weights.short   --power -0.25   --her 0.5   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B21   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_weighting/weights.short   --power -0.25   --her 0.9   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B22   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_weighting/weights.short   --power -0.25   --her 0.1   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B23   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_weighting/weights.short   --power -0.25   --her 0.5   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B24   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_weighting/weights.short   --power -0.25   --her 0.9   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  " > ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_B1_to_B24/Trait_B19toB24

# I am doing blabla
cd ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_B1_to_B24
sbatch Trait_B19toB24


```
## T 43 - 48 Black, LDAK, Prevalence = 0.01
```python 
##############################################################################################
B43 - B48
################################
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 4G
#SBATCH -t 2:0:0
#SBATCH -c 8
#SBATCH -A dsmwpred

  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_B43 \
  --bfile ${dir}/data_Black --weights ${dir}/data_Black_weighting/weights.short --power -0.25 --her 0.1 --num-phenos 5 --num-causals 10000 \
  --max-threads 8 --prevalence 0.01  --extract ${dir}/snps_1_to_12_Black.txt

    ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_B44 \
  --bfile ${dir}/data_Black --weights ${dir}/data_Black_weighting/weights.short --power -0.25 \
  --her 0.5 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.01  --extract ${dir}/snps_1_to_12_Black.txt

    ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_B45 \
  --bfile ${dir}/data_Black --weights ${dir}/data_Black_weighting/weights.short --power -0.25 --her 0.9 --num-phenos 5 --num-causals 10000 \
  --max-threads 8 --prevalence 0.01  --extract ${dir}/snps_1_to_12_Black.txt

    ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_B46 \
  --bfile ${dir}/data_Black --weights ${dir}/data_Black_weighting/weights.short  --power -0.25 \
  --her 0.1 --num-phenos 5 --num-causals 1000 --max-threads 8 --prevalence 0.01    --extract ${dir}/snps_1_to_12_Black.txt

    ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_B47 \
  --bfile ${dir}/data_Black \
  --weights ${dir}/data_Black_weighting/weights.short \
  --power -0.25 \
  --her 0.5 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --prevalence 0.01  --extract ${dir}/snps_1_to_12_Black.txt

    ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_B48 \
  --bfile ${dir}/data_Black \
  --weights ${dir}/data_Black_weighting/weights.short \
  --power -0.25 \
  --her 0.9 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --prevalence 0.01  --extract ${dir}/snps_1_to_12_Black.txt

" > ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_B25_to_B48_Binary/Trait_B43toB48

# I am doing blabla
cd ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_B25_to_B48_Binary
sbatch Trait_B43toB48
```






## T 37 - 48, LDAK, P001
```python
##############################################################################################
37 - 48
################################
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 4G
#SBATCH -t 2:0:0
#SBATCH -c 8
#SBATCH -A dsmwpred

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_37 --bfile ${dir}/data_qc --weights ${dir}/data_qc_weighting/weights.short --power -0.25 --her 0.1 --num-phenos 5 \
  --num-causals 1000  --max-threads 8 --prevalence 0.01 --extract ${dir}/snps_1_to_12_qc.txt


  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_38 --bfile ${dir}/data_qc --weights ${dir}/data_qc_weighting/weights.short --power -0.25 --her 0.5 --num-phenos 5 \
  --num-causals 1000 --max-threads 8 --prevalence 0.01 --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_39 --bfile ${dir}/data_qc --weights ${dir}/data_qc_weighting/weights.short --power -0.25 \
  --her 0.9 --num-phenos 5 --num-causals 1000 --max-threads 8 --prevalence 0.01 --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_40 \
  --bfile ${dir}/data_qc --weights ${dir}/data_qc_weighting/weights.short --power -0.25 --her 0.1 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.01 \
  --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_41 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_weighting/weights.short \
  --power -0.25 \
  --her 0.5 \
  --num-phenos 5 \
  --num-causals 10000 \
  --max-threads 8 \
  --prevalence 0.01 \
  --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_42 --bfile ${dir}/data_qc --weights ${dir}/data_qc_weighting/weights.short --power -0.25 --her 0.9 \
  --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.01 --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_43 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_weighting/weights.short --power -0.25 --her 0.1 --num-phenos 5 --num-causals 10000 \
  --max-threads 8 --prevalence 0.01 --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt


  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_44 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_weighting/weights.short --power -0.25 \
  --her 0.5 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.01 --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_45 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_weighting/weights.short --power -0.25 --her 0.9 --num-phenos 5 --num-causals 10000 \
  --max-threads 8 --prevalence 0.01 --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_46 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_weighting/weights.short  --power -0.25 \
  --her 0.1 --num-phenos 5 --num-causals 1000 --max-threads 8 --prevalence 0.01 \
  --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_47 \
  --bfile ${dir}/data_1Wan \
  --weights ${dir}/data_1Wan_weighting/weights.short \
  --power -0.25 \
  --her 0.5 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --prevalence 0.01 \
  --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_48 \
  --bfile ${dir}/data_1Wan \
  --weights ${dir}/data_1Wan_weighting/weights.short \
  --power -0.25 \
  --her 0.9 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --prevalence 0.01 \
  --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

" > ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_25_to_48_Binary/Trait_37to48

# I am doing blabla
cd ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_25_to_48_Binary
sbatch Trait_37to48
```


## Trait 13 include first 10 PCs, fastGWA







## T 37 - 48, LDAK, P015
```python
##############################################################################################
37 - 48
################################
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 4G
#SBATCH -t 2:0:0
#SBATCH -c 8
#SBATCH -A dsmwpred

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_37 --bfile ${dir}/data_qc --weights ${dir}/data_qc_weighting/weights.short --power -0.25 --her 0.1 --num-phenos 5 \
  --num-causals 1000  --max-threads 8 --prevalence 0.15 --extract ${dir}/snps_1_to_12_qc.txt
  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_38 --bfile ${dir}/data_qc --weights ${dir}/data_qc_weighting/weights.short --power -0.25 --her 0.5 --num-phenos 5 \
  --num-causals 1000 --max-threads 8 --prevalence 0.15 --extract ${dir}/snps_1_to_12_qc.txt
  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_39 --bfile ${dir}/data_qc --weights ${dir}/data_qc_weighting/weights.short --power -0.25 \
  --her 0.9 --num-phenos 5 --num-causals 1000 --max-threads 8 --prevalence 0.15 --extract ${dir}/snps_1_to_12_qc.txt
  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_40 \
  --bfile ${dir}/data_qc --weights ${dir}/data_qc_weighting/weights.short --power -0.25 --her 0.1 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.15 \
  --extract ${dir}/snps_1_to_12_qc.txt
  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_41 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_weighting/weights.short \
  --power -0.25 --her 0.5 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.15 --extract ${dir}/snps_1_to_12_qc.txt
  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_42 --bfile ${dir}/data_qc --weights ${dir}/data_qc_weighting/weights.short --power -0.25 --her 0.9 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.15 --extract ${dir}/snps_1_to_12_qc.txt
  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_43 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_weighting/weights.short --power -0.25 --her 0.1 --num-phenos 5 --num-causals 10000  --max-threads 8 --prevalence 0.15 --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt


  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_44 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_weighting/weights.short --power -0.25 \
  --her 0.5 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.15 --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_45 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_weighting/weights.short --power -0.25 --her 0.9 --num-phenos 5 --num-causals 10000 \
  --max-threads 8 --prevalence 0.15 --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_46 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_weighting/weights.short  --power -0.25 \
  --her 0.1 --num-phenos 5 --num-causals 1000 --max-threads 8 --prevalence 0.15 \
  --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_47 \
  --bfile ${dir}/data_1Wan \
  --weights ${dir}/data_1Wan_weighting/weights.short \
  --power -0.25 \
  --her 0.5 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --prevalence 0.15 \
  --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_48 \
  --bfile ${dir}/data_1Wan \
  --weights ${dir}/data_1Wan_weighting/weights.short \
  --power -0.25 \
  --her 0.9 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --prevalence 0.15 \
  --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

" > ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_37to48

# I am doing blabla
cd ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_25_to_48_Binary_P015
sbatch Trait_37to48
```


## fastGWA, 1Wan test, generator
```python
dir_Plink="/home/lezh/snpher/faststorage/plink"
dir="/home/lezh/dsmwpred/zly"
dir_j="/home/lezh/dsmwpred/jasper/Weights"
${dir_Plink} --bfile ${dir_j}/UKBB  --noweb --keep ${dir}/type_1_error/Test/UKBB_1Wan.fam --recode --make-bed --out ${dir}/type_1_error/Test/UKBB_1Wan
```

## fastGWA, 5Wan test, generator
```python
dir_Plink="/home/lezh/snpher/faststorage/plink"
dir="/home/lezh/dsmwpred/zly"
dir_j="/home/lezh/dsmwpred/jasper/Weights"
${dir_Plink} --bfile ${dir_j}/UKBB  --noweb --keep ${dir}/type_1_error/Test/UKBB_5Wan.fam --recode --make-bed --out ${dir}/type_1_error/Test/UKBB_5Wan
```



## fastGWA, 1Wan test, step 1and2
```python
dir="/home/lezh/dsmwpred/zly"

${dir}/software/gcta \
--bfile ${dir}/type_1_error/Test/UKBB_1Wan \
--autosome --maf 0.01 \
--make-grm --out ${dir}/type_1_error/Test/UKBB_1Wan_gcta_1 \
--thread-num 10

${dir}/software/gcta \
--grm ${dir}/type_1_error/Test/UKBB_1Wan_gcta_1 --make-bK-sparse 0.05 \
--out ${dir}/type_1_error/Test/UKBB_1Wan_gcta_2  \
--thread-num 10
```


## fastGWA, 5Wan test, step 1and2
```python
dir="/home/lezh/dsmwpred/zly"

${dir}/software/gcta \
--bfile ${dir}/type_1_error/Test/UKBB_5Wan \
--autosome --maf 0.01 \
--make-grm --out ${dir}/type_1_error/Test/UKBB_5Wan_gcta_1 \
--thread-num 10

${dir}/software/gcta \
--grm ${dir}/type_1_error/Test/UKBB_5Wan_gcta_1 --make-bK-sparse 0.05 \
--out ${dir}/type_1_error/Test/UKBB_5Wan_gcta_2  \
--thread-num 10
```


## fastGWA, white test, step 1and2
```python
dir="/home/lezh/dsmwpred/zly"

${dir}/software/gcta \
--bfile ${dir}/type_1_error/Test/data_White \
--autosome --maf 0.01 \
--make-grm --out ${dir}/type_1_error/Test/data_White_gcta_1 \
--thread-num 10


${dir}/software/gcta \
--grm ${dir}/type_1_error/Test/data_White_gcta_1 --make-bK-sparse 0.05 \
--out ${dir}/type_1_error/Test/data_White_gcta_2  \
--thread-num 10

${dir}/software/gcta \
--grm ${dir}/type_1_error/Test/data_White_gcta_1 --make-bK-sparse 0.0001 \
--out ${dir}/type_1_error/Test/data_White_gcta_2_1e4  \
--thread-num 10



${dir}/software/gcta \
--grm ${dir}/type_1_error/Test/data_White_gcta_1 --make-bK-sparse 0.1 \
--out ${dir}/type_1_error/Test/data_White_gcta_2_01  \
--thread-num 10
```












# LDAK-thin
## LDAK-thin on each dataset 
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

${dir_LDAK} --bfile ${dir}/data_qc  --max-threads 4  --thin ${dir}/data_qc_thin --window-prune 0.98 --window-kb 100


" > ${dir}/scripts/LDAK_Thin_Step1and2_qc

# I am doing blabla
cd ${dir}/scripts/
sbatch LDAK_Thin_Step1and2_qc

dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 8:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"
source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir_LDAK} --bfile ${dir}/data_Black  --max-threads 4  --thin ${dir}/data_Black_thin --window-prune 0.98 --window-kb 100

" > ${dir}/scripts/LDAK_Thin_Step1and2_Black

# I am doing blabla
cd ${dir}/scripts/
sbatch LDAK_Thin_Step1and2_Black

dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 8:0:0
#SBATCH -c 4
#SBATCH -A dsmwpred
#SBATCH --constraint \"s05\"
source /home/lezh/miniconda3/etc/profile.d/conda.sh

${dir_LDAK} --bfile ${dir}/data_1Wan  --max-threads 4  --thin ${dir}/data_1Wan_thin --window-prune 0.98 --window-kb 100

" > ${dir}/scripts/LDAK_Thin_Step1and2_1Wan

# I am doing blabla
cd ${dir}/scripts/
sbatch LDAK_Thin_Step1and2_1Wan
```

```python
dir="/home/lezh/dsmwpred/zly"
awk < ${dir}/data_qc_thin.in '{print $1, 1}' > ${dir}/data_qc_thin.thin
awk < ${dir}/data_1Wan_thin.in '{print $1, 1}' > ${dir}/data_1Wan_thin.thin
awk < ${dir}/data_Black_thin.in '{print $1, 1}' > ${dir}/data_Black_thin.thin
```


# Generator LDAK-thin
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
  --weights ${dir}/data_qc_thin.thin  \
  --power -0.25 \
  --her 0.1 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --extract ${dir}/snps_1_to_12_qc.txt


  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_13_to_24/Trait_14 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_thin.thin  \
  --power -0.25 \
  --her 0.5 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_13_to_24/Trait_15 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_thin.thin  \
  --power -0.25 \
  --her 0.9 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_13_to_24/Trait_16 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_thin.thin  \
  --power -0.25 \
  --her 0.1 \
  --num-phenos 5 \
  --num-causals 10000 \
  --max-threads 8 \
  --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_13_to_24/Trait_17 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_thin.thin  \
  --power -0.25 \
  --her 0.5 \
  --num-phenos 5 \
  --num-causals 10000 \
  --max-threads 8 \
  --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_13_to_24/Trait_18 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_thin.thin  \
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
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 4:0:0
#SBATCH -c 8
#SBATCH -A dsmwpred

source /home/lezh/miniconda3/etc/profile.d/conda.sh

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_13_to_24/Trait_19   --bfile ${dir}/data_1Wan   --weights ${dir}/data_1Wan_thin.thin    --power -0.25   --her 0.1   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt
  
  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_13_to_24/Trait_20   --bfile ${dir}/data_1Wan    --weights ${dir}/data_1Wan_thin.thin    --power -0.25   --her 0.5   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK}    --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_13_to_24/Trait_21   --bfile ${dir}/data_1Wan    --weights ${dir}/data_1Wan_thin.thin    --power -0.25   --her 0.9   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK}    --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_13_to_24/Trait_22   --bfile ${dir}/data_1Wan    --weights ${dir}/data_1Wan_thin.thin    --power -0.25   --her 0.1   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK}    --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_13_to_24/Trait_23   --bfile ${dir}/data_1Wan    --weights ${dir}/data_1Wan_thin.thin    --power -0.25   --her 0.5   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK}    --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_13_to_24/Trait_24   --bfile ${dir}/data_1Wan    --weights ${dir}/data_1Wan_thin.thin    --power -0.25   --her 0.9   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  " > ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_13_to_24/Trait_qt_LDAK_19to24

# I am doing blabla
cd ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_13_to_24
sbatch Trait_qt_LDAK_19to24
```



## T19 - 24, Black
```python
######################################################################
Trait B19 - B24
######################################################################
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 4:0:0
#SBATCH -c 8
#SBATCH -A dsmwpred

source /home/lezh/miniconda3/etc/profile.d/conda.sh

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B19   --bfile ${dir}/data_Black   --weights ${dir}/data_Black_thin.thin    --power -0.25   --her 0.1   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt
  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B20   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_thin.thin    --power -0.25   --her 0.5   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B21   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_thin.thin    --power -0.25   --her 0.9   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B22   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_thin.thin    --power -0.25   --her 0.1   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B23   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_thin.thin    --power -0.25   --her 0.5   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_B24   --bfile ${dir}/data_Black    --weights ${dir}/data_Black_thin.thin    --power -0.25   --her 0.9   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_Black.txt

  " > ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_B1_to_B24/Trait_B19toB24

# I am doing blabla
cd ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_B1_to_B24
sbatch Trait_B19toB24


```



## T 37 - 48, LDAK, P001
```python
##############################################################################################
37 - 48
################################
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 4G
#SBATCH -t 2:0:0
#SBATCH -c 8
#SBATCH -A dsmwpred

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_37 --bfile ${dir}/data_qc --weights ${dir}/data_qc_thin.thin --power -0.25 --her 0.1 --num-phenos 5 \
  --num-causals 1000  --max-threads 8 --prevalence 0.01 --extract ${dir}/snps_1_to_12_qc.txt


  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_38 --bfile ${dir}/data_qc --weights ${dir}/data_qc_thin.thin --power -0.25 --her 0.5 --num-phenos 5 \
  --num-causals 1000 --max-threads 8 --prevalence 0.01 --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_39 --bfile ${dir}/data_qc --weights ${dir}/data_qc_thin.thin --power -0.25 \
  --her 0.9 --num-phenos 5 --num-causals 1000 --max-threads 8 --prevalence 0.01 --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_40 \
  --bfile ${dir}/data_qc --weights ${dir}/data_qc_thin.thin --power -0.25 --her 0.1 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.01 \
  --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_41 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_thin.thin \
  --power -0.25 \
  --her 0.5 \
  --num-phenos 5 \
  --num-causals 10000 \
  --max-threads 8 \
  --prevalence 0.01 \
  --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_42 --bfile ${dir}/data_qc --weights ${dir}/data_qc_thin.thin --power -0.25 --her 0.9 \
  --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.01 --extract ${dir}/snps_1_to_12_qc.txt

  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_43 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_thin.thin --power -0.25 --her 0.1 --num-phenos 5 --num-causals 10000 \
  --max-threads 8 --prevalence 0.01 --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt


  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_44 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_thin.thin --power -0.25 \
  --her 0.5 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.01 --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_45 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_thin.thin --power -0.25 --her 0.9 --num-phenos 5 --num-causals 10000 \
  --max-threads 8 --prevalence 0.01 --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_46 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_thin.thin  --power -0.25 \
  --her 0.1 --num-phenos 5 --num-causals 1000 --max-threads 8 --prevalence 0.01 \
  --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_47 \
  --bfile ${dir}/data_1Wan \
  --weights ${dir}/data_1Wan_thin.thin \
  --power -0.25 \
  --her 0.5 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --prevalence 0.01 \
  --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary/Trait_48 \
  --bfile ${dir}/data_1Wan \
  --weights ${dir}/data_1Wan_thin.thin \
  --power -0.25 \
  --her 0.9 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --prevalence 0.01 \
  --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

" > ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_25_to_48_Binary/Trait_37to48

# I am doing blabla
cd ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_25_to_48_Binary
sbatch Trait_37to48
```


## T 37 - 48, LDAK, P015
```python
##############################################################################################
37 - 48
################################
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 4G
#SBATCH -t 2:0:0
#SBATCH -c 8
#SBATCH -A dsmwpred

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_37 --bfile ${dir}/data_qc --weights ${dir}/data_qc_thin.thin --power -0.25 --her 0.1 --num-phenos 5 \
  --num-causals 1000  --max-threads 8 --prevalence 0.15 --extract ${dir}/snps_1_to_12_qc.txt
  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_38 --bfile ${dir}/data_qc --weights ${dir}/data_qc_thin.thin --power -0.25 --her 0.5 --num-phenos 5 \
  --num-causals 1000 --max-threads 8 --prevalence 0.15 --extract ${dir}/snps_1_to_12_qc.txt
  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_39 --bfile ${dir}/data_qc --weights ${dir}/data_qc_thin.thin --power -0.25 \
  --her 0.9 --num-phenos 5 --num-causals 1000 --max-threads 8 --prevalence 0.15 --extract ${dir}/snps_1_to_12_qc.txt
  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_40 \
  --bfile ${dir}/data_qc --weights ${dir}/data_qc_thin.thin --power -0.25 --her 0.1 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.15 \
  --extract ${dir}/snps_1_to_12_qc.txt
  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_41 \
  --bfile ${dir}/data_qc \
  --weights ${dir}/data_qc_thin.thin \
  --power -0.25 --her 0.5 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.15 --extract ${dir}/snps_1_to_12_qc.txt
  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_42 --bfile ${dir}/data_qc --weights ${dir}/data_qc_thin.thin --power -0.25 --her 0.9 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.15 --extract ${dir}/snps_1_to_12_qc.txt
  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_43 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_thin.thin --power -0.25 --her 0.1 --num-phenos 5 --num-causals 10000  --max-threads 8 --prevalence 0.15 --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt


  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_44 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_thin.thin --power -0.25 \
  --her 0.5 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.15 --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_45 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_thin.thin --power -0.25 --her 0.9 --num-phenos 5 --num-causals 10000 \
  --max-threads 8 --prevalence 0.15 --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_46 \
  --bfile ${dir}/data_1Wan --weights ${dir}/data_1Wan_thin.thin  --power -0.25 \
  --her 0.1 --num-phenos 5 --num-causals 1000 --max-threads 8 --prevalence 0.15 \
  --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_47 \
  --bfile ${dir}/data_1Wan \
  --weights ${dir}/data_1Wan_thin.thin \
  --power -0.25 \
  --her 0.5 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --prevalence 0.15 \
  --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

  ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_48 \
  --bfile ${dir}/data_1Wan \
  --weights ${dir}/data_1Wan_thin.thin \
  --power -0.25 \
  --her 0.9 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --prevalence 0.15 \
  --extract /home/lezh/dsmwpred/zly/snps_1_to_12_1Wan.txt

" > ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_25_to_48_Binary_P015/Trait_37to48

# I am doing blabla
cd ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_25_to_48_Binary_P015
sbatch Trait_37to48
```


## T 43 - 48 Black, LDAK, Prevalence = 0.01
```python 
##############################################################################################
B43 - B48
################################
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 4G
#SBATCH -t 2:0:0
#SBATCH -c 8
#SBATCH -A dsmwpred

  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_B43 \
  --bfile ${dir}/data_Black --weights ${dir}/data_Black_thin.thin --power -0.25 --her 0.1 --num-phenos 5 --num-causals 10000 \
  --max-threads 8 --prevalence 0.01  --extract ${dir}/snps_1_to_12_Black.txt

    ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_B44 \
  --bfile ${dir}/data_Black --weights ${dir}/data_Black_thin.thin --power -0.25 \
  --her 0.5 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.01  --extract ${dir}/snps_1_to_12_Black.txt

    ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_B45 \
  --bfile ${dir}/data_Black --weights ${dir}/data_Black_thin.thin --power -0.25 --her 0.9 --num-phenos 5 --num-causals 10000 \
  --max-threads 8 --prevalence 0.01  --extract ${dir}/snps_1_to_12_Black.txt

    ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_B46 \
  --bfile ${dir}/data_Black --weights ${dir}/data_Black_thin.thin  --power -0.25 \
  --her 0.1 --num-phenos 5 --num-causals 1000 --max-threads 8 --prevalence 0.01    --extract ${dir}/snps_1_to_12_Black.txt

    ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_B47 \
  --bfile ${dir}/data_Black \
  --weights ${dir}/data_Black_thin.thin \
  --power -0.25 \
  --her 0.5 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --prevalence 0.01  --extract ${dir}/snps_1_to_12_Black.txt

    ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_B48 \
  --bfile ${dir}/data_Black \
  --weights ${dir}/data_Black_thin.thin \
  --power -0.25 \
  --her 0.9 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --prevalence 0.01  --extract ${dir}/snps_1_to_12_Black.txt

" > ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_B25_to_B48_Binary/Trait_B43toB48

# I am doing blabla
cd ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_B25_to_B48_Binary
sbatch Trait_B43toB48
```


## Next: Run software on Binary Traits



# White dataset
## White thin
```python
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
${dir_LDAK} --bfile ${dir}/data_White  --max-threads 4  --thin ${dir}/data_White_thin --window-prune 0.98 --window-kb 100
awk < ${dir}/data_White_thin.in '{print $1, 1}' > ${dir}/data_White_thin.thin
```
## T19 - 24, White
```python
######################################################################
Trait W19 - W24
######################################################################
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 8G
#SBATCH -t 4:0:0
#SBATCH -c 8
#SBATCH -A dsmwpred

source /home/lezh/miniconda3/etc/profile.d/conda.sh

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_W19   --bfile ${dir}/data_White   --weights ${dir}/data_White_thin.thin    --power -0.25   --her 0.1   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_White.txt
  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_W20   --bfile ${dir}/data_White    --weights ${dir}/data_White_thin.thin    --power -0.25   --her 0.5   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_White.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_W21   --bfile ${dir}/data_White    --weights ${dir}/data_White_thin.thin    --power -0.25   --her 0.9   --num-phenos 5   --num-causals 1000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_White.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_W22   --bfile ${dir}/data_White    --weights ${dir}/data_White_thin.thin    --power -0.25   --her 0.1   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_White.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_W23   --bfile ${dir}/data_White    --weights ${dir}/data_White_thin.thin    --power -0.25   --her 0.5   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_White.txt

  ${dir_LDAK}   --make-phenos /home/lezh/dsmwpred/zly/type_1_error/Multi_Traits/Trait_B1_to_B24/Trait_W24   --bfile ${dir}/data_White    --weights ${dir}/data_White_thin.thin    --power -0.25   --her 0.9   --num-phenos 5   --num-causals 10000   --max-threads 8   --extract /home/lezh/dsmwpred/zly/snps_1_to_12_White.txt

  " > ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_B1_to_B24/Trait_W19toW24

# I am doing blabla
cd ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_B1_to_B24
sbatch Trait_W19toW24


```


## T 43 - 48 White, LDAK, Prevalence = 0.01
```python 
##############################################################################################
W43 - W48
################################
dir_LDAK="/home/lezh/snpher/faststorage/ldak5.2.linux"
dir="/home/lezh/dsmwpred/zly"
echo "#"'!'"/bin/bash
#SBATCH --mem 4G
#SBATCH -t 2:0:0
#SBATCH -c 8
#SBATCH -A dsmwpred

  ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_W43 \
  --bfile ${dir}/data_White --weights ${dir}/data_White_thin.thin --power -0.25 --her 0.1 --num-phenos 5 --num-causals 10000 \
  --max-threads 8 --prevalence 0.01  --extract ${dir}/snps_1_to_12_White.txt

    ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_W44 \
  --bfile ${dir}/data_White --weights ${dir}/data_White_thin.thin --power -0.25 \
  --her 0.5 --num-phenos 5 --num-causals 10000 --max-threads 8 --prevalence 0.01  --extract ${dir}/snps_1_to_12_White.txt

    ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_W45 \
  --bfile ${dir}/data_White --weights ${dir}/data_White_thin.thin --power -0.25 --her 0.9 --num-phenos 5 --num-causals 10000 \
  --max-threads 8 --prevalence 0.01  --extract ${dir}/snps_1_to_12_White.txt

    ${dir_LDAK} --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_W46 \
  --bfile ${dir}/data_White --weights ${dir}/data_White_thin.thin  --power -0.25 \
  --her 0.1 --num-phenos 5 --num-causals 1000 --max-threads 8 --prevalence 0.01    --extract ${dir}/snps_1_to_12_White.txt

    ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_W47 \
  --bfile ${dir}/data_White \
  --weights ${dir}/data_White_thin.thin \
  --power -0.25 \
  --her 0.5 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --prevalence 0.01  --extract ${dir}/snps_1_to_12_White.txt

    ${dir_LDAK} \
  --make-phenos ${dir}/type_1_error/Multi_Traits/Trait_B25_to_B48_Binary/Trait_W48 \
  --bfile ${dir}/data_White \
  --weights ${dir}/data_White_thin.thin \
  --power -0.25 \
  --her 0.9 \
  --num-phenos 5 \
  --num-causals 1000 \
  --max-threads 8 \
  --prevalence 0.01  --extract ${dir}/snps_1_to_12_White.txt

" > ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_B25_to_B48_Binary/Trait_W43toW48

# I am doing blabla
cd ${dir}/scripts/type_1_error_new/Multi_Traits/Trait_B25_to_B48_Binary
sbatch Trait_W43toW48
```






# 5.9 Missions
1. Write the introduction   
2. Analyze META on other traits
3. Try MR META
4. To run on real traits(Height, Urate, Urate_binary)
5. fastGWA email
6. White 的GCTA
7. Average chisq-test 搞定





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

