# Commands for Master's thesis
## An evaluation of software for performing GWAS mixed model association analysis  
## Date: 2023/2 to 2023/6

## Date: 2023/1/30
1. Copy folder UKBB: `cp -r data/ukbb zly`
2. Download ldak5.XXX via: http://dougspeed.com/short/   
3. Pheno: awake, bmi, chron, ever, fvc, **height**, hyper, imp, neur, pulse, quals, reaction, sbp, snoring.   
三件套Three sets: geno, geno2 

## Env
master-thesis   
regenie_env   

## Softwares Already Downloaded
Ref: https://www.frontiersin.org/articles/10.3389/fgene.2022.897210/full   
BOLT, GENESIS(Rstudio), REGENIE(conda), plink, ldak   
**Note:**   
BOLT: LMM和REML. https://storage.googleapis.com/broad-alkesgroup-public/BOLT-LMM/downloads/BOLT-LMM_v2.4_manual.pdf.    
GENESIS: GWAS, using GRM to account for known and unknown relatedness in the data.   
REGENIE: whole-genome regression model for quantitative and binary phenotypes. https://rgcgithub.github.io/regenie/recommendations/

## Week 1, 2023/1/31
### Start by QC(genomeDK, Plink)
Filter out SNPs with genotype missingness >10%, samples with >10% missingness, MAF <5%, minor allele count(MAC) <100, 不做这个HWE p-value exceeding 1e-15.(MAF可以改成1%)   
`./software/plink --bfile data --geno 0.1 --mind 0.1 --maf 0.05 --mac 100 --make-bed --out data_qc`  
Output: data_qc   


### VCF
`./software/plink --bfile data_qc --recode vcf-iid --out data_qc_vcf`   
Output: data_qc_vcf   
Now we have a fully filtered VCF we can start some analyses with it.    
### Identify prune sites
--indep-pairwise demo: the first argument, 50 denotes we have set a window of 50 Kb.   The second argument, 2 is our window step size - meaning we move 2 bp each time we calculate linkage.   
Finally, 0.2 represents r2 threshold.   
`./software/plink --vcf data_qc_vcf.vcf --double-id --allow-extra-chr --set-missing-var-ids @:# --indep-pairwise 50 2 0.2 --out data_qc`
### PCA
Too large to run in Plink   
`./software/plink --vcf data_qc_vcf.vcf --double-id --allow-extra-chr --set-missing-var-ids @:# --extract data_qc.prune.in --pca --make-bed --out data_qc_pca`   

### Check family relatedness
./software/plink --bfile data_qc --genome --min 0.0625 --pheno height.pheno --mpheno 2 --allow-no-sex

### Missingliness
./software/plink --bfile data_qc --missing --out data_qc


### Association study --- height
https://blog.csdn.net/qq_41954318/article/details/107859900   

./software/plink --bfile data_qc --linear --pheno height.pheno --allow-no-sex --out data_qc_height

./software/plink --bfile data_qc --assoc --out data_qc

**Output**: data_qc_height.assoc.linear
然后做manhattan和qq

### REGENIE
