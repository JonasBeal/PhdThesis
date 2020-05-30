# Mechanistic modeling of cancer: from complex disease to systems biology {#mechanistic-cancer}

\epigraph{"How remarkable is life? The answer is: very. Those of us who deal in networks of chemical reactions know of nothing like it... How could a chemical sludge become a rose, even with billions of years to try."}{George Whitesides}



\initial{T}he previous chapter identified the need to organize cancer knowledge and data. The integration of biological knowledge, particularly in the form of networks, is a first step in this direction. The deepening of knowledge, however, requires the ability to manipulate objects even more, to experiment, to dissect their behaviour in an infinite number of situations, such as the astronomer with his orrery or physicians with their old anatomical models (Figure \@ref(fig:anatomy)). Is it then possible to create mechanistic models of cancer in the same way?






\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/anatomy} 

}

\caption[Dissecting a biological phenomenon using a non-computational model]{(ref:anatomy-caption)}(\#fig:anatomy)
\end{figure}
(ref:anatomy-caption) **Dissecting a biological phenomenon using a non-computational model.**  Rembrandt, *The Anatomy Lesson of Dr Nicolaes Tulp*, 1634, oil on canvas, Mauritshuis museum, The Hague

## Introducing the diversity of mechanistic models of cancer

Modeling cancer is not a new idea. And the diversity of biological phenomena involved in cancer has given rise to an equally important diversity of models and formalisms, which we seek here to give a brief overview in order to better identify the specific models that we will focus on later. One way to order this diversity is to consider the scales of these models (Figure \@ref(fig:multiscale)). Indeed, **cancer can be read at different levels, from the molecular level of DNA and proteins, to the cellular level, to the level of tissues and organisms** [@anderson2008integrative]. Models have been proposed at all these scales, using different formalisms [@bellomo2008foundations] and answering different questions.  
  

Consistent with the evolution of knowledge and data, the early models were at the **macroscopic level**. While methods and terminologies may have changed, there are nevertheless traces of these models as early as the 1950s. We then speak rather of mathematical modeling with a meaning that is nevertheless intermediate between what we have defined as mechanistic models and statistical models [@byrne2010dissecting]. First, the initiation of tumorigenesis was theorized with biologically-supported mathematical expressions in order to make sense of cancer incidence statistics [@armitage1954age, @knudson1971mutation]. These models, however, remained relatively descriptive in that they did not shed any particular light on the biological mechanisms involved and focused on gross characteristics
of tumours. The integration of more advanced knowledge as well as the progressive refinement of mathematical formalisms has nevertheless allowed these models to proliferate while gaining in interpretability, with for instance mechanistic models of metastatic relapse [@nicolo2020machine]. Always on a macroscopic scale, the study of tumor growth has also been the playground of many mathematicians [@araujo2004history; byrne2010dissecting], even predicting invasion or response to surgical treatments using spatial modeling [@swanson2003virtual]. This line of research is still quite active today and provides a mathematical basis for comparison with tumour experimental growth [@benzekry2014classical].

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/multiscale} 

}

\caption[The different scales of cancer modeling]{(ref:multiscale-caption)}(\#fig:multiscale)
\end{figure}
(ref:multiscale-caption) **The different scales of cancer modeling.** Cancer can be approached at different scales, from molecules to organs, using different data (dark blue), but often with the direct or indirect objective of contributing to the study of clinically interpretable phenomena (yellow boxes), in particular by studying the influence of anticancer agents (pale blue). Reprinted from @barbolosi2016computational.  
  

Taking it down a step further, it is also possible to model cancer at the **cellular level**, for example by looking at the clonal evolution of cancer [@altrock2015mathematics]. The aim is then to understand the impact of the processes of mutation, selection, expansion and cohabitation of different populatons of cells, at specifc rates. The accumulation of a mutation in a population of cells can thus be studied [@bozic2010accumulation]. Modeling at the cellular level is well suited to the study of interactions between cells, between cancer cells and their environment or with the immune system. Similar to other kinds of studies of population dynamics, formalisms based on differential equations are quite common [@bellomo2008foundations]; but there are many other methods such partial differential equations or agent-based modeling [@letort2019physiboss].  
  

Finally, at an even smaller scale, it is possible to model the **molecular networks** at work in cells [@le2015quantitative]. The aim is then to simulate mathematically how the different genes and molecules regulate each other, transmit information and, in the case of cancer, end up being deregulated [@calzone2010mathematical]. These models will be the subject of the thesis and will therefore be defined more precisely and used to detail the concepts and tools of systems biology in the following sections. It can already be noted that while these models can integrate the most fundamental biological mechanisms of living organisms, one of the most burning questions is whether it is possible to link them to the larger scales that are clinically more interesting (tissues, organs etc.). Can these models tell us something about the molecular nature of cancer? About patient survival? Their response to treatment? These questions apply to all of the above models, whatever their scales (Figure \@ref(fig:multiscale)), but are more difficult to answer for models defined at molecular scale that are further from the clinical data of interest. The aim of this thesis is to provide potential answers to these questions. One of the ways of approaching these issues has been to propose multi-scale models, which are nevertheless very complex [@anderson2008integrative; @powathil2015systems]. We will focus here on the use of models defined almost exclusively at the molecular scale, which is assumed to be prominent, to study what can be inferred on the larger scales.

## Cell circuitry and the need for cancer systems biology

Most biological systems, and certainly cells, fall into the category of **complex systems**. These are systems made up of many interacting elements. While these systems can be found in many different scientific fields, the cell as a complex system is characterized by the diversity and multifunctionality of its constituent elements (genes, proteins, small molecules, enzymes), which nevertheless contribute to organized and a priori non-chaotic behaviour [@kitano2002computational]. Thus, the role of a protein such as the p53 tumour suppressor can only be understood by taking into account the interplay between its relationships with transcription factors and biochemical modifications of the molecule itself [@kitano2002computational]. In a cell, as in any complex system, the multiplication of components and interactions can make the response or behaviour of the system unexpected or unpredictable. Non-linear responses, such as abrupt changes in the state of a system, called critical transitions, can be observed in response to a moderate change in the signal [@trefois2015critical]. Generally speaking, it is possible to observe **emergent behaviours**, i.e. behaviours of the system as a whole that were not trivially deducible from the individual behaviours of its components. This has been documented, through experiments and simulations, in the study of cell signalling pathways and the resulting biological decisions [@bhalla1999emergent; @helikar2008emergent]. These considerations have thus given rise to **system-level or holistic approaches that aim to integrate data and knowledge into more comprehensive representations, often called systems biology**.  
  

What is true for the cell in general is just as true for cancer in particular. Understanding the intertwining of signaling pathways is necessary to study their contributions to different cancer hallmarks, as shown in Figure \@ref(fig:circuit). The concepts described above can thus be transposed to **cancer systems biology** [@hornberg2006cancer; @kreeger2010cancer; @barillot2012computational]. Indeed, it is often a question of understanding or predicting the impact of perturbations on cellular networks. Understanding how a single genetic mutation disrupts and reprograms networks, or even predicting the responses triggered by a drug on a presumably promising molecular target, makes little sense without integrated approaches. In addition, cancers are characterized by the accumulation of numerous mutations and alterations over time that must be considered concomitantly. These points of view of biologists and modellers reinforce the observation already made in the previous chapter of cancer as a network disease, as a system disease (Figure \@ref(fig:pathways)).  
  

Finally, to conclude this general presentation, it is important to understand that while small molecular network modeling is not recent, the rise and multiplication of wide range systems biology approaches is very much related to the production of biological data [@de2002modeling]. The last few decades have seen the emergence of high-throughput data that have made it possible to identify and link hundreds of genes or proteins involved in cancer. Exploring the interaction and back and forth between these models and the data they use or predict is therefore of utmost importance. In addition, the now ** massive amount of data has also imposed mathematical or computational approaches as a central element in the management of this profusion** and more and more modeling approaches are focused on data integration or inference [@frohlich2018efficient; @bouhaddou2018mechanistic]. More generally, Figure \@ref(fig:pubmed) shows that while the number of scientific articles devoted to cancer has increased drastically since the 1950s (panel A), the proportion of these same articles mentioning *models*, *networks* or *computational* approaches has also increased (panel B), illustrating a change in paradigms.  

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{03-Mechanistic_files/figure-latex/pubmed-1} 

}

\caption[PubMed trends in cancer studies.]{(ref:pubmed-caption)}(\#fig:pubmed)
\end{figure}
(ref:pubmed-caption) **PubMed trends in cancer studies.** (A) PubMed articles with the word *Cancer* in either title or abstract from 1950 to 2019. (B) Proportion of the *Cancer* articles with additional keywords expressed as PubMed logical queries.

## Mechanistic models of molecular signaling

Once the context has been defined, both biologically and methodologically, it is possible to begin the exploration of the models that will constitute the core of this thesis: the **mechanistic models of molecular networks** and signaling pathways. Before describing and illustrating some of the existing mathematical formalisms, it is possible to describe the common fundamental elements of this family of approaches. 

### Networks and data

The first step is to identify the relevant biological entities from a question or system of interest (e.g. tumor suppressor genes, signaling cascades of proteins) and then to model their interactions, the regulatory relationships that link them. At this stage the model can generally be represented by a network but this word can cover different realities [@le2015quantitative]. The simplest network just represents undirected interactions between entities, which therefore only establishes relationships and not causal mechanisms. But modeling requires more precise definitions, in particular concerning the direction of the interaction (is it A that acts on B or the opposite) and its nature (type of chemical reaction, activation/inhibition etc.). This is usually summarized as **activity flows (or influence diagrams) with activation and inhibition arrows** as in Figure \@ref(fig:circuit) or Figure \@ref(fig:toyraf)A. These arrows emphasize the transormation of static networks into dynamic objects that can be manipulated and interpreted mechanistically. This work can be taken further by writing bipartite graphs, known as process descriptions, which explicitly show the different states of each variable (first type of nodes), depending on their phosphorylation sate for instance, and the reactions that link them (second type of nodes) as in Figure \@ref(fig:toyraf)B. A more precise description of these different representations and their meanings can be found in @le2015quantitative. **Once the network structure of the model has been defined, it is possible write the corresponding mathematical formalism** and potentially to refine certain parameters. Finally, the model is often confronted with new data to check its consistency with the biological behaviour studied or possibly make new predictions.  
  

However, all these steps are not linear and sequential, but rather iterative and cyclical. This **modeling cycle**, with back and forth to the data, is not specific to molecular network models, but it is possible to specify it in this case (Figure \@ref(fig:cycle)). The names of the key players involved in the question of interest are thus first extracted from adapted data or from the literature. A first mathematical translation of the relationships between the entities is then proposed before verifying the compatibility of this model with the observations, whether qualitative or quantitative. If the compatibility is not good, we come back to the definition or the parameterization of the model. If compatibility is correct, the model can be used to make new predictions or study phenomena that go beyond the initial data set. Ideally, these predictions will be tested afterwards. This cyclic approach with two successive checks is analogous to the use of validation and test data in the evaluation of most learning algorithms. This analogy can sometimes be masked by the qualitative nature of the predictions or by the lack of explicit fitting of the parameters.

\begin{figure}

{\centering \includegraphics[width=0.7\linewidth]{fig/cycle} 

}

\caption[Modeling a biological network: an iterative and cyclical process]{(ref:cycle-caption)}(\#fig:cycle)
\end{figure}
(ref:cycle-caption) **Modeling a biological network: an iterative and cyclical process.** Reprinted from [@beal2020modelisation]. A different and simpler version of this cycle is described in [@le2015quantitative].

### Different formalisms for different applications

Beyond these similarities in the construction and representation of models, the precise mathematical formalism that underlies them varies according to the type of question and the data [@de2002modeling]. For the sake of simplicity, and without exhaustiveness, we propose to divide into quantitative and qualitative formalisms which will be essentially illustrated respectively by **ordinary differential equation (ODE)** models and **logical (or Boolean) models** for which a graphical and schematic comparison is proposed in Figure \@ref(fig:toyraf).  

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/toyraf} 

}

\caption[Schematic example of logical and ODE modeling around MAPK signaling]{(ref:toyraf-caption)}(\#fig:toyraf)
\end{figure}
(ref:toyraf-caption) **Schematic example of logical and ODE modeling around MAPK signaling.** (A) Activity flow diagram of a small part of MAPK signaling, each node representing a gene or protein, with an example of logical rule for MEK node for the corresponding logical model. (B) Process description of the same diagram with BRAF and CRAF merged in RAF for the sake of simplicity; each square representing a reaction and the correspondong rate; an example differential equation is provided for the phosphorylated (active) form of MEK.

One of the most frequent approaches is the use of **chemical kinetics** equations to construct ODE systems which are a fairly natural translation of the process descritption networks described in the previous section [@polynikis2009comparing]. Each biological interaction is treated as a reaction governed by the law of mass action and, under certain hypotheses, as a differential equation (Figure \@ref(fig:toyraf)B); the set of reactions in the system then generates a set of differential equations with coupled variables, in an analogous way to the Lotka Volterra system presented in section \@ref(lotkasection). Thus the variables generally represent quantities of molecular species, for example concentrations of RNA or proteins, and the stoichiometric coefficients and reaction rates are used to define the system parameters. Approximations are sometimes made to simplify the equations, for example by assuming that they can be written as Michaelis-Menten's enzymatic reactions, which have a simple and well known behaviour. However, the theoretical accuracy of quantitative models has a cost since **each differential equation requires parameters**, such as reaction constants or initial conditions, to which the system is very sensitive [@le2015quantitative]. The biochemical interpretation of the parameters sometimes allow to find their value in the literature, if the reactions are well characterized, even if possible variations in a given biological or physical context are often unknown. Since knowledge of the values of these parameters  is often limited or even non-existent, it may require a very large volume of data (including time series) to fit the many missing parameters which can be difficult if the number of parameters is large [@villaverde2014reverse]. However, recent work has demonstrated the feasibility and scalability of this type of inference with sufficiently rich data [@frohlich2018efficient].  
  

At the same time, more qualitative approaches to modeling biological networks have been proposed with discrete variables linked together by rules expressed as logical statements [@abou2016logical]. These models are both more abstract since variables do not have a direct biological interpretation (e.g. concentration of a species) but are more versatile since they can unify different biological realities under the same formalism (e.g. activation of a gene or phosphorlation of a protein). The discrete nature of the variables can then be seen as an asymptotic case of the sigmoidal (e.g. Hill function) relationships often found in biology [@le2015quantitative]. The step function thus obtained can keep a natural interpretation in the context of biological phenomena: genes activated or not, protein present or absent etc. Similarly, interactions between species are not quantified but are based on a qualitative statements (e.g. A will be active if B and C are active), drastically reducing the number of parameters (Figure \@ref(fig:toyraf)A). If the theoretical interest of this formalism to study biological mechanisms was proposed quite early [@kauffman1969homeostasis; @thomas1973boolean], many concrete applications have also been developed over the years, particularly in cancer research [@saez2011comparing; @remy2015modeling]. This **logical formalism will constitute the core of the work presented in Part II**, where it will therefore be discussed in greater detail.  
  

\begin{table}

\caption{(\#tab:odelogic)(ref:odelogic-caption)}
\centering
\begin{tabular}[t]{>{\bfseries\raggedright\arraybackslash}p{6em}||>{\raggedright\arraybackslash}p{12em}|>{\raggedright\arraybackslash}p{12em}}
\hline
\rowcolor[HTML]{808080}  \multicolumn{1}{c}{\textcolor{white}{\textbf{ }}} & \multicolumn{1}{c}{\textcolor{white}{\textbf{Quantitative modeling}}} & \multicolumn{1}{c}{\textcolor{white}{\textbf{Qualitative modeling}}}\\
\hline
Example formalism & Ordinary differential equation (ODE) models & Logical models\\
\hline
Type of variables & Direct translation of biological quantities, usually continuous & Abstract representation of activity levels, usually discrete\\
\hline
Objective & Quantitatively accurate and temporal simulation of an experimental phenomenon & Coarse-grained simulation of qualitative phenotypes\\
\hline
Advantages & Direct confrontation with experimental data; precise; linear representation of time & Faster design; easy translation of literature-based assertions; simulation of perturbations\\
\hline
Drawbacks & Difficulty determining or fitting parameters & More difficult to link to data; lower precision\\
\hline
\end{tabular}
\end{table}
(ref:odelogic-caption) **Features of quantitative and qualitative modeling applied to biological molecular networks** (adapted from @le2015quantitative)

These two formalisms, which are among the most frequent for modelling biological networks, share many similarities, in particular the propensity to be built according to bottom-up strategies based on knowledge of the elementary parts of the model, i.e. biological entities and reactions. However, they differ in their implementation and objectives, **one aiming at the most accurate representation possible, the other seeking to capture the essence of the system's dynamics in a parsimonious way** (Table \@ref(tab:odelogic)). The opposition is not irrevocable, as illustrated by the numerous hybrid formalisms that lie within the spectrum delimited by these two extremes such as fuzzy logic or discrete-time differential equations [@le2015quantitative; @calzone2018logical]. To conclude, a comparison between the two approaches applied to the same problem is proposed by @calzone2018logical, studying the epithelio-mesenchymal transition (EMT, a biological process involved in cancer), to illustrate in concrete terms their complementarity.

### Some examples of complex features

With the help of these models, both qualitative and quantitative, many complex behaviours have been identified. Benefiting from the knowledge accumulated in the study of dynamic systems, a whole zoo of patterns with complex and non-intuitive behaviours such as non-linearities have been highlighted [@tyson2003sniffers]. The MAPK pathway, coarsely described in Figure \@ref(fig:toyraf), and often simplified as a rather unidirectional cascade, shows switch or bistability behaviors generated by the complexity of its multiple phosphorylation sites [@markevich2004signaling]. These models have also been put at the service of understanding cancer and the erroneous decision-making by cells resulting from impaired signaling pathways. Thus, @tyson2011dynamic summarize superbly well the complexity that can be hidden in the dynamics of smallest molecular networks as soon as they contain more than two entites and crossed regulations or feedback loops. Logical models have also made it possible to better dissect some complex phenomena at play in the cell such as emergent behaviours [@helikar2008emergent] or mechanisms behind mutation patterns in cancer [@remy2015modeling].


## From mechanistic models to clinical impact?

Mechanistic models have therefore undeniably led to a better understanding of the complex molecular machinery of signalling pathways. But beyond the interest that this understanding represents, do these models also have a clinical utility? In other words, **are they of clinical or only scientific value?** 

### A new class of biomarkers

Throughout this thesis, the clinical value of mechanical models will often be analyzed by analogy to that of biomarkers. Throughout this thesis, the clinical value of mechanical models will often be analyzed by analogy to that of biomarkers. Biomarkers are usually defined as measurable indicators of patient status or disease progression, such as prostate-specific antigen (PSA) for prostate cancer screening or BRCA1 mutation for breast cancer risk [@henry2012cancer]. Biomarkers also encompass multivariate signatures that identify more complex patterns with clinical significance. Taking the logic even further, it was therefore proposed that mechanistic models, which also reveal complex molecular behaviours, could be considered as biomarkers, capturing perhaps even dynamic information [@fey2015signaling].  
  

Like oncology biomarkers, the models will be divided into two categories according to their clinical objectives: **prognostic models and predictive models** [@oldenhuis2008prognostic]. Prognostic biomarkers and models are those that provide information on the evolution of cancer independently of treatment. They are therefore generally confronted with survival or relapse data. The protein Ki-67 for example, encoded by the MKI67 gene, is known to be indicative of the level of proliferation and high levels of expression are thus associated with a poorer prognosis in many cancers [@sawyers2008cancer]. Predictive biomarkers and models, on the other hand, give an indication of the effect of a therapeutic strategy. The simplest example, but not the only one, concerns biomarkers that are themselves the target of treatment: treatments based on monoclonal antibodies directed against HER2 receptors in breast cancer are only effective if the HER2 receptor has been detected in the patient [@sawyers2008cancer]. Without attempting to be exhaustive, some logical and ODE models, with either prognostic or predictive claims, will be described.

### Prognostic models

One of the first mechanical models of cell signalling to have been explicitly presented as a prognostic biomarker is the one proposed by @fey2015signaling and describing c-Jun N-terminal kinase (JNK) pathway in
neuroblastoma cells. A summary of the study is provided in Figure \@ref(fig:fey)). The model is an ODE translation of the process description network of Figure \@ref(fig:fey))A, further determined and calibrated with molecular biology experimental data obtained using neuroblastoma cell lines. We thus observe the non-linear switch-like dynamics of JNK activation as a function of cellular stress (Figure \@ref(fig:fey))B). The precise characteristics of this sgmoidal response can, however, vary from one individual to another as captured by the network output descriptors $A$, $K_{50}$ and $H$. Fey et al. proposed to perform neuroblastoma patient–specific simulations of the model, using patient gene expressions for ZAK, MKK4, MKK7, JNK and AKT genes to specify the initial conditions of the ODE system. Since JNK activation induces cell death through apoptosis, the patient-specific $A$, $K_{50}$ and $H$ derived from patient-specifc models are then analyzed as prognostic biomarkers (Figure \@ref(fig:fey))C). Readers are invited to refer to the original article for details on model calibration or binarization of network descriptors [@fey2015signaling]. The authors also showed that in the absence of positive feedback from $JNK^{**}$ to $^PMKK7$, an important component of non-linearity, the prognostic value is drastically decreased. All in all, this pipeline from ODE model to survival curves, thus provides a **paradigmatic example of the clinical interpretation of mechanistic models of molecular networks** that will be reused in later chapters for illustration purposes. Other ODE models following a similar rationale have been proposed by the same group for colorectal cancer [@hector2012clinical; @salvucci2017stepwise] or glioblastoma [@murphy2013activation; salvucci2019system]. Machine learning approaches have also been proposed to ease the clinical implementation of this kind of prognostic models by dealing with the potential lack of patient data needed to personalize them [@salvucci2019machine].  

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/fey} 

}

\caption[Schematic example of logical and ODE modeling around MAPK signaling]{(ref:fey-caption)}(\#fig:fey)
\end{figure}
(ref:fey-caption) **Mechanistic modeling of JNK pathway and survival of neuroblastima patients, as described by @fey2015signaling.** (A) Schematic representation, as a process description, for the ODE model of JNK pathway. (B) Response curve (phosphorylated JNK) as a function of the input stimulus (Stress) and characterization of the corresponding sigmoidal function with maximal amplitude $A$, Hill exponent $H$ and activation threshold $K_{50}$. (C) Survival curves for neuroblastoma patients based on binarized $A$, $K_{50}$ and $H$; binarization thresholds having been defined based on optimization screening on calibration cohort.  
  

On the logical modeling side, there are also studies including prognostic value validation. Thus, @khan2017unraveling proposed two logical models of epitelio-mesenchymal transition (EMT) in bladder and breast cancers. These models are inferred from prior mechanisms knowledge and data analysis with particular attention to potential feedback loops. Using these models, it is possible to study the behaviour of them for all combinations of model inputs (growth factors and receptor proteins) and derive subsequent signatures for good or bad prognosis. These signatures are later validated with cohorts of patients. In this case, the mechanistic model does not seek to capture a dynamic behavior but to facilitate and **make understandable the exploration of combinations of input signals that grow exponentially with the number of inputs considered**. Other formalisms, called pathway activity analysis and following the same activity flows principles (Figure \@ref(fig:toyraf)A), have been analysed in the light of their prognostic value. Their greater flexibility enables the direct use of networks of several hundred or thousands of genes, such as those present in the KEGG database [@kanehisa2012kegg]. The benefit of mechanistic modeling is then to organize high-dimensional data and to facilitate the *a posteriori* analysis of the results.
  

### Predictive models

But the explicit representation of biological entities in mechanistic models makes them particularly **suitable for the study of well-defined perturbations such as drug effects**. Indeed, by assuming that the mechanism of action of a drug is at least partially known, it is possible to integrate this mechanism into the model if it contains the target of the drug (Figure \@ref(fig:netdrug)). One can therefore simulate the effect of one drug or even compare several. These strategies have already been implemented in a qualitative way with logical models used to explain resistance to certain treatments of breast cancer [@zanudo2017network] or even highlight the synergy of certain combinations of treatments in gastric cancer [@flobak2015discovery]. The value of these models, however, is more scientific than clinical in that they focus on a single cell line or a restricted group of cell lines. The possibility to personalize the predictions or recommendations for different molecular profiles of cell lines or patients is therefore not obvious. Still within the context of logical formalism, @knijnenburg2016logic proposed a broader approach: if their model needs to be trained, it can nevertheless provide an analytical framework for several hundred cell lines, while remaining within the scope of the training data to ensure the validity of predictions.  
  

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/netdrug} 

}

\caption[Network model of oncogenic signal transduction in ER+ breast cancer, including some drugs and their targets]{(ref:netdrug-caption)}(\#fig:netdrug)
\end{figure}
(ref:netdrug-caption) **Network model of oncogenic signal transduction in ER+ breast cancer, including some drugs and their targets.** Reprinted from @zanudo2017network.

Conceptually comparable strategies can be found on the side of differential equations where large mechanical models of cell signalling are also trained to predict the response to different treatments [@bouhaddou2018mechanistic; @frohlich2018efficient]. A calibrated model can then predict the response to a combination of treatments not tested in the training data, thereby proving the ability of mechanistic models to extend their predictive value beyond the data [@frohlich2018efficient]. As with prognostic models, mechanical approaches other than logical formalisms and ODEs have been proposed and validated [@jastrzebski2018integrative]. What can be learned from these predictive models is that they require **significant training data to be able to go beyond qualitative predictions and dissect treatment response mechanisms of many cell lines simultaneously**. For obvious practical and ethical reasons, the validation of these models is for the moment limited to preclinical data since they require data for many uncertain therapeutic interventions.  
  

This first bridge between mechanistic models of cell signalling and clinical applications concludes this introductory part. The next part will be devoted to the definition of new methods to establish this connection based on logical formalism, before the third part proposes a more statistical evaluation of the prognostic and predictive values of the models presented in the previous parts. 



