# Commands for Master's thesis
## An evaluation of software for performing GWAS mixed model association analysis  
## Date: 2023/2 to 2023/6

## Date: 2023/1/30
1. Copy folder UKBB: `cp -r data/ukbb zly`
2. Download ldak5.XXX via: http://dougspeed.com/short/   
3. Pheno: awake, bmi, chron, ever, fvc, **height**, hyper, imp, neur, pulse, quals, reaction, sbp, snoring.   
三件套Three sets: geno, geno2   

## Week 1, 2023/1/31
### Start by QC(genomeDK, Plink)
`./software/plink --bfile data --geno 0.2 --mind 0.2 --maf 0.05 --make-bed --out data_qc`  
Output: data_qc   

