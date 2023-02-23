# Commands for Master's thesis
## Week 2
Since there are a lot problems occuring with UKBB data, I use 1000g as a demo. If it can work, I'll run on UKBB.   
   
   
You may also specify some requirements for the job, such as the amount of memory that should be allocated:   
srun --account lezh --mem 16g --pty bash   


### fastGWA
https://yanglab.westlake.edu.cn/software/gcta/#fastGWA   
1. After download, see: **gcta** in dsmwpred/zly/software   
2. GCTA-GRM: calculating the genetic relationship matrix (GRM) from all the autosomal SNPs:   
```python
./software/gcta --bfile ./1000g/1000g_out --chr 1 --maf 0.01 --make-grm --out ./1000g/1000g_out_chr1 --thread-num 10  
./software/gcta --bfile data_qc --chr 2 --maf 0.01 --make-grm --out data_qc_chr2 --thread-num 10
```
```python
./software/gcta --bfile data_qc --chr 22 --maf 0.01 --make-grm --out data_qc_chr22 --thread-num 10
Output: .grm.bin, .grm.N.bin, .grm.id   
```
3. To generate a sparse GRM from SNP data:
  ```python
./software/gcta \
--bfile ./1000g/1000g_out \
--autosome --maf 0.01 \
--make-grm --out ./1000g/1000g_out_gcta \
--thread-num 10
```
```python  
./software/gcta --grm ./1000g/1000g_out_gcta --make-bK-sparse 0.05 --out ./1000g/1000g_out_grm_gcta   
```

I didn't use PCs
```python
./software/gcta --bfile ./1000g/1000g_out --grm-sparse ./1000g/1000g_out_grm_gcta --fastGWA-mlm --pheno ./1000g/1000g_out.pheno --thread-num 10 --out ./1000g/1000g_fastgwa_height   
```

I ran fastGWA as the first one, and it worked quickly: in 22.8 sec, with 2504 individuals. So it could also work on UKBB, and 900 times of the time? So it should work in 5 hours, by theory...


### PCA
```python
  ./software/plink \
  --vcf data_qc_vcf.vcf \
  --double-id --allow-extra-chr \
  --set-missing-var-ids @:# \
  --extract data_qc.prune.in \
  --pca --make-bed \
  --out data_prune_pca   
```
   
After this, output: .eigenval & .eigenvec   
Plot by ggplot.   
   

### PCA for population prediction, K-means
Using K-means to cluster populations into 4 groups, with data of PC1 and PC2.   

## Simulate Phenotype with LDAK
To simulate binary traits of UKBB, of the use of REGENIE.   
```python
  ./software/ldak5.XXX \
  --make-phenos data_binary \
  --bfile data_qc \
  --prevalence 0.1 \
  --ignore-weights YES \
  --power -1 \
  --her 0.5 \
  --num-phenos 1 \
  --num-causals 100
```   
Phenotypes saved in data_binary.pheno, with liabilities in data_binary.liab, breeding values in data_binary.breed and effect sizes in data_binary.effects   


### Regenie for 1000g, quantitative
done   
1. 
```python
  regenie \
  --step 1 \
  --force-step1  \
  --bed ./1000g/1000g_out   \
  --phenoFile ./1000g/1000g_out_1.pheno   \
  --bsize 100   \
  --out ./1000g/1000g_regenie_out
```
   
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式, FID, IID, Phenotype)   
Convert .bed to .bgen: ./software/plink2 --bfile ./1000g/1000g_out --export bgen-1.2 --out ./1000g/1000g_out   
**Output**: 1000g_regenie_out_pred.list   
2. 
```python
  regenie \
  --step 2 \
  --bgen ./1000g/1000g_out.bgen \
  --phenoFile ./1000g/1000g_out_1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ./1000g/1000g_regenie_out_pred.list \
  --out ./1000g/1000g_regenie_out_firth
```
Output: data_regenie_out_firth_Phenotype.regenie   
然后就是画图还没做

### Regenie for UKBB
done   
1. 
```python
   regenie \
  --step 1 \
  --bed data_qc \
  --covarFile covar1.covars \
  --phenoFile data_binary_1.pheno \
  --bsize 100 \
  --bt \
  --out data_regenie_out_binary  
``` 
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen: ./software/plink2 --bfile data_qc --export bgen-1.2 --out data_qc   
**Output**: data_regenie_out_binary_pred.list
2. 
```python
   regenie \
  --step 2 \
  --bgen data_qc.bgen \
  --phenoFile data_binary_1.pheno \
  --bsize 200 \
  --bt \
  --firth --approx \
  --pThresh 0.01 \
  --pred data_regenie_out_binary_pred.list \
  --out data_regenie_out_binary_firth
```
Output: data_regenie_out_binary_firth_Phenotype.regenie


### GEMMA
not yet, GEMMA is too slow to run, give up.   
Before using GEMMA, the 6th column of .fam should be replaced by real phenotypes. 先把Phenotype替换到.fam文件第6行   
1. Calculate Kinship Matrix    
```python
gemma -bfile ./1000g/1000g_out -gk 2 -o ./1000g/1000g_gemma
```   
2. LMM   
Move Kinship out to the present location.   
LMM analysis:   
```python
gemma -bfile ./1000g/1000g_out -k data_gemma_height.sXX.txt -lmm 1 -c covars.covar -o GEMMA_GWAS
```

Again, try with another command:
1.   
```python
gemma -bfile data_qc -gk 2 -o data_gemma_height
```
2.   
```python
gemma -bfile data_gemma_height -k 1000g_out.sXX.txt -lmm 1 -o data_gemma_height_yield
```

### Bolt lmm
```python
./software/BOLT-LMM_v2.4/bolt --bfile=./1000g/1000g_out --phenoFile=./1000g/1000g_out.pheno --phenoCol=Phenotype --lmmForceNonInf --statsFile=1000g_bolt --maxModelSnps 9000000
```
Since the number of SNPs is 6M here(>1M), adding --maxModelSnps option.   
Output: ./1000g/1000g_bolt   


### Bolt lmm ukbb(--covarFile=covar1.covars --qCovarCol) 跑通了, 回去重新跑
```python
./software/BOLT-LMM_v2.4/bolt --bfile=data_qc --phenoFile=height1.pheno --phenoCol=Phenotype --lmmForceNonInf --LDscoresUseChip --statsFile=data_height_bolt --maxModelSnps 9000000
```
Since the number of SNPs is 6M here(>1M), adding --maxModelSnps option. 

# Binary Trait test for UKBB
## Softwares Using
Regenie, fastGWA, Bolt-lmm   
Location: ./ukbb_binary_test/
## Regenie for binary UKBB
Already done from above.   
## fastGWA for binary UKBB
### fastGWA
运行3和4   
https://yanglab.westlake.edu.cn/software/gcta/#fastGWA   
1. After download, see: **gcta** in dsmwpred/zly/software   
2. GCTA-GRM: calculating the genetic relationship matrix (GRM) from all the autosomal SNPs:   
```python
./software/gcta --bfile ./1000g/1000g_out --chr 1 --maf 0.01 --make-grm --out ./1000g/1000g_out_chr1 --thread-num 10  
./software/gcta --bfile data_qc --chr 2 --maf 0.01 --make-grm --out data_qc_chr2 --thread-num 10
```
```python
./software/gcta --bfile data_qc --chr 22 --maf 0.01 --make-grm --out data_qc_chr22 --thread-num 10
Output: .grm.bin, .grm.N.bin, .grm.id   
```
3. To generate a sparse GRM from SNP data:
  ```python
./software/gcta \
--bfile ./ukbb_binary_test/data_qc \
--autosome --maf 0.01 \
--make-grm --out ./ukbb_binary_test/data_qc_gcta \
--thread-num 10
```
```python  
./software/gcta --grm ./ukbb_binary_test/data_qc_gcta --make-bK-sparse 0.05 --out ./ukbb_binary_test/data_qc_grm_gcta   
```
done
4. I didn't use PCs
```python
./software/gcta --bfile ./ukbb_binary_test/data_qc --grm-sparse ./ukbb_binary_test/data_qc_grm_gcta --fastGWA-mlm --pheno ./ukbb_binary_test/data_binary.pheno --thread-num 10 --out ./ukbb_binary_test/data_qc_fastgwa_binary   
```

### Bolt lmm ukbb binary(--covarFile=covar1.covars --qCovarCol) 跑通了, 回去重新跑
```python
./software/BOLT-LMM_v2.4/bolt --bfile=./ukbb_binary_test/data_qc --phenoFile=./ukbb_binary_test/data_binary_1.pheno --phenoCol=Phenotype --lmmForceNonInf --LDscoresUseChip --statsFile=./ukbb_binary_test/data_qc_bolt_binary --maxModelSnps 9000000
```
Since the number of SNPs is 6M here(>1M), adding --maxModelSnps option.





# Ancestry Inference
## Extract .bed and .fam into a single population
In the folder: ./ukbb_by_ancestry
```python
./software/plink --bfile ./ukbb_by_ancestry/data_qc --noweb --keep ./ukbb_by_ancestry/data_qc_1.fam --recode --make-bed --out ./ukbb_by_ancestry/data_region1
```
data_1 is the data of population 1, and there will also be data_2 ...   

## Download softwares for ancestry inference
ADMIXTURE: admixture_env   
fastSTRUCTURE: faststructure_env (py2)   
### ADMIXTURE
Dict: ./dsw/zly/ADMIXTURE   
4 Populations   
```python
admixture data_qc.bed 4
```

## Feb 23th
1. Run ADMIXTURE on ukbb whole and Bolt-lmm on binary trait + ukbb   
2. Extract **Region 1** out from .fam   
3. Question: How to evaluate teh accuracy of K-means?   
   How to evaluate the performance between PCA+Kmeans and ADMIXTURE?
4. By step2, I got **region 1** -> Run REGENIE again on data_region1, see difference.

### REGENIE on data_region1
Using Binary Traits   
1. 
```python
   regenie \
  --step 1 \
  --bed ./ukbb_by_ancestry/data_region1 \
  --covarFile covar1.covars \
  --phenoFile data_binary_1.pheno \
  --bsize 100 \
  --bt \
  --out ./ukbb_by_ancestry/data_region1_regenie_out_binary  
``` 
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen: ./software/plink2 --bfile ./ukbb_by_ancestry/data_region1 --export bgen-1.2 --out ./ukbb_by_ancestry/data_region1    
**Output**: data_region1_regenie_out_binary_pred.list
1. 
```python
   regenie \
  --step 2 \
  --bgen ./ukbb_by_ancestry/data_region1.bgen \
  --phenoFile data_binary_1.pheno \
  --bsize 200 \
  --bt \
  --firth --approx \
  --pThresh 0.01 \
  --pred ./ukbb_by_ancestry/data_region1_regenie_out_binary_pred.list \
  --out ./ukbb_by_ancestry/data_region1_regenie_out_binary_firth
```
Output: data_regenie_out_binary_firth_Phenotype.regenie