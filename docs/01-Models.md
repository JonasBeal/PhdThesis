# (PART) Cells and their models {-}

# Scientific modeling: abstract the complexity

\epigraph{"Ce qui est simple est toujours faux. Ce qui ne l'est pas est inutilisable."}{Paul Valéry (Mauvaises pensées et autres, 1942)}



\initial{T}he notion of modeling is embedded in science, to the point that it has sometimes been used to define the very nature of scientific research. What is called a model can, however, correspond to very different realities which need to be defined before addressing the object of this thesis which will consist, if one wants to be mischievous, in analyzing models with other models. This semantic elucidation is all the more necessary as this thesis is interdisciplinary, suspended between systems biology and biostatistics. In order to convince the reader of the need for such a preamble, he is invited to ask a statistician and a systems biologist the question how they would define what a model is.





\begin{figure}[ht]

{\centering \includegraphics[width=0.9\linewidth]{fig/orrery} 

}

\caption[A scientist and his model]{(ref:orrery-caption)}(\#fig:orrery)
\end{figure}
(ref:orrery-caption) **A scientist and his model.** Joseph Wright of Derby, *A Philosopher Giving a Lecture at the Orrery (in which a lamp is put in place of the sun)*, c. 1763-65, oil on canvas, Derby Museums and Art Gallery

## What is a model?

<!-- Generic intro -->
### In your own words

A model is first of all an ambiguous object and a polysemous word. It therefore seems necessary to start with a semantic study. Among the many meanings and synonymous proposed by the dictionary (Figure \@ref(fig:visual-thesaurus)), while some definitions are more related to art, several find echoes in scientific practice. It is sometimes a question of the physical representation of an object, often on a reduced scale as in Figure \@ref(fig:orrery), and sometimes of a theoretical description intended to facilitate the understanding of the way in which a system works [@dictionnarymodel]. It is even sometimes an ideal to be reached and therefore an ambitious prospect for an introduction.


\begin{figure}[ht]

{\centering \includegraphics[width=0.9\linewidth]{fig/visualThesaurus} 

}

\caption[Network visualization of *model* thesaurus entries]{(ref:visual-thesaurus-caption)}(\#fig:visual-thesaurus)
\end{figure}
(ref:visual-thesaurus-caption) **Network visualization of *model* thesaurus entries.** Generated with the ['Visual Thesaurus'](https://www.visualthesaurus.com) ressource

<!-- For scientists -->

The narrower perspective of the scientist does not reduce the completeness of the dictionary's description to an unambiguous object [@bailer2002scientists]. In an attempt to approach these mult-faceted objects that are the models, Daniela Bailer-Jones interviewed different scientists and asked them the same question: what is a model? Across the different profiles and fields of study, the answers vary but some patterns begin to emerge (Figure \@ref(fig:interviews)). A model must capture the essence of the phenomenon being studied. Because it eludes, voluntarily or not, many details or complexity, it is by nature a simplification of the phenomenon. These limitations may restrict its validity to certain cases or suspend it to the fulfilment of some hypotheses. They are not necessarily predictive, but they must be able to generate new hypotheses, be tested and possibly questioned. Finally, and fundamentally, they must provide insights about the object of study and contribute to its understanding. 

\begin{figure}[ht]

{\centering \includegraphics[width=0.9\linewidth]{01-Models_files/figure-latex/interviews-1} 

}

\caption[Scientists talk about their models: words cloud.]{(ref:interviews-caption)}(\#fig:interviews)
\end{figure}
(ref:interviews-caption) **Scientists talk about their models: words cloud.** Cloud of words summarizing the lexical fields used by scientists to talk about their models in dedicated interviews [@bailer2002scientists].

These definitions circumscribe the *model* object, its use and its objectives, but they do not in any way describe its nature. And for good reason, because even if we agree on the described contours, the biodiversity of the models remains overwhelming for taxonomists:

>*Probing models, phenomenological models, computational models, developmental models, explanatory models, impoverished models, testing models, idealized models, theoretical models, scale models, heuristic models, caricature models, exploratory models, didactic models, fantasy models, minimal models, toy models, imaginary models, mathematical models, mechanistic models, substitute models, iconic models, formal models, analogue models, and instrumental models are but some of the notions that are used to categorize models.*<br/>
>[@frigg2020models]

### Physical world and world of ideas

Without claiming to be exhaustive, we can make a first simple dichotomy between physical/material and formal/intellectual models [@rosenblueth1945role]. The former consist in replacing the object of study by another object, just as physical but nevertheless simpler or better known. These may be models involving a change of scale such as the simple miniature replica placed in a wind tunnel, or the metal double helix model used by Watson and Crick to visualize DNA. In all these cases the model allows to visualize the object of study (Figure \@ref(fig:planets) A and B) to manipulate it and play with it to better understand or explain, just like the scientist with his orrery (Figure \@ref(fig:orrery)). In the case of biology, we will think mainly of model organisms such as drosophila, zebrafish or mice, for example. We then benefit from the relative simplicity of their genomes, a shorter time scale or ethical differences, usually to elucidate mechanisms of interest in humans. Correspondence between the target system and its model can sometimes be more conceptual, such as that ones relying on mechanical–electrical analogies: a mechanical system (e.g. a spring-mass system) can sometimes be represented by an electric network (e.g. a RLC circuit).

\begin{figure}[ht]

{\centering \includegraphics[width=0.9\linewidth]{01-Models_files/figure-latex/planets-1} 

}

\caption[Orrery, planets and models]{(ref:planets-caption)}(\#fig:planets)
\end{figure}
(ref:planets-caption) **Orrery, planets and models**. Physical models of planetary motion, either geocentric (Armillary sphere from *Plate LXXVII* in [*Encyclopedia Britannica*](https://commons.wikimedia.org/wiki/File:EB1711_Armillary_Sphere.png), 1771) or heliocentric in panel B (Bion, 1751, [catalogue Bnf](https://gallica.bnf.fr/ark:/12148/btv1b2600252q/f8.item.r=Bion)) and some geometric representations by Johannes Kepler in panel C (in [*Astronomia Nova*](https://commons.wikimedia.org/wiki/File:Kepler_astronomia_nova.jpg), 1609)

The model is then no longer simply a mimetic replica but is based on an intellectual equivalence: we are gradually moving into the realm of formal models [@rosenblueth1945role]. These are of a more symbolic nature and they represent the original system with a set of logical or mathematical terms, describing the main driving forces or similar structural properties as geometrical models of planetary motions summarized by Kepler in Figure \@ref(fig:planets)C. Historically these models have often been expressed by sets of mathematical equations or relationships. Increasingly, these have been implemented by computer. Despite their sometimes less analytical and more numerical nature, many so-called computational models could also belong to this category of formal models. There are then many formalisms, discrete or continuous, deterministic or stochastic, based on differential equations or Boolean algebra [@fowler1997mathematical]. Despite their more abstract nature, they offer similar scientific services: it is possible to play with their parameters, specifications or boundary conditions in order to better understand the phenomenon. One can also imagine these formal models from a different perspective, which starts from the data in a bottom-up approach instead of starting from the phenomenon in a top-down analysis. These models will then often be called statistical models or models of data[@frigg2020models]. This distinction will be further clarified in section \@ref(stat-mech).

To summarize and continue a little longer with the astronomical metaphor, the study of a particularly complex system (the solar system) can be broken down into a variety of different models. Physical and mechanical models such as armillary spheres (\@ref(fig:planets)A and B), which make it possible to touch the object of study. Moreover, we can observe the evolution of models which, when confronted with data, have progressed from a geocentric to a heliocentric representation to get closer to the current state of knowledge. Sometimes, models with more formal representations are used to give substance to ideas and hypotheses (\@ref(fig:planets)C). One of the most conceptual forms is then the mathematical language and one can thus consider that the different models find their culmination in Kepler's equations about orbits, areas and periods that describe the elliptical motion of the planets. We refer to them today as Kepler's laws. The model has become a law and therefore a paragon of mathematical modeling [@wan2018mathematical].

### Preview about cancer models

As we get closer to the subject of our study, and in order to illustrate these definitions more concretely, we can take an interest in the meaning of the word *model* in the context of cancer research. For this, we restrict our corpus to articles responding to the "cancer model" search in the Pubmed article database. Among these, we look at the occurrences of the word *model* and the sentences in which it is included. This cancer-related context of model is represented as a tree in Figure \@ref(fig:pubmed-tree). Some of the distinctions already mentioned can be found here. The *mouse* and *xenograft* models, which will be discussed later in this thesis, represent some of the most common physical models in cancer studies. These are animal models in which the occurrence and mechanisms of cancer, usually induced by the experimenter, are studied. On the other hand, *prediction*, *prognostic* or *risk score* models refer to formal models and borrow from statistical language. 

\begin{figure}[ht]

{\centering \includegraphics[width=0.9\linewidth]{fig/pubmed-tree} 

}

\caption[Tree visualization of *model* semantic context in cancer-related literature]{(ref:pubmed-tree-caption)}(\#fig:pubmed-tree)
\end{figure}
(ref:pubmed-tree-caption) **Tree visualization of *model* semantic context in cancer-related literature** Generated with the ['PubTrees'](https://esperr.github.io/pub-trees/) tool by Ed Sperr, and based on most relevant PubMed entries for "cancer model" search.

Another way to classify cancer models may be to group them into the following categories: *in vivo*, *in vitro* and *in silico*. The first two clearly belong to the physical models but one uses whole living organisms (a human tumour implanted in an immunodeficient mouse) and the other separates the living from its organism in order to place it in a controlled environment (tumour cells in growth medium in a Petri dish). **In the thesis, data from both *in vivo* and *in vitro* models will be used. However, unless otherwise stated, a model will always refer to a representation *in silico*.** This third category, however, contains a very wide variety of models [@deisboeck2009silico], to which we will come back in chapter \@ref(computational_cancer). A final ambiguity about the nature of the formal models used in this thesis needs to be clarified beforehand.

## Statistics or mechanistic {#stat-mech}

Within formal models -> 2 kinds

[@baker2018mechanistic]

https://gosilico.com/technology/mechanistic-vs-statistical-models/

Mechanistic already answer the "how" --> causality inside
Breiman --> Inside the box

https://theartofmodelling.wordpress.com/2012/02/19/mechanistic-models-what-is-the-value-of-understanding/


Example with data, stat and mech for Lotka-Volterra 
https://mc-stan.org/users/documentation/case-studies/lotka-volterra-predator-prey.html
http://www2.nau.edu/lrm22/lessons/predator_prey/predator_prey.html

## Simplicity is the ultimate sophistication

To conclude this modeling introduction, it is important to highlight one of the most important points already introduced in a concise manner by Valéry at the beginning of this chapter. Whatever its nature, a model is a simplified representation of reality and by extension is always wrong to a certain extent. This is a generally well-accepted fact, but it is crucial to understand the implications for the modeller. This simplification is not a collateral effect but an intrinsic feature of any model:

>*No substantial part of the universe is so simple that it can be grasped and controlled without abstraction. Abstraction consists in replacing the part of the universe under consideration by a model of similar but simpler structure. Models, formal and intellectual on the one hand, or material on the other, are thus a central necessity of scientific procedure.*<br/>
>[@rosenblueth1945role]

Therefore, a model exists only because we are not able to deal directly with the phenomenon and simplification is a necessity to make it more tractable
[@potochnik2017idealization]. This simplification appeared many times in the studies of frictionless planes or theoretically isolated systems, in a totally deliberate strategy. However, this idealization can be viewed in several ways [weisberg2007three]. One of them, called Aristotelian or minimal idealization, is to eliminate all the properties of an object that we think are not relevant to the problem in question. This amounts to lying by omission or making assumptions of insignificance by focusing on key causal factors only [@frigg2020models]. We therefore refer to the *a priori* idea that we have of the phenomenon. The other idealization, called Galilean, is to deliberately distort the theory to make it tractable as explicited by Galileo himself:

>*We are trying to investigate what would happen to moveables very diverse in weight, in a medium quite devoid of resistance, so that the whole difference of speed existing between these moveables would have to be referred to inequality of weight alone. ... Since we lack such a space, let us (instead) observe what happens in the thinnest and least resistant media, comparing this with what happens in others less thin and more resistant.*

This fairly pragmatic approach should make it possible to evolve iteratively, reducing distortions as and when possible. We will have the opportunity to come back to the idealizations made in the course of the cancer models but it is already possible to give some orientations. The experimenter who seeks to study cancer using cell lines or animal models is clearly part of Galileo's lineage. The mathematical or *in silico* modeler has a more balanced profile. The design of qualitative mechanistic models based on prior knowledge, which is the core of the second part of the thesis, is more akin to minimal idealization, which seeks to highlight the salient features of a system. This pragmatism consisting in creating computationnaly-tractable models  is also quite widespread, particularly in highly dimensional statistical approaches.

Because of the complexity of the phenomena, simplification is therefore a necessity. The objective then should not necessarily be to make the model more complex, but to match its level of simplification with its assumptions and objectives. Faced with the temptation of the author of the model, or his reviewer, to always extend and complicate the model, it could be replied with Lewis Carrol words^[More concisely, in [@rosenblueth1945role], "best material model for a cat is another cat, or preferably the same cat."]:

> *"That’s another thing we’ve learned from your Nation," said Mein Herr, "map-making. But we’ve carried it much further than you. What do you consider the largest map that would be really useful?"<br/>
"About six inches to the mile."<br/>
"Only six inches!" exclaimed Mein Herr. "We very soon got to six yards to the mile. Then we tried a hundred yards to the mile. And then came the grandest idea of all! We actually made a map of the country, on the scale of a mile to the mile!"<br/>
"Have you used it much?" I enquired.<br/>
"It has never been spread out, yet," said Mein Herr: "the farmers objected: they said it would cover the whole country, and shut out the sunlight! So we now use the country itself, as its own map, and I assure you it does nearly as well."<br/>
>Lewis Carroll, *Sylvie and Bruno* (1893)


