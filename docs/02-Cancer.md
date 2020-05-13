# Cancer as deregulation of complex machinery

\epigraph{"All happy families are alike; each unhappy family is unhappy in its own way."}{Leo Tolstoy (Anna Karenina, 1877)}



\initial{A}rmed with all these models, whether statistical or mechanistic, we are going to look at a particularly complex system that fully justifies their use: cancer. Since the first chapter recalled how important prior knowledge of the phenomenon under study is for designing models, whatever their nature, this chapter will briefly summarize some of the most important characteristics of this disease before returning to the models themselves in the next chapter. Without aiming for exhaustiveness, and after an epidemiological and statistical description, we will focus on the most useful information for the modeller, i.e. the underlying biological mechanisms and available data.






\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/bath} 

}

\caption[Cancer is an old disease]{(ref:bath-caption)}(\#fig:bath)
\end{figure}
(ref:bath-caption) **Cancer is an old disease**  Rembrandt, *Bathsheba at Her Bath*, c. 1654, oil on canvas, Louvre Museum, Paris

## What is cancer?

Cancer can be described as a group of diseases characterized by uncontrolled cell divisions and growth which can spread to surrounding tissues. Descriptions of this disease, and essentially associated solid tumours, have been found as far back as ancient Egyptian documents, at least 1600 BC and we know from the first century A.D. with Aulus Celsus that it is better to remove the tumors and this as soon as possible [@hajdu2011note]. Progress will accelerate during the Renaissance with the renewed interest in medicine, and anatomy in particular, which will advance the knowledge of tumour pathology and surgery [@hajdu2011note2]. The progress of anatomical knowledge has also left brilliant testimonies in the field of painting, which make the renown of the Renaissance today. The precision of these artists' traits has also allowed some retrospective medical analyses, some of them going so far as to identify the signs of a tumour in certain subjects [@bianucci2018earliest]. Such is the bluish stain on the left breast of the Bathsheba painted by Rembrandt (Figure \@ref(fig:bath)) which has been subject to controversial interpretations, sometimes described as an example of "skin discolouration, distortion of symmetry with axillary fullness and peau d'orange" [@braithwaite1983rembrandt] and sometimes spared by photonic and computationnal analyses [@heijblom2014monte]. The mechanisms of the disease only began to be elucidated with the appearance of the microscope in the 19th century, which revealed its cellular origin [@hajdu2012note]. The classification and description of cancers is then gradually refined and the first non-surgical treatments appear with the discovery of ionising radiation by the Curies [@hajdu2012note2]. The 20th century is then the century of understanding the causes of cancer [@hajdu2013note; @hajdu2013note2]. Some environmental exposures are characterized as asbestos or tobacco. Finally, the biological mechanisms become clearer with the identification of tmour-causing viruses and especially with the discovery of DNA [@watson1953molecular]. The foundations of our current understanding of cancer date back to this period, which marks the beginning of the molecular biology of cancer. It is this branch of biology that contains the bulk of the knowledge that will be used to build our mechanistic models, and it will be later detailed in Section \@ref(molecular-biology).  
  
One of the ways to read this brief history of cancer is to see that theoretical and clinical progress has not followed the same timeframes.The medical and clinical management of cancers initially progressed slowly but surely, and this in the absence of an understanding of the mechanisms of cancer. Conversely, the theoretical progress of the last century has not always led to parallel medical progress, except on certain specific points. The interaction between the two is therefore not always obvious. The transformation of fundamental knowledge into medical and clinical impact is therefore of particular importance. This is what is called *translational medicine*, the aim of which is to go from laboratory bench to bedside [@cohrs2015translational]. It is, modestly, in this perspective that the mechanistic models of cancer that will receive particular attention in this thesis are placed. Their objective is to integrate biological knowledge, or at least a synthesis this knowledge, in order to transform it into  with a relevant clinical information.

## Cancer from a distance: epidemiology and main figures

Before going down to the molecular level, it is important to detail some figures and trends in the epidemiology of cancer today. Following the description in the previous section, cancer is first and foremost defined as a disease. Considered to be a unique disease, it caused 18.1 million new cancer cases and 9.6 million cancer deaths in 2018 according to the Global Cancer Observatory affiliated to World Health Organization [@bray2018global]. However, these aggregated data conceal disparities of various kinds. The first one is geographical. Indeed, mortality figures make cancer one of the leading causes of premature death in most countries of the world but its importance relative to other causes of death is even greater in the more developed countries (Figure \@ref(fig:globocan-map)). All in all, cancer is the first or second cause of premature death in almost 100 countries worldwide [@bray2018global]. These differences call for careful consideration of the impact of population age structures and health-related covariates.

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/globocan-map} 

}

\caption[Network visualization of *model* thesaurus entries]{(ref:globocan-map-caption)}(\#fig:globocan-map)
\end{figure}
(ref:globocan-map-caption) **World map and national rankings of cancer as a cause of premature death.** Classification of cancer as a cause of death before the age of 70, based on data for the year 2015. Original Figure, data and methods from @bray2018global.

A second disparity lies in the different types of cancer. If we classify tumours solely according to their location, i.e. the organ affected first, we already obtain very wide differences. First of all, the incidence varies considerably (Figure \@ref(fig:cancer-tissues)A)). Cancers do not occur randomly anywhere in the body and certain environments or cell types appear to be more favourable [@tomasetti2015variation]. Mortality is also highly variable but is not directly inferred from incidence. Not all types of cancer have the same prognosis (Figure \@ref(fig:cancer-tissues)A and B) and survival rates [@liu2018integrated]. Although breast cancer is much more common than lung cancer, it causes fewer deaths because its prognosis is, on average, much better. The mechanisms at work in the emergence of cancer are therefore not necessarily the same as those that will govern its evolution or its response to treatment. And still on the response to treatment, Figure \@ref(fig:cancer-tissues)B highlights another disparity: not only are the survival prognosis associated with each cancer very different, but the evolution (and generally the improvement) of these prognoses has been very uneven over the last few decades. This means that theoretical and therapeutic advances have not been applied to all types of cancer with the same success. It is one more indication of the diversity of biological mechanisms at work, which make it impossible to find a panacea, and which, on the contrary, encourage us to carefully consider the particularities of each tumour, both to understand them and to treat them. Under a generic name and in spite of common characteristics, the cancers thus appear as extremely heterogeneous. And to understand the sources of this heterogeneity, it will be necessary to place ourselves on a much smaller scale.  
  

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{02-Cancer_files/figure-latex/cancer-tissues-1} 

}

\caption[Some analyses around Lotka-Volterra model of a prey-predator system]{(ref:cancer-tissues-caption)}(\#fig:cancer-tissues)
\end{figure}
(ref:cancer-tissues-caption) **Incidence, mortility and survival per cancer types**. (A) World incidence and mortality for the 19 most frequent cancer types in 2018, expressed age-standardized rates (adjusted age structure based on world population); data retrieved from [Global Cancer Observatory](https://gco.iarc.fr/today/home). (B) Evolution of 5-years relative survival for the same cancer types based on US data from SEER registries in 1975-1977 and 2006-2012; data retrieved from @jemal2017annual.

## Basic molecular biology of cancer {#molecular-biology}

[@weinberg2013biology]

[@tomasetti2015only]

## High-throughput data and multi-omics

## From genetic to network disease

[@sanchez2018oncogenic]
