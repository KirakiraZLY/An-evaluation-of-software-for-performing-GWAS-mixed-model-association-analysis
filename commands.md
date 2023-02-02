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


## Softwares Already Downloaded
Ref: https://www.frontiersin.org/articles/10.3389/fgene.2022.897210/full   
BOLT, GENESIS(Rstudio), REGENIE(conda), plink, ldak   
**Note:**   
BOLT: LMM和REML. https://storage.googleapis.com/broad-alkesgroup-public/BOLT-LMM/downloads/BOLT-LMM_v2.4_manual.pdf.    
GENESIS: GWAS, using GRM to account for known and unknown relatedness in the data.   
REGENIE: whole-genome regression model for quantitative and binary phenotypes. https://rgcgithub.github.io/regenie/recommendations/

## Week 1, 2023/1/31
### Start by QC(genomeDK, Plink)
Filter out SNPs with genotype missingness >10%, samples with >10% missingness, MAF <5%, minor allele count(MAC) <100, HWE p-value exceeding 1e-15.   
`./software/plink --bfile data --geno 0.1 --mind 0.1 --maf 0.05 --mac 100 --hwe 1e-15 --make-bed --out data_qc`  
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
`./software/plink --vcf data_qc_vcf.vcf --double-id --allow-extra-chr --set-missing-var-ids @:# --extract data_qc.prune.in --pca --make-bed --out data_qc_pca`   

### regenie
