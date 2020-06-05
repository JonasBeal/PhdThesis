
# Personalization of logical models: method and prognostic validation

\epigraph{"All happy families are alike; each unhappy family is unhappy in its own way."}{Leo Tolstoy (Anna Karenina, 1877)}



  

\initial{N}ow that logical modeling has been introduced in detail, it is possible to come back to the question that structures this part and to refine it. **Is it possible to use routine omics data to obtain logical models that provide qualitative clinical interpretation?**. We thus propose a sequential approach, separating the model construction process from the integration of biological data. A generic logical model is first built, based on the literature knowledge, and the data are then used to specify the model. Indeed, the model as defined from the literature is often generic in the sense that it summarizes the state of knowledge on a probably heterogeneous pathology or population. Assuming that this general regulatory scheme provides a relevant framework for the system, it may then be relevant to use more precise omics data to impose biologically sourced constraints on the model: inactivation of a gene in a patient, activation of a protein or a signalling pathway by overexpression or phosphorylation, etc. This approach, called **PROFILE**, allows the integration of both discrete (mutations) and continuous data (RNA expression levels, proteins) based on the MaBoSS software, and leads to specific models of a cell line or a patient.





\BeginKnitrBlock{summarybox}<div class="summarybox">
#### Publications {-}

This chapter presents the method developed during the thesis to personlize logical models, i.e. generate patient-specific models from a single generic one. The description of the method and analyses on patient data from TCGA have been comprehensively described in @beal2019personalization and briefly summarized in @beal2020personalized. Analyses on cell lines and PDX data are unpublished.</div>\EndKnitrBlock{summarybox}

## From one generic model to data-specific models with PROFILE method

The PROFILE method is summarized in Figure \@ref(fig:PROFILE-abstract) and the different steps are successively described in the following subsections.

\begin{figure}

{\centering \includegraphics[width=0.8\linewidth]{fig/PROFILE-abstract} 

}

\caption[Graphical abstract of PROFILE method to personalize logical models with omics data]{(ref:PROFILE-abstract-caption)}(\#fig:PROFILE-abstract)
\end{figure}
(ref:PROFILE-abstract-caption) **Graphical abstract of PROFILE method to personalize logical models with omics data.** On the one hand (upper left), a generic logical model, in a MaBoSS format is derived from literature knowledge to serve as the starting-point. On the other hand (upper right), omics data are gathered (e.g., genome and transcriptome) as data frames, and processed through functional inference methods (for already discrete genome data) or binarization/normalization (for continuous expression data). The resulting patient profiles are used to perform model personalization, i.e. adapt the generic model with patient data. The merging of the generic model with the patient profiles creates a personalized MaBoSS model per patient. Then, biological or clinical relevance of these patient-specific models can be assessed.

### Gathering knowledge and data

The first steps are therefore to build a logical model adapted to the biological question (Figure \@ref(fig:PROFILE-abstract), upper left) and to collect omics data that will be used to personalize the model (Figure \@ref(fig:PROFILE-abstract), upper right). The construction of the model can be based on literature or data (see previous chapter). In the latter case, the data used to build the model will preferably be distinct from those used to personalize the model.

#### A generic logical model of cancer pathways

In this chapter, which is essentially methodological in nature, we will use a published logical model of cancer pathways to illustrate our PROFILE methodology. It is based on a regulatory network summarizing several key players and pathways involved in cancer mechanisms: RTKs, PI3K/AKT, WNT/$\beta$-catenin, TGF-$\beta$/Smads, Rb, HIF-1, p53 and ATM/ATR [@fumia2013boolean]. The later analyses will be mainly focused on two read-out nodes, *Proliferation* and *Apoptosis*. Based on the model’s logical rules *Proliferation* node is activated by any of the cyclins (CyclinA, CyclinB, CyclinD, and CyclinE) and is, thus, an indicator of cyclin activity as an abstraction and simplification of the cell cycle behavior. *Apoptosis* node is regulated by Caspase 8 and Caspase 9. The generic model of Fumiã and Martins (2013) contains 98 nodes and 254 edges. Further details and visual representation are provided in section \@ref(appendix-fumia) and Figure \@ref(fig:Fumia). Model files are available in MaBoSS format in a dedicated [GitHub repository](https://github.com/sysbio-curie/PROFILE/tree/master/Models/Fumia2013).

#### Cancer data

In order to showcase the method, breast-cancer patient data are gathered from METABRIC studies [@curtis2012genomic; @pereira2016somatic]. 1904 patients have data for both mutations, copy number alterations, RNA expression and clinical status (e.g relapse, survival). This number rises to 2504 patients if we only look at the mutations. Additional analyses were also performed based on the smaller and clinically less complete TCGA breast cancer data [@cancer2012comprehensive]. These are detailed in @beal2019personalization but not included in this thesis.


### Adapting patient profiles to a logical model

Before describing precisely the methodologies for using the data to generate patent-specific models, it is important to understand that these data will need to be transformed. This is the transformation of raw omics data into processed profiles that can be used directly in logical modeling.

#### Functional inference of discrete data

Since the logical formalism is itself discrete, the integration of discrete data is more straightforward. The most natural idea, used in many previous works, is to interpret the effect of these alterations and to encode it discreetly in the model. For instance, a deleterious mutation is integrated into the model by setting the corresponding node to $0$ and ignoring the logical rule associated to it. For activating mutation, the node is set to $1$. The main obstacle is therefore to estimate the functional impact of the alterations in order to translate them as well as possible in the model.  
  

For mutations, based on the variant classification provided by the data, inactivating mutations (nonsense, frame-shift insertions or deletions and mutation in splice or translation start sites) are assumed to correspond to loss of function mutations and therefore the corresponding nodes of the model are forced to $0$. Then, missense mutations are matched with OncoKB database [@chakravarty2017oncokb]: for each mutation present in the database, an effect is assessed (gain or loss of function assigned to $1$ and $0$, respectively) with a corresponding confidence based on expert and literature knowledge. Mutations targeting oncogenes (resp. tumor-suppressor genes), as defined in the 2020+ driver gene prediction method [@tokheim2016evaluating], are assumed to be gain of function mutations (resp. loss of function) and therefore assigned to $1$ (resp. $0$). To rule potential passenger mutations out, each assignment requires that the effect of the mutation has been identified as significant by predictive software based on protein structure such as SIFT [@kumar2009predicting] or PolyPhen [@adzhubei2010method].  
  

For integration of copy number alterations, we use the discrete estimation of gain and loss of copies from GISTIC algorithm processing [@mermel2011gistic]. The loss of both alleles of a gene (labelled -2) can thus be interpreted as a 0. Conversely, a significant gain of copies (labelled +2) denotes a gene that tends to be more highly expressed although the interpretation is more uncertain.

#### Normalization of continuous data

The integration of continuous data, such as RNA expression levels, in logical modeling is more difficult. The stochastic framework of MaBoSS provides however some possibilities. The main continuous mechanistic parameters of MaBoSS are the initial conditions of each node (its initial probability of being activated among the set of simulated stochastic trajectories) and the transition rates associated with the nodes (its probability to have its transition performed in an asynchronous update). In order to facilitate the use of continuous data through one of these two possibilities, we propose to transform them so that the values are continuous between 0 and 1, what we will refer to hereafter as normalized data. It is assumed that these continuous data can be good proxies of activity, 0 corresponding to a very low level of activity of the biological entity and 1 to a very high level. This assumption will have to be explained and justified each time: high level of expression of an RNA or significant phosphorylation of a protein interpreted as continuous markers of an important biological activity for example.  
  

One of the assumptions of our analysis is that the interpretation of continuous data can only be relative and not absolute. It is indeed difficult to define an absolute threshold of RNA level at which a gene will be considered as activated. This may depend on contexts, technologies or even the way in which the data have been processed. On the other hand, it is possible to estimate that a gene is over-expressed for a patient compared to a cohort of interest. In contrast, the effect of a mutation can be estimated more independently. Thus, the continuous data will be normalized for the whole cohort studied, for each gene individually. In order to retain biological information as much as possible, distribution patterns are identified and normalized in different ways.
  

### Personalizing logical models with patient data


## An integration tool for high-dimensional data in cell lines

## An uncertain validation with patient data



