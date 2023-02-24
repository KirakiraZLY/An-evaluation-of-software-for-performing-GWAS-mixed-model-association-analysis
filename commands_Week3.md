# Commands for Master's thesis
## Week 3
2.24 - 3.1

### 2.24
1. Finished running: ukbb binary bolt, ./ukbb_binary_test
2. Manhattan and QQ plot of 1, bad result.

Command for 1 is:   
### Bolt lmm ukbb binary(--covarFile=covar1.covars --qCovarCol)
```python
./software/BOLT-LMM_v2.4/bolt --bfile=./ukbb_binary_test/data_qc --phenoFile=./ukbb_binary_test/data_binary_1.pheno --phenoCol=Phenotype --lmmForceNonInf --LDscoresUseChip --statsFile=./ukbb_binary_test/data_qc_bolt_binary --maxModelSnps 9000000
```
Since the number of SNPs is 6M here(>1M), adding --maxModelSnps option.