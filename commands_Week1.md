# Commands for Master's thesis
## Week 1
https://zhuanlan.zhihu.com/p/380709653   
### Download nextflow
https://github.com/genepi/nf-gwas   
https://www.nextflow.io/docs/latest/getstarted.html#installation   

### Start by QC(genomeDK, Plink)
Filter out SNPs with genotype missingness >10%, samples with >10% missingness, MAF <5%, minor allele count(MAC) <100, 不做这个HWE p-value exceeding 1e-15.(MAF可以改成1%)   
`./software/plink --bfile data --geno 0.1 --mind 0.1 --maf 0.05 --mac 100 --make-bed --out data_qc`  
Output: data_qc   

### Missingness
./software/plink --bfile  data_qc --missing --out data_qc



### fastGWA
https://yanglab.westlake.edu.cn/software/gcta/#fastGWA   
1. After download, see: **gcta** in dsmwpred/zly/software   
2. GCTA-GRM: calculating the genetic relationship matrix (GRM) from all the autosomal SNPs:   
./software/gcta --bfile data_qc --chr 1 --maf 0.01 --make-grm --out data_qc_chr1 --thread-num 10  
./software/gcta --bfile data_qc --chr 2 --maf 0.01 --make-grm --out data_qc_chr2 --thread-num 10
...
./software/gcta --bfile data_qc --chr 22 --maf 0.01 --make-grm --out data_qc_chr22 --thread-num 10
Output: .grm.bin, .grm.N.bin, .grm.id   
3. To generate a sparse GRM from SNP data:
./software/gcta --bfile data_qc --autosome --maf 0.01 --make-grm --out data_qc_gcta --thread-num 10   
./software/gcta --grm data_qc_gcta --make-bK-sparse 0.05 --out sp_grm_gcta   

I didn't use PCs(--qcovar covar.covars)
./software/gcta --bfile data_qc --grm-sparse sp_grm_gcta --fastGWA-mlm --pheno height.pheno  --thread-num 10 --out data_fastgwa_height

### Plink
done
1. PCA
```./software/plink --bfile data_qc --pca 6 --out data_qc```   
Output first 6 PCs, with 2 files: .eigenval and .eigenvec   
While since we have covars.covar, skip it
2. assoc test   
```./software/plink --bfile data_qc --linear --pheno height.pheno --allow-no-sex --out data_plink_height```   


### Regenie
done
1. regenie \
  --step 1 \
  --bed data_qc \
  --covarFile covar1.covars \
  --phenoFile height1.pheno \
  --bsize 100 \
  --out data_regenie_out   
  Since .pheno file needs FID and IID, I copied it and renamed height1.pheno with the titles.(因为.pheno需要FID和IID，就复制了一个height1.pheno文件并更改格式)   
Convert .bed to .bgen: ./software/plink2 --bfile data_qc --export bgen-1.2 --out data_qc   
**Output**: data_regenie_out_pred.list
2. regenie \
  --step 2 \
  --bgen data_qc.bgen \
  --covarFile covar1.covars \
  --phenoFile height1.pheno \
  --bsize 200 \
  --qt \
  --firth --approx \
  --pThresh 0.01 \
  --pred data_regenie_out_pred.list \
  --out data_regenie_out_firth
Output: data_regenie_out_firth_Phenotype.regenie

### GEMMA
not yet
Before using GEMMA, the 6th column of .fam should be replaced by real phenotypes. 先把Phenotype替换到.fam文件第6行   
1. Calculate Kinship Matrix    
```gemma -bfile data_qc -gk 2 -o data_gemma_height```   
2. LMM   
Move Kinship out to the present location.   
LMM analysis:   
```gemma -bfile data_qc -k data_gemma_height.sXX.txt -lmm 1 -c covars.covar -o GEMMA_GWAS```

Again, try with another command:
1. gemma -bfile data_qc -gk 2 -o data_gemma_height
2. gemma -bfile data_gemma_height -k 1000g_out.sXX.txt -lmm 1 -o data_gemma_height_yield

### Bolt-lmm
not yet
./software/BOLT-LMM_v2.4/bolt --bfile=data_qc --phenoFile=height1.pheno --phenoCol=Phenotype --covarFile=covar1.covars --qCovarCol --lmmForceNonInf --statsFile=data_bolt_height