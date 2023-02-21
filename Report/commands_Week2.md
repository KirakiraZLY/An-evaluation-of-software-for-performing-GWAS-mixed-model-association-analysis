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
not yet   
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
./software/BOLT-LMM_v2.4/bolt --bfile=./1000g/1000g_out --phenoFile=./1000g/1000g_out.pheno --phenoCol=Phenotype --covarFile=covar1.covars --qCovarCol --lmmForceNonInf --statsFile=1000g_bolt --maxModelSnps 9000000
```
Since the number of SNPs is 6M here(>1M), adding --maxModelSnps option.   

### Bolt lmm ukbb
```python
./software/BOLT-LMM_v2.4/bolt --bfile=data_qc --phenoFile=height1.pheno --phenoCol=Phenotype --covarFile=covar1.covars --qCovarCol --lmmForceNonInf --statsFile=data_bolt_height --maxModelSnps 9000000
```
Since the number of SNPs is 6M here(>1M), adding --maxModelSnps option. 