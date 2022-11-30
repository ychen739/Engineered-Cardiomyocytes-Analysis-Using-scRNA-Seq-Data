# Engineered-Cardiomyocytes-Analysis-Using-scRNA-Seq-Data

## Research Question 1: How pure are the engineered cardiomyocytes? ##
The pySCN package was used to validate the purity of cardiomyocyte (CM) cells from Stone’s subsampled 5000 cells data. pySCN was trained with a reference dataset from [Tabula Muris](https://www.czbiohub.org/tabula-muris/). 

184 cells in the dataset were recognized as CM cells with major enrichment in the batch 6 cell (day 14) population. A large number of cells in Stone et al. \[1\] 's study are random cells which are not recognized by pySCN. This is sensible as the cells were analyzed in different time points and the majority of the cells are still in less differentiated transition or undifferentiated states. By performing the comparison between the Stone’s engineered CMs and the reference data, we can conclude that the engineered cardiomyocytes have relatively poor purity. 

In terms of exploring the dataset, dimensionality reduction of Stone’s engineered CMs with uniform manifold approximation and projection (UMAP) revealed that clusters are formed for certain cell types. 


## Research Question 2: How mature are the engineered cardiomyocytes? ##
The CM cells were selected from the previous procedure. The second step is to determine the temporal maturity of the CM cells. Using the entropy method described in Kannan et al. [2] ’s paper and the featured CM maturation TF (transcription factor) markers from Padula et al. [3] ’s paper, 
Cells with higher maturity tend to have lower entropy values. The engineered CM cells are relatively less mature with the majority of cells enriched at early time points, e14, e18 and p0 stages. Only a few cells are more mature.


## Research Question 3: What genetic alterations could improve the engineered cardiomyocytes? How well do CellOracle’s predicted fold changes correspond to what would actually happen? ##
1) CellOracle was trained with Kannan’s perinatal reference dataset. 18 CM characteristic transcription factor-targets networks [3] were added to the Oracle object for CM cells’ GRN activation.

2) Then we showcase the network perturbation on the evaluation dataset from Wu et al. by knocking out the Prdm16 expression. The inner product score was used as an indicator of change in cell state. A positive value indicates change in a similar direction whereas a negative value indicates opposing cell state transfer. Our results show that with later CM state (larger pseudotime value), CM cells are more sensitive to the treatment of Prdm16 knockout, as signified by the lower inner product over increased pseudotime value. This is consistent with the wet lab result conducted by Wu et al. [4], where Prdm16 is required to maintain cardiomyocyte identity for left ventricle. 

3) We utilized the default base gene regulatory network inserted in the CellOracle package. We ranked the usefulness of three TFs (Foxo1, Clock, Prdm1) by the average inner product scores from high to low. The most useful TF is Foxo1 indicated by the lowest inner product, meaning Foxo1 is required. This observation contradicts the previous study held by Uosaki et al (2015, Transcriptional landscape of Cardiomyocyte Maturation), where Foxo1 expression is decreased in neonate-adult CM cells, suggesting that low level Foxo1 is required for CM maturation. This may be explained by the different roles of Foxo1 at different maturation stages, where Foxo1 is required for early CM lineage commitment (as the majority of the mouse CMs are in early developmental stages) but should be decreased when CM cells undergo later stage maturation. Another rationale is that Uosaki et al’s study exploits human cells whereas the tested dataset is from mouse cells. Discrepancy of the roles of TFs in CM development across species is possible. Since the scores are all negative, these three TFs are all beneficial to drive the maturation of CM cells. We only tested the perturbation of three TFs due to lack of computational power. All TFs in the dataset would be tested for knockout and overexpression simulation whenever there is enough computational power.


## Research Question 4: How can the computational methods be translated to help engineer human cardiomyocytes? ##
Same assessments and TF screening methods from question 1 to 3 were applied to human iPSCs. However, initially, we performed gene mapping for human cells on mouse cells as the two species have different names for orthologs.

Since the scores are all positive, knockout of each of the four TFs (Foxo1, Prdm1, Cux1, Ctcf) cannot provide enough improvement for the maturity of CMs, suggesting that they should be absent in order to support CM cells maturation. This result for Foxo1 is especially consistent with the previous result obtained by Uosaki et al (2015, Transcriptional landscape of Cardiomyocyte Maturation). Foxo1 was found to be decreased in expression in neonatal adult CM cells.

## References
\[1\] Stone NR, Gifford CA, Thomas R, Pratt KJB, Samse-Knapp K, Mohamed TMA, Radzinsky EM, Schricker A, Ye L, Yu P, van Bemmel JG, Ivey KN, Pollard KS, Srivastava D. Context-Specific Transcription Factor Functions Regulate Epigenomic and Transcriptional Dynamics during Cardiac Reprogramming. Cell Stem Cell. 2019 Jul 3;25(1):87-102.e9. doi: 10.1016/j.stem.2019.06.012. PMID: 31271750; PMCID: PMC6632093.

\[2\] Kannan S, Farid M, Lin BL, Miyamoto M, Kwon C (2021) Transcriptomic entropy benchmarks stem cell-derived cardiomyocyte maturation against endogenous tissue at single cell level. PLOS Computational Biology 17(9): e1009305. https://doi.org/10.1371/journal.pcbi.1009305

\[3\] Padula SL, Velayutham N, Yutzey KE. Transcriptional Regulation of Postnatal Cardiomyocyte Maturation and Regeneration. Int J Mol Sci. 2021 Mar 23;22(6):3288. doi: 10.3390/ijms22063288. PMID: 33807107; PMCID: PMC8004589.

\[4\] Wu T, Liang Z, Zhang Z, Liu C, Zhang L, Gu Y, Peterson KL, Evans SM, Fu XD, Chen J. PRDM16 Is a Compact Myocardium-Enriched Transcription Factor Required to Maintain Compact Myocardial Cardiomyocyte Identity in Left Ventricle. Circulation. 2022 Feb 22;145(8):586-602. doi:
