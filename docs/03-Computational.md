# Mechanistic and computational modeling of cancer: from complex disease to systems biology

\epigraph{"How remarkable is life? The answer is: very. Those of us who deal in networks of chemical reactions know of nothing like it... How could a chemical sludge become a rose, even with billions of years to try."}{George Whitesides}



\initial{T}he previous chapter identified the need to organize cancer knowledge and data. The integration of biological knowledge, particularly in the form of networks, is a first step in this direction. The deepening of knowledge, however, requires the ability to manipulate objects even more, to experiment, to dissect their behaviour in an infinite number of situations, such as the astronomer with his orrery or physicians with their old anatomical models (Figure \@ref(fig:anatomy)). Is it then possible to create mechanistic models of cancer in the same way?






\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/anatomy} 

}

\caption[Dissecting a biological phenomenon using a non-computational model]{(ref:anatomy-caption)}(\#fig:anatomy)
\end{figure}
(ref:anatomy-caption) **Dissecting a biological phenomenon using a non-computational model.**  Rembrandt, *The Anatomy Lesson of Dr Nicolaes Tulp*, 1634, oil on canvas, Mauritshuis museum, The Hague

## Introducing the diversity of mechanistic models of cancer

Modeling cancer is not a new idea. And the diversity of biological phenomena at work in cancer has given rise to an equally important diversity of models and formalisms, which we seek here to give a brief overview in order to better identify the specific models that we will focus on later. One way to order this diversity is to consider the scales of these models (Figure \@ref(fig:multiscale)). Indeed, cancer can be read at different levels, from the molecular level of DNA and proteins, to the cellular level, to the level of tissues and the organism [@anderson2008integrative]. Models have been proposed at all these scales, using different formalisms [@bellomo2008foundations] and answering different questions.  
  

Consistent with the evolution of knowledge and data, the early models were at the macroscopic level. While methods and terminologies may have changed, there are nevertheless traces of these models as early as the 1950s. We then speak rather of mathematical modeling with a meaning that is nevertheless intermediate between what we have defined as mechanistic models and statistical models [@byrne2010dissecting]. First, the initiation of tumorigenesis was theorized with biologically-supported mathematical expressions in order to make sense of cancer incidence statistics [@armitage1954age, @knudson1971mutation]. These models, however, remained relatively descriptive in that they did not shed any particular light on the biological mechanisms involved and focused on gross characteristics
of tumours. The integration of more advanced knowledge as well as the progressive refinement of mathematical formalisms has nevertheless allowed these models to proliferate while gaining in interpretability, with for instance mechanistic models of metastatic relapse [@nicolo2020machine]. Always on a macroscopic scale, the study of tumor growth has also been the playground of many mathematicians [@araujo2004history; byrne2010dissecting], even predicting invasion or response to surgical treatments using spatial modeling [@swanson2003virtual]. This line of research is still quite active today and provides a mathematical basis for comparison with tumour experimental growth [@benzekry2014classical].  
  

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/multiscale} 

}

\caption[The different scales of cancer modeling]{(ref:multiscale-caption)}(\#fig:multiscale)
\end{figure}
(ref:multiscale-caption) **The different scales of cancer modeling.** Cancer can be approached at different scales, from molecules to organs, using different data (dark blue), but often with the direct or indirect objective of contributing to the study of clinically interpretable phenomena (yellow boxes), in particular by studying the influence of anticancer agents (pale blue). Reprinted from @barbolosi2016computational.


Taking it down a step further, it is also possible to model cancer at the cellular level, for example by looking at the clonal evolution of the cancer [@altrock2015mathematics]. The aim is then to understand the impact of the processes of mutation, selection, expansion and cohabitation of different populatons of cells, at specifc rates. The accumulation of a mutation in a population of cells can thus be studied [@bozic2010accumulation]. Modeling at the cellular level is well suited to the study of interactions between cells, between cancer cells and their environment or with the immune system. Similar to other kinds of studies of population dynamics, formalisms based on differential equations are quite common, some conceptually analogous to the Lotka Volerra system presented in section \@ref(lotkasection) [@bellomo2008foundations]; but there are many other methods such partial differential equations or agent-based modeling [@letort2019physiboss].  
  

Finally, at an even smaller scale, it is possible to model the molecular networks at work in cells [@le2015quantitative]. The aim is then to simulate mathematically how the different genes and molecules regulate each other, transmit information and, in the case of cancer, end up being deregulated [@calzone2010mathematical; @flobak2015discovery]. These models will be the subject of the thesis and will therefore be defined more precisely and used to detail the concepts and tools of systems biology in the following sections. It can already be noted that while these models can integrate the most fundamental biological mechanisms of living organisms, one of the most burning questions is whether it is possible to link them to the larger scales that are clinically more interesting (tissues, organs etc.). Can these models tell us about the molecular nature of cancer? About patient survival? Their response to treatment? These questions apply to all of the above models, whatever their scales (Figure \@ref(fig:multiscale)), but are more difficult to answer for models defines at molecular scale that are further from the clinical data of interest. The aim of this thesis is to provide potential answers to these questions. One of the ways of approaching these issues has been to propose multi-scale models, which are nevertheless very complex [@anderson2008integrative; @powathil2015systems]. We will focus here on the use of models defined almost exclusively at the molecular scale, which is assumed to be prominent, to study what can be inferred on the larger scales.

## Cell circuitry and the need for cancer systems biology

Most biological systems, and certainly cells, fall into the category of complex systems. These are systems made up of many interacting elements. While these systems can be found in many different scientific fields, the cell as a complex system is characterized by the diversity and multifunctionality of its constituent elements (genes, proteins, small molecules, enzymes), which nevertheless contribute to organized and a priori non-chaotic behaviour [@kitano2002computational]. Thus, the role of a protein such as the p53 tumour suppressor can only be understood by taking into account the interplay between its relationships with transcription factors and biochemical modifications of the molecule itself [@kitano2002computational]. In a cell, as in any complex system, the multiplication of components and interactions can make the response or behaviour of the system unexpected or unpredictable. Non-linear responses, such as abrupt changes in the state of a system, called critical transitions, can be observed in response to a moderate change in the signal [@trefois2015critical]. Generally speaking, it is possible to observe emergent behaviours, i.e. behaviours of the system as a whole that were not trivially deducible from the individual behaviours of its components. This has been documented, through experiments and simulations, in the study of cell signalling pathways and the resulting biological decisions [@bhalla1999emergent; @helikar2008emergent]. These considerations have thus given rise to system-level or holistic approaches that aim to integrate data and knowledge into more comprehensive representations, often called **systems biology**.  
  

What is true for the cell in general is just as true for cancer in particular. Understanding the intertwining of signaling pathways is necessary to study their contributions to different cancer hallmarks, as shown in Figure \@ref(fig:circuit). The concepts described above can thus be transposed to cancer systems biology [@hornberg2006cancer; @kreeger2010cancer; @barillot2012computational]. Indeed, it is often a question of understanding or predicting the impact of perturbations on cellular networks. Understanding how a single genetic mutation disrupts and reprograms networks, or even predicting the responses triggered by a drug on a presumably promising molecular target, makes little sense without integrated approaches. In addition, Cancers are characterized by the accumulation of numerous mutations and alterations over time that must be considered concomitantly. These points of view of biologists and modellers reinforce the observation already made in the previous chapter of cancer as a network disease, as a system disease (Figure \@ref(fig:pathways)).  
  
Finally, to conclude this general presentation, it is important to understand that while small molecular network modeling is not recent, the rise and multiplication of wide range systems biology approaches is very much related to the production of biological data [@de2002modeling]. The last few decades have seen the emergence of high-throughput data that have made it possible to identify and link hundreds of genes or proteins involved in cancer. Exploring the interaction and back and forth between these models and the data they use or predict is therefore of utmost importance. In addition, the now massive amount of data has also imposed mathematical or computational approaches as central to managing this profusion. Thus, Figure \@ref(fig:pubmed) shows that while the number of scientific articles devoted to cancer has increased drastically since the 1950s (panel A), the proportion of these same articles mentioning *models*, *networks* or *computational* approaches has also increased (panel B), illustrating a change in paradigms.  
  

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{03-Computational_files/figure-latex/pubmed-1} 

}

\caption[PubMed trends in cancer studies.]{(ref:pubmed-caption)}(\#fig:pubmed)
\end{figure}
(ref:pubmed-caption) **PubMed trends in cancer studies.** (A) PubMed articles with the word *Cancer* in either title or abstract from 1950 to 2019. (B) Proportion of the *Cancer* articles with additional keywords expressed as PubMed logical queries.

## Mechanistic models of molecular signaling

Once the context has been defined, both biologically and methodologically, it is possible to begin the exploration of the models that will constitute the core of this thesis: the **mechanistic models of molecular networks** and signaling pathways. Before describing and illustrating some of the existing mathematical formalisms, it is possible to describe the common fundamental elements of this family of approaches.

### Common elements to capture the complexity

\begin{figure}

{\centering \includegraphics[width=0.6\linewidth]{fig/cycle} 

}

\caption[Modeling a biological network: an iterative and cyclical process]{(ref:cycle-caption)}(\#fig:cycle)
\end{figure}
(ref:cycle-caption) **Modeling a biological network: an iterative and cyclical process.** [@beal2020modelisation]

Networks in action

### Different formalisms for different applications

With two main formalisms: ODE and logical
[@le2015quantitative]
[@de2002modeling]

### Some examples of complex features


Theory --> Features of complex systems: emergence, non-linearity, feedback

bistable and switches [@markevich2004signaling]

tyson ode examples breast [@tyson2011dynamic] and general [@tyson2003sniffers]

network and complex elements. Examples of loops [@kitano2002computational] [@kitano2002systems]


## Applications --> impact of data // Clincal impact

Boris Kholodenko
With data also [@bouhaddou2018mechanistic]
Details Fey





