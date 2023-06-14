# Commands for Master's thesis
## Week 1

### Start by QC(genomeDK, Plink)
Filter out SNPs with genotype missingness >10%, samples with >10% missingness, MAF <5%, minor allele count(MAC) <100, 不做这个HWE p-value exceeding 1e-15.(MAF可以改成1%)   
```python
dir="/home/lezh/dsmwpred/zly"
${dir}/software/plink --bfile data --geno 0.001 --mind 0.001 --maf 0.05 --mac 100 --make-bed --out data_qc_nomissing
```  
Output: data_qc   
