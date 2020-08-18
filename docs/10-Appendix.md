# (APPENDIX) Appendix {-}



# About datasets {#appendix-datasets}

## Cell lines {#appendix-cl}

Several analyses in previous chapters are based on data derived from cell lines. Among the different databases, the ones used in the thesis are briefly described below. Please refer to corresponding references for additional details.

### Omics profiles

The omics profiles of cancer cell lines have been downloaded from Cell Model Passports [@van2019cell] containing genotypic and phenotypic information about more than 1,000 cell lines. Among the available data used in this thesis are the exome sequencing, copy number variations and RNA-sequencing.

### Drug screenings {#appendix-GDSC}

Information about response to treatments is retrieved from Genomics of Drug Sensitivity in Cancer Database (GDSC, @yang2012genomics). In order to allow detailed analyses at the level of cancer types, we will restrict ourselves here to tissues represented by at least 20 cell lines and highlighted in dark grey in Figure \@ref(fig:GDSC)A. Most of the 663 cell lines in this subcohort have a complete profile with all omics data (mutations, CNA and expression) and drug responses. However, not all cell lines have necessarily been tested for all drugs.

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{10-Appendix_files/figure-latex/GDSC-1} 

}

\caption[Distribution of cancer types and data types in GDSC-associated dataset]{(ref:GDSC-caption)}(\#fig:GDSC)
\end{figure}
(ref:GDSC-caption) **Distribution of cancer types and data types in GDSC-associated dataset.** (A) Distribution of cell lines per cancer types, highlighting the ones selected in this thesis with more than 20 cell lines. (B) Availibility of data for the 663 selected cell lines in 17 different cancer types.  
  

The cell lines are treated with increasing concentration of drugs and the viability of the cell line relative to untreated control is measured. The dose-response relative viability curve is fitted and then used to compute the half maximal inhibitory concentration ($IC_{50}$) and the area under the dose-response curve (AUC) [@vis2016multilevel], both being represented in Figure \@ref(fig:AUC). Since the $IC_{50}$ values are often extrapolated outside the concentration range actually tested, we will focus on the AUC metric for all validation with drug screening data. AUC is a value between 0 and 1: values close to 1 mean that the relative viability has not been decreased, and lower values correspond to increased sensitivity to inhibitions. In cases where the ranges of concentrations tested for different drugs vary, comparison of their AUC values does not have a simple and straightforward interpretation.

\begin{figure}

{\centering \includegraphics[width=0.5\linewidth]{fig/AUC} 

}

\caption[Drug screening metrics in cell lines]{(ref:AUC-caption)}(\#fig:AUC)
\end{figure}
(ref:AUC-caption) **Drug screening metrics in cell lines.** Based on a tested drug concentration range, $IC_{50}$ and area under the dose-response curve (AUC) can be computed. For a given drug, red AUC corresponds to a more sensitive cell line than blue AUC.

### CRISPR-Cas9 screening {#appendix-CRISPR}

On top the previous drug response characterization, some CRISPR-Cas9 screenings have  been performed on cancer cell lines. Very basically, this involves using single-guide RNAs (sgRNAs) to direct the targeted inhibition of certain genes. Conceptually, screening is not very different from drug screening since it allows the sensitivity of cell lines to the inhibition of certain targets to be studied. However, this technology makes it possible to target many more different genes since it is based on RNA guide synthesis and not on the existence of drugs with an affinity for the target of interest. Schematically, sreening is therefore broader (thousands of genes), less biased (any gene can be targeted *a priori*) and more precise (much lower off-target effect).  
  

Among the various databases available, the ones used in this thesis have been downloaded from Cell Model Passports and come from Sanger Institute [@behan2019prioritization] and Broad Institute [@meyers2017computational]. Both databases present CRISPR inhibition results for thousands of genes for a few hundred cell lines among those presented in the previous section. The Sanger dataset for instance includes 324 cell lines, and 238 in common with the subcohort previously described in the previous section and in Figure \@ref(fig:GDSC).  
  

Among the different metrics, the examples presented in this thesis will focus on scaled Bayesian factors to assess the effect of CRISPR targeting of genes. These scores are computed based on the fold change distribution of sgRNA [@hart2016bagel]. The highest values indicate that the targeted gene is essential to the cell fitness.

## Patient-derived xenografts {#appendix-PDX}

Another type of data exists, halfway between cell lines and patients, and that is patient-derived xenografts (PDX). Each patient tumour is divided into pieces later implanted in several immunodeficient cloned mice treated with different drugs, thus providing access to sensitivities to several different drugs for each tumour. 

### Overview of PDX data from @gao2015high

The PDX dataset used in this thesis is the one published by @gao2015high. The original dataset contains 281 different tumours of origin (sometimes called PDX models, in the sense of a biological model) and 63 tested drugs, not all drugs having been tested for all tumours and some drugs have been tested with tissue-specific patterns (Figure \@ref(fig:PDX-appendix)). 192 of these tumours have also been characterized for their mutations, copy-number alterations and mRNA. More detailed analyses of this dataset are available in the dedicated [Github repository](https://github.com/JonasBeal/Causal_Precision_Medicine), in the file *Analysis_PDX.Rmd* and its corresponding HTML report.

\begin{figure}

{\centering \includegraphics[width=0.95\linewidth]{10-Appendix_files/figure-latex/PDX-appendix-1} 

}

\caption[Comprehensive overview of tumours and drugs screened in PDX dataset from @gao2015high]{(ref:PDX-appendix-caption)}(\#fig:PDX-appendix)
\end{figure}
(ref:PDX-appendix-caption) **Comprehensive overview of tumours and drugs screened in PDX dataset from @gao2015high.**

### Drug response metrics

#### A continuous outcome

The first drug response metric used in this article is called *Best Average Response*. For each combination tumour/drug, the response is determined by comparing tumor volume change at time $t$, $V_t$ to tumor volume at time $t_0$, $V_{t_0}$. Several scores are computed:

$$\text{Tumour Volume Change (\%)} = \Delta Vol_t = 100\% \times \dfrac{V_t-V_{t_0}}{V_t}$$

$$\text{Best Response} = min(\Delta Vol_t), t>10d$$

$$\text{Average Response}_t = mean(\Delta Vol_i, 0 \leq i\leq t)$$

$$\text{Best Average Response} = min(\text{Average Response}_t), t>10d$$

We will mainly focus on *Best Average Response*. This metric "captures a combination of speed, strength and durability of response into a single value" [@gao2015high]. Qualitatively, lower values correspond to more efficient drugs.

#### A binary outcome

Thresholds of *Best Response* and *Best Average Response* are also defined, inspired by RECIST criteria [@therasse2000new], in order to classify response to treatment into 4 categories: Complete Response (CR), Partial Response (PR, Stable Disease (SD) and Progressive Disease (PD). We designed a binary response status by combining the response categories (CR, PR and SD) into a single "responder"" category (1), opposed to the "non-responders" progressive diseases (0).

## Patients {#appendix-datasets-patients}

### METABRIC

METABRIC dataset is large breast cancer dataset with more than 2'000 patients [@pereira2016somatic]. Mutations, CNA, expression (transcriptomics micro-array) and clinical data are available for a majority of patients (Figure \@ref(fig:METABRIC)A), with 1'904 patients for whom all the data is available. One of the  particular features of these data is to propose a very long clinical follow-up, over more than 10 years (Figure \@ref(fig:METABRIC)B).

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{10-Appendix_files/figure-latex/METABRIC-1} 

}

\caption[Available omics and survival in METABRIC Breast Cancer dataset]{(ref:METABRIC-caption)}(\#fig:METABRIC)
\end{figure}
(ref:METABRIC-caption) **Available omics and survival in METABRIC Breast Cancer dataset**. (A) Number of patients for each omics type and their combinations, depicted as a Venn diagram. (B) Overall survival probability for all patients with clinical follow-up, stratified per breast cancer PAM50 subtype; administrative censoring at 180 months.

### TCGA: Breast cancer

Another reference database for breast cancer is the one from the TCGA consortium [@cancer2012comprehensive]. The cohort is smaller than METABRIC and its clinical follow-up is more limited. In contrast, the omics data are more comprehensive and include RNA sequencing and relative quantification of proteins with RPPA technology (Figure \@ref(fig:TCGA-bp)A). 

\begin{figure}

{\centering \includegraphics[width=0.7\linewidth]{10-Appendix_files/figure-latex/TCGA-bp-1} 

}

\caption[Available omics for TCGA Breast and Prostate cancer]{(ref:TCGA-bp-caption)}(\#fig:TCGA-bp)
\end{figure}
(ref:TCGA-bp-caption) **Available omics for TCGA Breast and Prostate cancer**. (A) Number of patients for each omics type and their combinations, depicted as a Venn diagram, in TCGA BRCA (Breast Invasive Carcinoma) study. (B) Same for the TCGA PRAD (Prostate Adenocarcinoma) study.

### TCGA: Prostate cancer {#appendix-prostate}

Similarly, for prostate cancer, reference can be made to data from the TCGA study [@abeshouse2015molecular], which has the same type of data but for a smaller number of patients than the breast cancer (Figure \@ref(fig:TCGA-bp)B).

# About logical models

Several logical models of cancer are used in this thesis and some additional descriptive elements about them are given below.

## Generic logical model of cancer pathways {#appendix-fumia}

For this thesis, a published Boolean model from [@fumia2013boolean] has first been used to illustrate our PROFILE methodology. This regulatory network summarizes several key players and pathways involved in cancer mechanisms such as RTKs, PI3K/AKT, WNT/$\beta$-catenin, TGF-$\beta$/Smads, Rb, HIF-1, p53 and ATM/ATR. An input node *Acidosis* has been added, along with an output node *Proliferation* used as a readout for the activity of any of the cyclins (*CyclinA*, *CyclinB*, *CyclinD* and *CyclinE*). This slightly extended model contains 98 nodes and 254 edges and its inputs are *Acidosis*, *Nutrients*, *Growth Factors* (GFs), *Hypoxia*, *TNFalpha*, *ROS*, *PTEN*, *p14ARF*, *GLI*, *FOXO*, *APC* and *MAX*. Its outputs are *Proliferation*, *Apoptosis*, *DNA_repair*, *DNA_damage*, *VEGF*, *Lactic_acid*, *GSH*, *GLUT1* and *COX412*.

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/Fumia2013} 

}

\caption[GINsim representation of the logical model described in Fumia et al. (2013)]{(ref:Fumia-caption)}(\#fig:Fumia)
\end{figure}
(ref:Fumia-caption) **GINsim representation of the logical model described in @fumia2013boolean.**

## Extended logical model of cancer pathways {#appendix-verlingue}

Another logical model of similar size and scope was also used, primarily for the study of treatment responses. This model was built by Loïc Verlingue, a medical oncologist and member of the laboratory and preliminary versions of the model are described in @verlingue2016comprehensive and @verlingue2016silico. One of the interests of this model is that it has been designed with a more clinical perspective, notably centred on the response to MTOR inhibitors. In addition, it presents more biological read-outs used for interpretation, and we will use mainly *Proliferation* (also called *G1_S* in the model files to designate the associated stage of the cell cycle), *Apoptosis* and *Quiescence* in particular. In addition, being able to discuss and collaborate directly with the model autor has helped to avoid potential errors in use.

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/Verlingue} 

}

\caption[GINsim representation of the "Verlingue" logical model described in Verlingue et al.]{(ref:Verlingue-caption)}(\#fig:Verlingue)
\end{figure}
(ref:Verlingue-caption) **GINsim representation of the 'Verlingue' logical model described in @verlingue2016silico.**

## Logical model of BRAF pathways in melanoma and colorectal cancer {#appendix-pantolini}

Here are some details about the regulations represented in Figure \@ref(fig:BRAF-model). The MAPK pathway encompasses three families of protein kinases: RAF, MEK, ERK. If RAF is separated into two isoforms, CRAF and BRAF, the other two families MEK and ERK are represented by a single node. When BRAF is inhibited, ERK can still be activated through CRAF, and BRAF binds to and phosphorylates MEK1 and MEK2 more efficiently than CRAF [@wellbrock2004raf], especially in his V600E/K mutated form. When PI3K/AKT pathway is activated, through the presence of the HGF (Hepatocyte Growth Factors), EGF (Epidermal Growth Factors) and FGF (Fibroblast Growth Factors) ligands, it leads to a proliferative phenotype. The activation of this pathway results in the activation of PDPK1 and mTOR, both able to phosphorylate p70 (RPS6KB1) which then promotes cell proliferation and growth [@uniprot2019uniprot]. There has been some evidence of negative regulations of these two pathways carried out by ERK itself [@lake2016negative]: phosphorylated ERK is able to prevent the SOS-GRB2 complex formation through the activation of SPRY [@edwin2009intermolecular], inhibit the EGF-dependent GAB1/PI3K association [@lehr2004identification] and down-regulate EGFR signal through phosphorylation [@lake2016negative]. The model also accounts for a negative regulation of proliferation through a pathway involving p53 activation in response to DNA damage (represented by ATM); p53 hinders proliferation through the activation of both PTEN, a PI3K inhibitor, and p21 (CDKN1A) responsible for cell cycle arrest.  
  

We hypothesize that a single network is able to discriminate between melanoma and CRC cells. These differences may come from different sources. One of them is linked to the negative feedback loop from ERK to EGFR. As mentioned previously, this feedback leads to one important difference in response to treatment between melanoma and CRC: $BRAF^{(V600E)}$ inhibition causes a rapid feedback activation of EGFR, which supports continued proliferation. This feedback is observed only in colorectal since melanoma cells express low levels of EGFR and are therefore not subject to this reactivation [@prahallad2012unresponsiveness]. Moreover, phosphorylation of SOX10 by ERK inhibits its transcription activity towards multiple target genes by interfering with the sumoylation of SOX10 at K55, which is essential for its transcriptional activity [@han2018erk]. The absence of ERK releases the activity of SOX10, which is necessary and sufficient for FOXD3 induction. FOXD3 is then able to directly activate the expression of ERBB3 at the transcriptional level, enhancing the responsiveness of melanoma cells to NRG1 (the ligand for ERBB3), and thus leading to the reactivation of both MAPK and PI3K/AKT pathways [@han2018erk]. Furthermore, it has been shown that in colorectal cells, FOXD3 inhibits EGFR signal *in vitro* [@li2017foxd3]. Interestingly, SOX10 is highly expressed in melanoma cell lines when compared to other cancer cells. In the model, we define SOX10 as an input because of the lack of information about the regulatory mechanisms controlling its activity. The different expression levels of SOX10 have been reported to play an important role in melanoma (high expression) and colorectal (low expression) cell lines. 
  
Besides a list of formalized biological assertions, retrieved from literature, has been used during the model building to ensure the consitency of the model with some qualitative behaviours. These assertions, listed below, are all verified when the logical model is simulated (details are available on the corresponding [GitHub repository](https://github.com/sysbio-curie/MaBoSS_test)):

* BRAF inhibition causes a feedback activation of EGFR in colorectal cancer and not in melanoma [@prahallad2012unresponsiveness]
* MEK inhibition stops ERK signal but activates the PI3K/Akt pathway and increases the activity of ERBB3 [@gopal2010basal; @lake2016negative]
* HGF signal leads to the reactivation of the MAPK and PI3K/AKT pathways, and resistance to BRAF inhibition [@wroblewski2013bh3]
* BRAF inhibition in melanoma activates the SOX10/FOXD3/ERBB3 axis, which mediates resistance through the activation of the PI3K/AKT pathway [@han2018erk]
* Overexpression/mutation of CRAF results in constitutive activation of ERK and MEK also in the presence of a BRAF inhibitor [@manzano2016resistant; johannessen2010cot]
* Early resistance to BRAF inhibition may be observed in case of PTEN loss, or mutations in PI3K or AKT [@manzano2016resistant]
* Experiments in melanoma cell lines support combined treatment with BRAF/MEK + PI3K/AKT inhibitors to overcome resistance [@manzano2016resistant]
* BRAF inhibition (Vemurafenib) leads to the induction of PI3K/AKT pathway and inhibition of EGFR did not block this induction [@corcoran2012egfr]
* Induction of PI3K/AKT pathway signaling has been associated with decreased sensitivity to MAPK inhibition [@corcoran2012egfr]


## Logical model of prostate cancer {#appendix-montagud}

In the context of the European project [PRECISE](https://precise-project.eu/) (Personalized Engine for Cancer Integrative Study and Evaluation), focused on the integrative study of prostate cancer, an adapted logical model has been built. This prostate cancer model is initially based on the generic structure of the Fumia model presented in section \@ref(appendix-fumia), which has been considerably enriched and extended with genes and mechanisms specific to prostate cancer such as ERG, SPOP or AR. The model contains 133 nodes and 449 edges (Figure \@ref(fig:Montagud)) and includes pathways like androgen receptor and growth factor signalling, several signaling pathways (Wnt, NFkB, PI3K/AKT, MAPK, mTOR, SHH), cell cycle, epithelial-mesenchymal transition (EMT), Apoptosis, DNA damage, etc. The model has 9 inputs (EGF, FGF, TGF beta, Nutrients, Hypoxia, Acidosis, Androgen, TNF alpha and Carcinogen presence) and 6 outputs (*Proliferation*, *Apoptosis*, *Invasion*, *Migration*, (bone) *Metastasis* and *DNA repair*).


\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/Montagud} 

}

\caption[GINsim representation of the "Montagud" logical model of prostate cancer]{(ref:Montagud-caption)}(\#fig:Montagud)
\end{figure}
(ref:Montagud-caption) **GINsim representation of the 'Montagud' logical model of prostate cancer.**

# About statistics

## $R^2$ and beyond

### Decomposition of $R^2$ {#appendix-decomp}

The decomposition of $R^2$ according to the method of @lindeman1980introduction is detailed below. The presentation is taken directly from @gromping2006relative.  
  
A linear model is written $y_i=\beta_0+\beta_1x_{i1}+...+\beta_px_{ip}+e_i$ and the corresponding $R^2$ is:

$$R^2=\dfrac{\sum_{i=1}^{n} (\hat{y_i}-\bar{y_i})^2}{\sum_{i=1}^{n}  (y_i-\bar{y_i})^2}$$
Additionally, we define $R^2(S)$ for a model with regressors in set S. The additional $R^2$ when adding the regressors in set $M$ to a model with the regressors in set $S$ is given as:

$$seqR^2(M|S)=R^2(M\cup S)-R^2(S)$$

The order of the regressors in any model is a permutation of the available regressors $x_1, ..., x_p$ and is denoted by the tuple of indices $r = (r_1, ..., r_p)$. Let $S_k(r)$ denote the set of regressors entered into the model before regressor $x_k$ in the order $r$. Then the portion of $R^2$ allocated
to regressor $x_k$ in the order $r$ can be written as

$$seqR^2(\{x_k\}|S_k(r))=R^2(\{x_k\}\cup S_k(r))-R^2(S_k(r))$$

All in all, the $R^2$ allocated to $x_k$ after decomposition is:

$$R^2_{decomp}(x_k)=\dfrac{1}{p!}\sum_{r\text{ permutations}}seqR^2(\{x_k\}|r)$$

### $R^2$ for survival data {#appendix-r2surv}

Among the different $R^2$ analogues that have been proposed to measure the variation explained by survival models, the one described by @royston2004new, called $R^2_D$ appears to be one of the most relevant with respect to the following criteria: independance from sensoring, interpretability and robustness to model misspecification [@choodari2012simulation]. 


The description is given below in the context of a Cox proportional hazards (PH) survival model with $n$ individuals with $T_i$ and $C_i$ corresponding respectively to potential death (or relapse) and censoring times, with $i=1,2,...,n$. In this time-to-event setting, $X_i=min(T_i,C_i)$ is the time variables and $\delta_i=I(T_i \leq C_i)$ the status variable, $I$ being the indicator function. The Cox PH model then expresses the hazard function as follows:

$$h(t|X)=h_0(t).\text{exp}(\beta'X)$$,

with $t$ the time to a death event, $X$ the covariate vector and $beta$ the parameter vector. The adapted $R^2$ called $R^2_D$ is given by [@royston2006explained]:

$$R^2=\dfrac{D^2/\kappa^2}{D^2/\kappa^2 + \sigma^2_{\epsilon}}$$,

with the following component:

* $D$ quantifies the separation of survival curves. It is computed by ordering the estimated prognostic index, $\beta'X$, calculating the expected standard normal order statistics corresponding to these values, dividing the latter by a factor $\kappa$, and performing an auxiliary regression on the scaled scores: the resulting regression coefficient is $D$.
* $\kappa=\sqrt{8/\pi}\approx 1.60$ [@royston2004new]
* $\sigma^2_{\epsilon}$ is the variance of the error term, $\sigma^2_{\epsilon}=\pi^2/6$ for Cox PH models

For a better understanding of this formula, it is interesting to note that in a linear regression model $Y\sim N(\beta'X, \sigma^2)$, it is also possible to write $R^2$ equivalently as follows:

$$R^2=\dfrac{\text{Var}(\beta'X)}{\text{Var}(\beta'X)+\sigma^2}$$

This formula underlines the analogy with $R^2_D$, with $D^2/\kappa^2$ being interpreted as an estimate of the variance of the prognostic index $\beta'X$ for the Cox PH model. 

## Causal inference with multiple versions of treatment

This section gathers the demonstrations of the equations present in chapter \@ref(chapter-precision) when they are not present in this chapter and additional details about other estimators based on IPW and TMLE.

### Overall treatment effect with multiple versions of treatment (equation \@ref(eq:overall-treatment-effect)) {#appendix-overall-treatment-effect}

Here is the formal proof for equation \@ref(eq:overall-treatment-effect), mostly derived from the proof of Proposition 3 in [@vanderweele2013causal].

\begingroup
\footnotesize
\begin{equation*}
\begin{aligned}
  E[ & Y(a, K^a(a))] = E[Y(a)] &&K^a \text{ actually received}\\
                  & = \sum_{c,w} E[Y(a)|c,w] \times P[c,w]&& \\
                  & = \sum_{c,w} E[Y(a)|a,c,w] \times P[c,w]
                  && Y(a) \perp \!\!\! \perp A | (C,W)\\
                  & = \sum_{c,w} E[Y(a, K^a(a))|a,c,w] \times P[c,w]&& \\
                  & = \sum_{c,w,k^a} E[Y(a, k^a)|a,K^a(a)=k^a,c,w]\times P[K^a(a)=k^a|a,c,w] \times P[c,w] &&\\
                  & = \sum_{c,w,k^a} E[Y(a, k^a)|a,K^a=k^a,c,w]\times P[K^a=k^a|a,c,w] \times P[c,w]
                  &&\text{consistency K} \\
                  & = \sum_{c,w,k^a} E[Y|a,K^a=k^a,c,w]\times P[K^a=k^a|a,c,w] \times P[c,w]
                  &&\text{consistency Y} \\
                  & = \sum_{c,w} E[Y|a,c,w]\times P[c,w]
\end{aligned}
\end{equation*}
\endgroup

Then, the overall treatment effect can be defined and computed by:

$$E[Y(a, K^a(a))] - E[Y(a^*, K^{a^*}(a^*))]$$

### Treatment effect with predefined distributions of versions of treatment (equation \@ref(eq:distrib-treatment-effect)) {#appendix-distrib-treatment-effect}

Here is the formal proof for equation \@ref(eq:distrib-treatment-effect), partially derived from the proof of Proposition 5 in [@vanderweele2013causal].

\begingroup
\footnotesize
\begin{equation*}
\begin{aligned}
  E[ & Y(a, G^a)] = \sum_{c} E[Y(a, G^a)|C=c] \times P[c]\\
             & = \sum_{c, k^a} E[Y(a, k^a)|G^a=k^a, C=c] \times P[G^a=k^a|C=c] \times P[c]\\
             & = \sum_{c, k^a} E[Y(a, k^a)| C=c] \times g^{k^a,c} \times P[c]
             &&\text{since } P[G^a=k^a] = g^{k^a,c}\\
             & = \sum_{c, k^a} E[Y(a, k^a)| A=a, K^a=k^a, C=c] \times g^{k^a,c} \times P[c] 
             &&\text{with } Y(a,k^a) \perp \!\!\! \perp \{A,K\} | C\\
             & = \sum_{c, k^a} E[Y| A=a, K^a=k^a, C=c] \times P[c]
             &&\text{by consistency for Y}
\end{aligned}
\end{equation*}
\endgroup

### Inverse probability of treatment weighted (IPW) estimators for precision medicine {#appendix-IPW}

An extension of IPW methods described in section \@ref(IPW-classic) to multi-valued treatments (only treatment $K$ with different modalities and no $A$) has already been studied and the different formulas and estimators adapted accordingly [@imbens2000role; @feng2012generalized], defining in particular a generalized propensity score:

$$f(k|c)=P[K=k|C=c]=E[I(k)|C=c]$$

\begin{equation*}
\text{with }
I(k) = \left\{
\begin{array}{ll}
1 & \quad \text{if } K = k \\
0 & \quad \text{otherwise}
\end{array}
\right.
\end{equation*}

and a subsequent estimator:

$$E[Y(k)]=\dfrac{\hat{E}[I(K=k)W^{K}Y]}{\hat{E}[I(K=k)W^K]} \text{ with } W^K=\dfrac{1}{f[K|C]}$$



In our precision medicine settings, to be consistent with the previously defined causal diagram (Figure \@ref(fig:DAG-multiple)), we have both $A$, binary status depending on the class of drugs, and $K$, the multinomial variable for versions of treatments, *i.e.*, the precise drug. Therefore we need to define a slightly different propensity score with joint probabilities:

\begin{equation*}
\begin{aligned}
f(a,k|c) & =P[A=a,K=k|C=c]\\
         & =P[K=k|A=a, C=c].P[A=a|C=c]\\
         & =E[I(a,k)|C=c] 
\end{aligned}
\end{equation*}

\begin{equation*}
\text{with }
I(a,k) = \left\{
\begin{array}{ll}
1 & \quad \text{if } A = a, K = k \\
0 & \quad \text{otherwise}
\end{array}
\right.
\end{equation*}

From this we can deduce the estimator:

$$E[Y(a, k)]=\dfrac{\hat{E}[I(A=a,K=k)W^{A,K}Y]}{\hat{E}[I(A=a,K=k)W^{A,K}]} \text{ with } W^{A,K}=\dfrac{1}{f[A,K|C]}$$

In all the examples presented in this study and implemented in the code, $\mathcal{K}^{0} \cap \mathcal{K}^{1} = \emptyset$, it is therefore possible to simplify the joint probabilities since the knowledge of K automatically results in the knowledge of A allowing $P[A=a, K=k|C=c]=P[K=k|C=c]$. The above formulas with the attached probabilities are still necessary in the general case and allow for the derivation of causal effects $\text{CE}_1$, $\text{CE}_2$ and $\text{CE}_3$ previously described.

### TMLE {#appendix-TMLE}

Targeted maximum likelihood estimation is framework based on a doubly robust maximum-likelihood–based approach that includes a "targeting" step that optimizes the bias-variance trade-off for a defined target parameter. In particular, this method is perfectly compatible with the use of machine learning algorithms for outcome or treatment models. A detailed description of the method and its implementations can be found in @van2011targeted.  
  

The implementation proposed in this article is very similar to the one proposed in a recent tutorial concerning the application to binary processing [@luque2018targeted]. The specific characteristics of the problem of precision medicine studied here lead to modify this approach. In particular, the outcome and treatment models used in the first steps are modified in the same way as the one explained for the standardized estimators (outcome model) and for the IPW estimators (treatment model). The step of updating the estimates is done on a model similar to @luque2018targeted.  
  

The algorithm used for the models internal to the TMLE are, as much as possible, the same as those used for the standardised and IPW estimators:

* For simulated data: generalized linear models in all cases except multinomial classification performed through the function \emph{multinom} in \emph{nnet} package.
* For PDX data: random forests for all models. Use of SuperLearner [@van2007super] is made possible by simple modifications to the code but significantly slows down its execution. 
