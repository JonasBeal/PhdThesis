# (APPENDIX) Appendix {-}



# About datasets {#appendix-datasets}

## Cell lines {#appendix-cl}

Several analyses in previous chapters are based on data derived from cell lines. Among the different databases, the ones used in the thesis are briefly described below. Please refer to corresponding references for additional details.

### Omics profiles

The omics profiles of cancer cell lines have been downloaded from Cell Model Passports [@van2019cell] containing genotypic and phenotypic information about more than 1000 cell lines. Among the available data used in this thesis are the exome sequencing, copy number variations and RNA-sequencing.

### Drug screenings

Information about response to treatments is retrieved from Genomics of Drug Sensitivity in Cancer Database (GDSC, @yang2012genomics). In order to allow detailed analyses at the level of cancer types, we will restrict ourselves here to tissues represented by at least 20 cell lines and highlighted in dark grey in Figure \@ref(fig:GDSC)A. Most of the 663 cell lines in this subcohort have a complete profile with all omics data (mutations, CNA and expression) and drug responses. However, not all cell lines have necessarily been tested for all drugs.

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{10-Appendix_files/figure-latex/GDSC-1} 

}

\caption[Distribution of cancer types and data types in GDSC-associated dataset]{(ref:GDSC-caption)}(\#fig:GDSC)
\end{figure}
(ref:GDSC-caption) **Distribution of cancer types and data types in GDSC-associated dataset.** (A) Distribution of cell lines per cancer types, highlighting the ones selected in this thesis with more than 20 cell lines. (B) Availibility of data for the 663 selected cell lines in 17 different cancer types.  
  

The cell lines are treated with increasing concentration of drugs and the viability of the cell line relative to untreated control is measured. The dose-response relative viability curve is fitted and then used to compute the half maximal inhibitory concentration ($IC_{50}$) and the area under the dose-response curve (AUC) [@vis2016multilevel], both being represented in Figure. Since the $IC_{50}$ values are often extrapolated outside the concentration range actually tested, we will focus on the AUC metric for all validation with drug screening data. AUC is a value between 0 and 1: values close to 1 mean that the relative viability has not been decreased, and lower values correspond to increased sensitivity to inhibitions. In cases where the ranges of concentrations tested for different drugs vary, comparison of their AUC values does not have a simple and straightforward interpretation.

\begin{figure}

{\centering \includegraphics[width=0.5\linewidth]{fig/AUC} 

}

\caption[Drug screening metrics in cell lines]{(ref:AUC-caption)}(\#fig:AUC)
\end{figure}
(ref:AUC-caption) **Drug screening metrics in cell lines.** Based on a tested drug concentration range, $IC_{50}$ and area under the dose-response curve (AUC) can be computed. For a given drug, red AUC corresponds to a more sensitive cell line than blue AUC.

### CRISPR-Cas9 screening

On top the previous drug response characterization, some CRISPR-Cas9 screenings have  been performed on cancer cell lines. Very basically, this involves using single-guide RNAs (sgRNAs) to direct the targeted inhibition of certain genes. Conceptually, screening is not very different from drug screening since it allows the sensitivity of cell lines to the inhibition of certain targets to be studied. However, this technology makes it possible to target many more different genes since it is based on RNA guide synthesis and not on the existence of drugs with an affinity for the target of interest. Schematically, sreening is therefore broader (thousands of genes), less biased (any gene can be targeted a priori) and more precise (much lower off-target effect).  
  

Among the various databases available, the ones used in this thesis have been downloaded from Cell Model Passports and come from Sanger Institute [@behan2019prioritization] and Broad Institute [@meyers2017computational]. Both databases present CRISPR inhibition results for thousands of genes for a few hundred cell lines among those presented in the previous section. The Sanger dataset for instance includes 324 cell lines, and 238 in common with the subcohort previously described in the previous section and in Figure \@ref(fig:GDSC).  
  

Among the different metrics, the examples presented in this thesis will focus on scaled Bayesian factors to assess the effect of CRISPR targeting of genes. These scores are computed based on the fold change distribution of sgRNA [@hart2016bagel]. The highest values indicate that the targeted gene is essential to the cell fitness.

## Patient-derived xenografts

Distributions and some figures

## Patients {#appendix-datasets-patients}

### METABRIC

METABRIC dataset is large breast cancer dataset with around 2000 patients. Mutations, CNA, expression (transcriptomics micro-array) and clinical data are available for a majority of patients (Figure \@ref(fig:METABRIC)A), with 1904 patients for whom all the data is available. One of the  particular features of these data is to propose a very long clinical follow-up, over more than 10 years (Figure \@ref(fig:METABRIC)B).

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{10-Appendix_files/figure-latex/METABRIC-1} 

}

\caption[Available omics and survival in METABRIC Breast Cancer dataset]{(ref:METABRIC-caption)}(\#fig:METABRIC)
\end{figure}
(ref:METABRIC-caption) **Available omics and survival in METABRIC Breast Cancer dataset**. (A) Number of patients for each omics type and their combinations, depicted as a Venn diagram. (B) Overall survival probability for all patients with clinical follow-up, stratified per breast cancer PAM50 subtype; administrative censoring at 180 months.

### TCGA: Breast cancer

Another reference database for breast cancer is the one from the TCGA consortium [@cancer2012comprehensive]. The cohort is smaller than METABRIC and its clinical follow-up is more limited. In contrast, the omics data are more comprehensive and include RNA sequencing and relative quantification ofsproteins with RPPA technology (Figure \@ref(fig:TCGA-bp)A). 

\begin{figure}

{\centering \includegraphics[width=0.7\linewidth]{10-Appendix_files/figure-latex/TCGA-bp-1} 

}

\caption[Available omics and survival in METABRIC Breast Cancer dataset]{(ref:TCGA-bp-caption)}(\#fig:TCGA-bp)
\end{figure}
(ref:TCGA-bp-caption) **Available omics for TCGA Breast and Prostate cancer**. (A) Number of patients for each omics type and their combinations, depicted as a Venn diagram, in TCGA BRCA (Breast Invasive Carcinoma) study. (B) Same for the TCGA PRAD (Prostate Adenocarcinoma) study.

### TCGA: Prostate cancer

Similarly, for prostate cancer, reference can be made to data from the TCGA study [@abeshouse2015molecular], which has the same type of data but for a smaller number of patients than the breast cancer (Figure \@ref(fig:TCGA-bp)B).

# About logical models

Several logical models of cancer are used in this thesis and some additional descriptive elements about them are given below.

## Generic logical model of cancer pathways {#appendix-fumia}

For this thesis, a published Boolean model from [@fumia2013boolean] has been used to illustrate our PROFILE methodology. This regulatory network summarizes several key players and pathways involved in cancer mechanisms such as RTKs, PI3K/AKT, WNT/$\beta$-catenin, TGF-$\beta$/Smads, Rb, HIF-1, p53 and ATM/ATR. An input node *Acidosis* has been added, along with an output node *Proliferation* used as a readout for the activity of any of the cyclins (*CyclinA*, *CyclinB*, *CyclinD* and *CyclinE*). This slightly extended model contains 98 nodes and 254 edges and its inputs are *Acidosis*, *Nutrients*, *Growth Factors* (GFs), *Hypoxia*, *TNFalpha*, *ROS*, *PTEN*, *p14ARF*, *GLI*, *FOXO*, *APC* and *MAX*. Its outputs are *Proliferation*, *Apoptosis*, *DNA_repair*, *DNA_damage*, *VEGF*, *Lactic_acid*, *GSH*, *GLUT1* and *COX412*.

\begin{figure}

{\centering \includegraphics[width=0.8\linewidth]{fig/Fumia2013} 

}

\caption[Graphical abstract of PROFILE method to personalize logical models with omics data]{(ref:Fumia-caption)}(\#fig:Fumia)
\end{figure}
(ref:Fumia-caption) **GINSIM representation of the logical model described in @fumia2013boolean.**

## Logical model of BRAF pathways in melanoma and colorectal cancer {#appendix-pantolini}

## Logical model of prostate cancer {#appendix-montagud}

# About causality

## Theoretical framework


