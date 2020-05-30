# Cancer as deregulation of complex machinery

\epigraph{"All happy families are alike; each unhappy family is unhappy in its own way."}{Leo Tolstoy (Anna Karenina, 1877)}



\initial{A}rmed with all these models, whether statistical or mechanistic, we are going to look at cancer, a particularly complex system that fully justifies their use. Since the first chapter recalled how important prior knowledge of the phenomenon under study is for designing models, whatever their nature, this chapter will briefly summarize some of the most important characteristics of this disease before returning to the models themselves in the next chapter. Without aiming for exhaustiveness, and after an epidemiological and statistical description, we will focus on the most useful information for the modeller, i.e. the underlying biological mechanisms and available data.






\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/bath} 

}

\caption[Cancer is an old disease]{(ref:bath-caption)}(\#fig:bath)
\end{figure}
(ref:bath-caption) **Cancer is an old disease.**  Rembrandt, *Bathsheba at Her Bath*, c. 1654, oil on canvas, Louvre Museum, Paris

## What is cancer?

Cancer can be described as a group of diseases characterized by **uncontrolled cell divisions and growth which can spread to surrounding tissues**. Descriptions of this disease, especially when associated with solid tumours, have been found as far back as ancient Egyptian documents, at least 1600 BC and we know from the first century A.D. with Aulus Celsus that it is better to remove the tumors and this as soon as possible [@hajdu2011note]. Progress will accelerate during the Renaissance with the renewed interest in medicine, and anatomy in particular, which will advance the knowledge of tumour pathology and surgery [@hajdu2011note2]. The progress of anatomical knowledge has also left brilliant testimonies in the field of painting, which make the renown of the Renaissance today. The precision of these artists' traits has also allowed some retrospective medical analyses, some of them going so far as to identify the signs of a tumour in some of the subjects of these paintings [@bianucci2018earliest]. Such is the bluish stain on the left breast of the Bathsheba painted by Rembrandt (Figure \@ref(fig:bath)) which has been subject to controversial interpretations, sometimes described as an example of "skin discolouration, distortion of symmetry with axillary fullness and peau d'orange" [@braithwaite1983rembrandt] and sometimes spared by photonic and computationnal analyses [@heijblom2014monte]. The mechanisms of the disease only began to be elucidated with the appearance of the microscope in the 19th century, which revealed its cellular origin [@hajdu2012note]. The classification and description of cancers is then gradually refined and the first non-surgical treatments appear with the discovery of ionising radiation by the Curies [@hajdu2012note2]. The 20th century is then the century of understanding the causes of cancer [@hajdu2013note; @hajdu2013note2]. Some environmental exposures are characterized as asbestos or tobacco. Finally, the biological mechanisms become clearer with the identification of tumour-causing viruses and especially with the discovery of DNA [@watson1953molecular]. The foundations of our current understanding of cancer date back to this period, which marks the beginning of the molecular biology of cancer. It is this branch of biology that contains the bulk of the knowledge that will be used to build our mechanistic models, and it will be later detailed in Section \@ref(molecular-biology).  
  

One of the ways to read this brief history of cancer is to see that theoretical and clinical progress has not followed the same timeframes.The medical and clinical management of cancers initially progressed slowly but surely, and this in the absence of an understanding of the mechanisms of cancer. Conversely, the theoretical progress of the last century has not always led to parallel medical progress, except on certain specific points. The interaction between the two is therefore not always obvious. The **transformation of fundamental knowledge into medical and clinical impact is therefore of particular importance**. This is what is called *translational medicine*, the aim of which is to go from laboratory bench to bedside [@cohrs2015translational]. It is in this perspective that we will analyze the mechanistic models studied in this thesis. Their objective is to integrate biological knowledge, or at least a synthesis this knowledge, in order to transform it into a relevant clinical information.

## Cancer from a distance: epidemiology and main figures {#epidemio}

Before going down to the molecular level, it is important to detail some figures and trends in the epidemiology of cancer today. Following the description in the previous section, cancer is first and foremost defined as a disease. Considered to be a unique disease, it caused 18.1 million new cancer cases and 9.6 million cancer deaths in 2018 according to the Global Cancer Observatory affiliated to World Health Organization [@bray2018global]. However, these aggregated data conceal disparities of various kinds. The first one is geographical. Indeed, mortality figures make cancer one of the leading causes of premature death in most countries of the world but its importance relative to other causes of death is even greater in the more developed countries (Figure \@ref(fig:globocan-map)). All in all, cancer is the first or second cause of premature death in almost 100 countries worldwide [@bray2018global]. These differences call for careful consideration of the impact of population age structures and health-related covariates.

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/globocan-map} 

}

\caption[World map and national rankings of cancer as a cause of premature death]{(ref:globocan-map-caption)}(\#fig:globocan-map)
\end{figure}
(ref:globocan-map-caption) **World map and national rankings of cancer as a cause of premature death.** Classification of cancer as a cause of death before the age of 70, based on data for the year 2015. Original Figure, data and methods from @bray2018global.  
  

A second disparity lies in the different types of cancer. If we classify tumours solely according to their location, i.e. the organ affected first, we already obtain very wide differences. First of all, the incidence varies considerably (Figure \@ref(fig:cancer-tissues)A)). Cancers do not occur randomly anywhere in the body and certain environments or cell types appear to be more favourable [@tomasetti2015variation]. Mortality is also highly variable but is not directly inferred from incidence. Not all types of cancer have the same prognosis (Figure \@ref(fig:cancer-tissues)A and B) and survival rates [@liu2018integrated]. Although breast cancer is much more common than lung cancer, it causes fewer deaths because its prognosis is, on average, much better. The mechanisms at work in the emergence of cancer are therefore not necessarily the same as those that will govern its evolution or its response to treatment. And still on the response to treatment, Figure \@ref(fig:cancer-tissues)B highlights another disparity: not only are the survival prognosis associated with each cancer very different, but the evolution (and generally the improvement) of these prognoses has been very uneven over the last few decades. This means that theoretical and therapeutic advances have not been applied to all types of cancer with the same success. It is one more indication of the **diversity of cancer mechanisms in different tissues and biological contexts**, which make it impossible to find a panacea, and which, on the contrary, encourage us to carefully consider the particularities of each tumour, both to understand them and to treat them. Under a generic name and in spite of common characteristics, the cancers thus appear as extremely heterogeneous. And to understand the sources of this heterogeneity, it is necessary to consider the disease on a smaller scale.

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{02-Cancer_files/figure-latex/cancer-tissues-1} 

}

\caption[Incidence, mortality and survival per cancer types]{(ref:cancer-tissues-caption)}(\#fig:cancer-tissues)
\end{figure}
(ref:cancer-tissues-caption) **Incidence, mortality and survival per cancer types**. (A) World incidence and mortality for the 19 most frequent cancer types in 2018, expressed with age-standardized rates (adjusted age structure based on world population); data retrieved from [Global Cancer Observatory](https://gco.iarc.fr/today/home). (B) Evolution of 5-years relative survival for the same cancer types based on US data from SEER registries in 1975-1977 and 2006-2012; data retrieved from @jemal2017annual.  
  

## Basic molecular biology and cancer {#molecular-biology}

If it is not possible and desirable to summarize here the state of knowledge about the biology of cancer, we are going to give a very partial vision focused on the main elements used in this thesis, thus aiming to make it a self-sufficient document. The details necessary for a finer and more general understanding can be found in dedicated textbooks such as @alberts2007molecular and @weinberg2013biology.

### Central dogma and core principles

Some of the principles that govern biology can be described at the level of one of its simplest element, the cell. Let us consider for the moment a perfectly healthy cell. It must ensure a certain number of functions necessary for its survival and, if necessary, for its division/reproduction. These functions are encoded in its genetic information in the form of DNA, which is stable and shared by the different cells since it is defined at the level of the individual. Most biological functions, however, are not performed by DNA itself which remains in the nucleus of the cell. The DNA is thus transcribed into RNA, another nucleic acid which, in addition to performing some biological functions, becomes the support of the genetic information in the cell. The RNA is then itself translated into new molecules composed of long chains of amino acid residues and called proteins. They are the ones that execute most of the numerous cellular functions: DNA replication, physical structuring of the cell, molecule transport within the cell etc. A rather simplistic but fruitful way to understand this functioning is to consider it as a **progressive transfer of biological information from DNA to proteins**, which has sometimes been summarized as the central dogma of the molecular biology (\@ref(fig:central-dogma)), first stated Francis Crick [@crick1970central].

\begin{figure}

{\centering \includegraphics[width=0.8\linewidth]{fig/central-dogma} 

}

\caption[Central dogma of molecular biology]{(ref:central-dogma-caption)}(\#fig:central-dogma)
\end{figure}
(ref:central-dogma-caption) **Central dogma of molecular biology.** Schematic representation of the information flow within the cell, from DNA to proteins through RNA, more precisely described in this [video](https://www.youtube.com/watch?v=J3HVVi2k2No) (Image credit *Genome Research Limited*).  
  
  
However, many changes would be necessary to clarify this scheme and the uni-directional nature was questioned early on. Above all, a large number of regulations interact with and disrupt this master plan. The genes are not always all transcribed, or at least not at constant intensities, interrupting or varying the chain upstream. This modulation in the transcription of genes can be induced by proteins, called transcription factors. After a gene transcription, its expression can still be regulated at various stages. RNAs can also be degraded more or less rapidly. RNAs can be reshaped in their structure by a process called splicing, which varies the genetic information they carry. Finally, proteins are subject to all kinds of modifications referred to as post-translational, which can change the chemical nature of certain groups or modify the three-dimensional structure of the whole protein. For instance, some proteins perform their function only if a specific amino acid residue is phosphorylated. In addition, these modifications can be transmitted between proteins, further complicating the flow of information. **All these possibilities of regulation play an absolutely essential role in the life of the cell by allowing it to adapt to different contexts and situations**. From the same genetic material, a cell of the eye and a cell of the heart can thus perform different functions. Similarly, the same cell subjected to different stimuli at different times can provide different responses because these molecular stimuli trigger a regulation of its programme. But all these regulatory mechanisms can be corrupted.

### A rogue machinery

With the above knowledge we can now return to the definition of cancer as an uncontrolled division of cells that can lead to the growth of a tumour that eventually spreads to the surrounding tissues. Therefore, this corresponds to normal processes, like cell division and reproduction, that are no longer regulated as they should be and are out of control. Experiments on different model organisms have gradually identified genetic mutations as a major source of these deregulations [@nowell1976clonal, @reddy1982point] until cancer was clearly considered as a **genetic disease** making Renato Dulbecco, Nobel Laureate in Medicine for his work on oncoviruses, say: 

> *If we wish to learn more about cancer, we must now concentrate on the cellular genome.*  
> [@dulbecco1986turning].

However, cancer is not a Mendelian disease for which it would be sufficient to identify the one and only gene responsible for deregulation. Indeed, the cell has many protective mechanisms. For example, if a genetic mutation appears in the DNA, it has a very high chance of being repaired by dedicated mechanisms. And if it is not repaired, other mechanisms will take over to trigger the programmed death of the cell, called apoptosis, before it can proliferate wildly. So a cancer cell is probably a cell that has learned to resist this cell death. Similarly, in order to generate excessive growth, a cell will need to be able to replicate itself many times. However, there are pieces of sequences on chromosomes called telomeres that help to limit the number of times each cell can replicate. A cancer cell will therefore have to manage to bypass this protection. Thus we can schematically define the properties that must be acquired by the cancereous cells in order to truly deviate the machinery. In an influential article, these properties were summarized in six hallmarks (Figure \@ref(fig:hallmarks)) which are: resisting cell death, enabling replicatve immortality, sustaning proliferative signaling, evading growth suppressors, activating invasion and inducing angiogenesis [@hanahan2000hallmarks]. Two new ones were subsequently added in the light of advances in knowledge [@hanahan2011hallmarks]: deregulating cancer energetics and avoiding immne destruction. The acquisition of these capacities generally requires many genetic mutations and is therefore favoured by an underlying genome instability.  
  
\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/hallmarks} 

}

\caption[Hallmarks of cancer]{(ref:hallmarks-caption)}(\#fig:hallmarks)
\end{figure}
(ref:hallmarks-caption) **Hallmarks of cancer.** The different biological capabilities acquired by cancer cells, as described in @hanahan2000hallmarks. Reprinted from @hanahan2011hallmarks.  
  

Each of these characteristics, or hallmarks, constitutes a research program in its own right. And for each one there are genetic alterations. These are tissue-specific or not, specific to a hallmark or common to several of them [@hanahan2000hallmarks]. In any case, **cancer can only result from the combination of different alterations that invalidate several protective mechanisms** at the same time. This is often part of a multi-step process of hallmark acquisition that has been experimentally documented in some specific cases [@hahn1999creation] or more recently inferred from genome-wide data for human patients [@tomasetti2015only]. In summary, it appears that in order to study the functioning of cancer cells it is necessary to look at several mechanisms and to be able to consider them not separately but together, in as many different patients as possible. This ambitious programme has been made possible by a technological revolution.

## The new era of genomics

### From sequencing to multi-omics data

In 2001, the first sequencing of the human genome symbolized the beginning of a new era, that of what will become **high-throughput genomics** [@lander2001initial; @venter2001sequence]. From the end of the 20th century, biological data started to accumulate at an ever-increasing rate [@reuter2015high], feeding and accelerating cancer research in particular [@stratton2009cancer; @meyerson2010advances]. The ability to sequence the human genome as a whole, for an ever-increasing number of individuals, has enabled **less biased and more systematic studies of the causes of cancer** [@lander2011initial]. The number of genes associated with cancer increased drastically and some very important genes such as BRAF of PIK3CA have been identified [@davies2002mutations; @samuels2004high]. Progress also extended to the gene expression data. Gene-expression arrays have made an important contribution by providing access to transcriptomic data (RNA), i.e. what has been transcribed from DNA and is therefore one step further in terms of biological information. This information has made it possible to further explore the differences betwween normal and tumour cells [@perou1999distinctive], or even to refine the classification of cancers, which until now has been done mainly according to the tumour site. Breast cancers are thus divided into subtypes with different combinations of molecular markers that facilitate the understanding of clinical behavior [@perou2000molecular]. One step further, we also note the appearance of prognostic gene signatures such as gene expression patterns correlated with the survival of patients [@van2002gene]. This revolution was then extended to other types of data such as proteins (proteomics), reversible modifications of DNA or DNA-associated proteins (epigenomics), metabolites (metabolomics) and others, each representing a perspective that can complement the others to better understand biological mechanisms, particularly in the case of diseases [@hasin2017multi]. We have thus entered the era of multi-omics data [@vucic2012translating].  
  

### State-of-the art of cancer data

With respect to cancer in particular, this wealth of data is particularly represented by a family of **studies conducted by The Cancer Genome Atlas (TCGA) consortium**, started in 2008 [@cancer2008comprehensive]. Cohorts of several hundred patients are thus sequenced over the years for different types of cancer [@cancer2012comprehensive], resulting today in a total of 11,000 tumors from 33 of the most prevalent forms of cancer [@ding2018perspective]. Figure \@ref(fig:tcga) provides a partial but striking overview of the depth of data available under this program. We can see the frequencies of alterations of certain groups of genes for a list of cancer types, making it possible to visualize the disparities already anticipated in section \@ref(epidemio) based on patient survival. There are indeed important differences between the organs but also between the different subtypes associated with the same organ. And this representation only corresponds to one layer of data, that of genetic alterations. It could be used for transcriptomic, epigenomic or proteomic data, thus giving rise to an incredibly complex photography.

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/tcga} 

}

\caption[Genetic alterations frequencies for cancer types from TCGA data]{(ref:tcga-caption)}(\#fig:tcga)
\end{figure}
(ref:tcga-caption) **Genetic alterations frequencies for cancer types from TCGA data.** Frequencies of alteration per pahway and tumour types as summaried in Pan-cancer analyses from TCGA data. Reprinted from @sanchez2018oncogenic.  
  

However, the diversity of data available for cancer research extends far beyond this, both in terms of technology and type of data. This may be data from model organisms such as mice or tumours of human origin made more suitable for experimentation. In the latter category, it is crucial to mention the **huge amount of data available on cell lines**, extracted from human tumours and transformed to be studied in culture. It is then possible to go beyond descriptive data and vary the experimental conditions in order to study the responses of these cells to perturbations and to enrich our knowledge. This provides an opportunity to know the response to more than 100 drugs of about 700 cell lines [@yang2012genomics]. The richness of these data, coupled with the omic profiling of each cell line, enables to study the determinants of response to treatment with unprecedented scope [@iorio2016landscape]. More recently, but following a similar logic, other types of inhibition screenings have been proposed based on a more specific technique called CRISPR-Cas9 [@behan2019prioritization]. The simplicity of the cell lines in relation to the original tumours makes all these studies possible but sometimes hinders the clinical application of the knowledge acquired. For this reason, other types of biological models have been developed, including patient-derived xenografts (PDX) which is an implant of human tumours in mice to maintain the existence of a certain tumour microenvironment [@hidalgo2014patient], while maintaining drug screening possibilities [@gao2015high]. These two types of data, cell lines and PDX, have been used in this thesis, in addition to TCGA patient data, thus justifying the limitation of this presentation, which could otherwise be extended to other types of biological models. Similarly, other technologies are becoming increasingly important in the generation of cancer data, such as single-cell sequencing [@navin2015first], but will not be used in this work.


## Data and beyond: from genetic to network disease

All that remains to be done now is to make sense of all these data, to organize it, because **cancer understanding does not flow directly from the abundance of data**, and the ability to produce it may have been outpaced by the ability to analyze it [@stadler2014cancer]. A striking example is that of the prognostic signatures mentioned above. The many signatures or lists of genes proposed, even for the same cancer type, share relatively few genes, are difficult to interpret and their efficiency is sometimes poorly reproducible [@domany2014using]. Even more surprisingly, most signatures composed of randomly selected genes were also found to be associated with patient survival [@venet2011most]. One of the main avenues for improving the interpretability of the data is the **integration of the prior knowledge** we have of the phenomena, especially in the case of cancer [@domany2014using].  
  

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/circuit} 

}

\caption[Simplistic representation of cellular circuit and pathways]{(ref:circuit-caption)}(\#fig:circuit)
\end{figure}
(ref:circuit-caption) **Simplistic representation of cellular circuitry.** Normal cellular circuit sand sub-circuits (identified by colours) can be reprogrammed to regulate hallmark capabilities within cancer cells. Reprinted from @hanahan2011hallmarks.

This *a priori* knowledge is in fact already present in Figure \@ref(fig:tcga) since genetic alterations have been grouped in several categories called pathways. A pathway is group of biological entities, and associated chemical reactions, working together to control a specific cell function like apoptosis or cell division. The interest of these groupings may be understood based on the description of hallmarks. Indeed, if the "aim" of a cancer cell is to inactivate each of the protective functions, then it is more relevant to think not by gene but by function. Inactivating only one of the genes associated with the function may be sufficient and it is no longer necessary to inactivate the others. Numerous alterations in a large number of genes in various patients result often in the same key impaired pathways, like alterations of cell cycle or angiogenesis for instance [@jones2008core]. It is therefore possible to improve the stability and interpretability of analyses by moving **from the gene scale to the pathway scale** [@drier2013pathway]. More generally, the integration of biological knowledge often leads to improved performance in various cancer-related prediction tasks, either through the selection of variables or by taking into account the structure of the variables [@bilal2013improving; @ferranti2017value]. Increasingly, the biological variables are not interpreted separately but in relation to each other [@barabasi2004network]. This is reflected in the emergence of more and more resources to summarize and represent signaling pathways and associated networks such as SIGNOR [@perfetto2016signor], OmniPath [@turei2016omnipath] or the Atlas of Cancer Signaling Network [@kuperstein2015atlas]. Like other diseases, cancer then goes **from a genetic disease to a network disease** [@del2010diseases] and one can study how all kinds of genetic alterations affect the wiring of these networks [@pawson2007oncogenic], and modify the cellular functions leading to the previously described cancer hallmarks as depicted schmatically in Figure \@ref(fig:circuit). In short, the richness of the data did not make it less necessary to use prior knowledge in order to make the analyses more interpretable and more robust.  
  

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/pathways} 

}

\caption[Genetic alterations frequencies from TCGA data mapped on a schematic signaling network]{(ref:pathways-caption)}(\#fig:pathways)
\end{figure}
(ref:pathways-caption) **Genetic alterations frequencies from TCGA data mapped on a schematic signaling network.** Frequencies of alteration per pathway and tumour types as summarized in Pan-cancer analyses from TCGA data. Reprinted from @sanchez2018oncogenic.

The final step, to obtain one of the most complete and integrated visions of cancer biology, is then to integrate omics knowledge with knowledge about the structure of pathways to try to understand in detail how their combinations can lead to so many cancers that are both similar and different. An example of such a representation is given by mapping the TCGA data about genetic alterations, presented in Figure \@ref(fig:tcga), on a representation of the different pathways showing not only their internal organization but also their cross-talk [@sanchez2018oncogenic]. This representation is proposed in Figure \@ref(fig:pathways) and is one the most recent and comprehensive view of the kind of tools and data available to the modeller who wants to dissect more deeply the mechanisms involved in cancer.

