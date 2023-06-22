# An-evaluation-of-software-for-performing-GWAS-mixed-model-association-analysis
Master's thesis   
Date: 2023-2 to 2023-6   

## Project Description
The most common way to test SNPs for association with a phenotype is via classical association analysis (i.e., least 
squares regression). However, it is now increasingly common to instead use mixed-model analyses (MMA). The main 
advantage of MMA is that it reduces false positives due to population structure and relatedness. Further, it can increase 
power to detect (because instead of testing SNPs individually, it uses a multi-SNP model).    

Objective 1 – This project will first evaluate different MMA software (e.g., Bolt-LMM, SAIGE, REGENIE) on large scale 
data (e.g., 300k individuals and 600k SNPs from UK Biobank) for a wide variety of traits (both simulated and real). 
Methods will be compared based on type 1 error, power and speed.    

Objective 2 – This project will compare strategies for analyzing multi-ancestry datasets. In particular, it will quantify the 
power increase (or decrease) of MMAA (analyzing all individuals together) with per-ancestry analyses (e.g., analyze 
European, African and Asian separately, then meta-analyse the three sets of results). In particular, it will investigate 
whether the optimum strategy depends on consistency of genetic architecture across ancestries.    

Objective 3 – This project will construct prediction models (PRS) computed using the results of MMA, and compare their 
accuracy (and transferability across populations) with PRS computed from classical association analysis.   

      
## Abstract
Genome-wide association studies (GWAS) are statistical methods used to identify associations be- tween genes and traits or specific diseases. Two commonly employed methods for GWAS are linear regression (LR) and mixed model analysis (MMA), each with distinct capabilities in preventing false positives, statistical power, and eﬀiciency. This study explores the advantages and limita- tions of different software tools in assessing various traits under different conditions, including the number of individuals, the number of causal single-nucleotide polymorphisms (SNPs), heritability, heritability model, and quantitative or binary traits. For linear regression, I selected software tools: Plink and LDAK, while for MMA, I evaluated Bolt-lmm, Bolt-lmm-inf, Regenie, and fastGWA. The population data consisted of 66,688 individuals from a multi-ancestry (admixed) population from the UK Biobank. I employed PCA + K-means clustering to stratify the admixed population into five single-ancestry population datasets to compare the performance of the software tools under dif- ferent population structures. The evaluated criteria included Type I error, statistical power, time, and memory usage. I also discussed the performance of Multi-ancestry Meta-analysis (MAMA) in assessing the multi-ancestry population by combining association test results from multiple single- ancestry groups. My study revealed that fastGWA is not suitable for assessing multi-ancestry populations but can provide feasible statistical power with eﬀicient time usage when evaluating single-ancestry (homogeneous) populations. Bolt-lmm exhibited the slowest speed but performed well in the evaluation of admixed population. Regenie showed limited performance in controlling Type I error and statistical power, making it less favourable. Furthermore, my study demonstrated that MAMA can enhance statistical power by incorporating a large number of individuals from other ethnic groups when the sample size of a specific ethnic group is insuﬀicient, although it may limit the detection ability for the major population. Moreover, MAMA is not an optimal choice in the presence of significant trait heterogeneity. In comparison to MMA software such as Bolt-lmm, MAMA exhibited a more conservative detection ability in admixed populations. Finally, I utilized the results from MMA analyses to construct a polygenic risk score (PRS) model using the Clumping
+ Threshold (C+T) method, which enables the prediction of complex trait likelihoods for diverse population genotypes. I tested the performance of PRS by Plink with the C+T method on different population structures and software tools. I suggest that the choice of training method should be based on a specific population structure.

