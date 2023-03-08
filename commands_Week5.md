# Commands for Master's thesis
## Week 5
三月七号 - 三月十五号   
## Urate, Meta-analysis
No significant loci found by Regenie.

## Bolt, height
### Chinese
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_Chinese --phenoFile=${dir}/MAMA/height1.pheno --phenoCol=Phenotype --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Height/data_Chinese_bolt_height
```
### AsianSWC
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_SWC --phenoFile=${dir}/MAMA/height1.pheno --phenoCol=Phenotype --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Height/data_AsianSWC_bolt_height
```
### White
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_White --phenoFile=${dir}/MAMA/height1.pheno --phenoCol=Phenotype --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Height/data_White_bolt_height
```
### Black
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_Black --phenoFile=${dir}/MAMA/height1.pheno --phenoCol=Phenotype --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Height/data_Black_bolt_height
```
### Mixed
```python
${dir}/software/BOLT-LMM_v2.4/bolt --bfile=${dir}/MAMA/Bolt_Height/data_Mixed --phenoFile=${dir}/MAMA/height1.pheno --phenoCol=Phenotype --lmmForceNonInf --LDscoresUseChip --statsFile=${dir}/MAMA/Bolt_Height/data_Mixed_bolt_height
```