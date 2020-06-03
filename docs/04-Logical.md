# (PART) Personalized logical models of cancer {-}

# Logical modeling principles and data integration

\epigraph{"Je suis l’halluciné de la forêt des Nombres.

Ils me fixent, avec leurs yeux de leurs problèmes ;

Ils sont, pour éternellement rester : les mêmes.

Primordiaux et définis,

Ils tiennent le monde entre leurs infinis ;

Ils expliquent le fond et l’essence des choses,

Puisqu’à travers les temps planent leurs causes."}{Émile Verhaeren (Les nombres)}



\initial{A}nother way of ordering the diversity of mechanistic models presented above is to consider their relationship to biological data. Those that make little use of these data are essentially theoretical scope models that describe the general functioning of signaling pathways and associated systems [@calzone2010mathematical]. Other models propose more quantitative models but require much more data, either experimental data generated for the occasion or the use of databases to fit the parameters. In the latter case, the necessary data is usually perturbation data: How does my system react to this or that inhibition or activation? For a single cell line this already corresponds to a large amount of data [@razzaq2018computational]. And if we want to extend these approaches to many cell lines the amount of data becomes massive [@frohlich2018efficient]. For patient-specific models, access to this perturbation data is even more difficult.





Between theoretical models that are not very demanding in terms of data but not very applicable clinically and models with a clinical focus but very demanding in terms of data, an intermediate alternative is missing. **Can patient-specific mechanistic models be developed that would provide qualitative clinical interpretation with a small amount of data, accessible even in patients?** In this part, a middle way will be described to answer positively to this question. This methodology will be based on a historically qualitative mathematical formalism already presented in the previous chapter under the name of logical modelling.

#### Publications {-}

This chapter presents the theoretical bases of logical modeling and the tools used thereafter. It does not present any original work but refers to the synthesis and analyses of logical modeling as described in @beal2019personalization and @beal2020modelisation.



## Logical modeling paradigms for qualitative description

Mathematical models serve as tools to answer a biological question in a formal way, to detect blind spots and thus better understand a system, to organize, into a consensual and compact manner, information dispersed in different articles. In the light of this definition, logical formalism (also called Boolean) may seem one of the closest to natural language in that it **can translate quite directly the statements present in the literature** such as "protein A activates protein B" or "the expression of gene C requires the joint presence of factors D and E". Indeed, shortly after the first descriptions of control circuits by @jacob1961genetic, the interest of logical models to describe biological systems was put forward by @kauffman1969homeostasis and @thomas1973boolean. Since then, studies have multiplied [@thomas1990biological], varying the fields of biological applications and also the mathematical and computational implementations [@naldi2018colomoto]. The two subsections below summarize the characteristics common to most of the logical formalisms, before detailing the implementation chosen in this thesis in section \@ref(maboss-section).

### Regulatory graph and logical rules

A logical model is based on a network called **regulatory graph** (Figure \@ref(fig:logical)), where each node represents a component (e.g. genes, proteins, complexes, phenotypes or processes), and is associated with discrete levels of activity ($0$, $1$, or more when justified). The use of a discrete formalism in molecular network modeling relies on the highly non-linear nature of regulation, and thus on the existence of a regulatory threshold. Assuming that each variable represents a level of expression: it will take the value $0$ if the level of expression of the entity is below the regulation threshold, i.e. insufficient to carry out the regulation; and the value $1$ if it is above the threshold and regulation is possible. In other words, the control threshold discretizes the state space, here the expression levels. It is therefore possible to distinguish several thresholds for the same variable, corresponding to distinct controls that do not take place at the same expression levels. The variable is then multivalued. This extension greatly enriches the formalism, because it allows to distinguish situations that are qualitatively different and that would be confused with boolean variables. In the continuation of this thesis, we will consider by default that the activity levels are binary, $0$ corresponding to an inactive entity and $1$ to an active entity.  
  

The edges of this regulatory graph correspond to influences, either positive or negative, which illustrate the possible interactions between two entities. Positive edges can represent the formation of active complexes, mediation of synthesis, catalysis, etc. and they will be later depicted as green arrows ($\leftarrow$). Negative edges on the othe rhand can represent inhibition of synthesis, degradation, inhibiting (de)phosphorylation, etc. and they will be depicted as red turnstile ($\vdash$).

\begin{figure}

{\centering \includegraphics[width=0.5\linewidth]{fig/logical} 

}

\caption[A simple example of a logical model]{(ref:logical-caption)}(\#fig:logical)
\end{figure}
(ref:logical-caption) **A simple example of a logical model.** Regulatory graph on the left with positive (green) and negative regulations (red); a set of possible corresponding logical rules on the right.  
  

Then, each node of the regulatory graph has a corresponding Boolean variable associated to it. The variables can take two values: $0$ for absent or inactive (OFF), and $1$ for present or active (ON). These variables change their value according to a logical rule assigned to them. The state of a variable will thus depend on its logical rule, which is based on logical statements, i.e., on a function of the node regulators linked with logical connectors AND ($\&$), OR ($|$) and NOT ($!$). These operators can account for what is known about the biology behind these edges. If two input nodes are needed for the activation of the target node, they will be linked by an AND gate; to list different means of activation of a node, an OR gate will be used. For negative influences, a NOT gate will be utilized. Thus for each node, a logical rule is associated. The rules corresponding to the toy model in Figure \@ref(fig:logical) could be interpreted literally like this: A is acivated to 1 if B is active; B is updated to 1 in the absence of A and the presence/activity of C; C is an input of the model and therefore not regulated. It can be noted that the logical rules cannot be deduced only from the regulatory graph, which can be less precise and ambiguous. One could thus imagine that B is activated if C is, OR if A is not, thus changing the behavior of the model.

### State transition graph and updates

In a Boolean framework, the variables associated to each node can take two values, either $0$ or $1$. We define a model state as a vector of all node states. All the possible transitions from any model state to another are dependent on the set of logical rules that define the model. These transitions can be viewed into a graph called a **state transition graph** (STG), where nodes are model states and edges are the transitions from one model state to another. STG nodes will be later depicted with rounded squares instead of circles in order to emphasize the difference with regulatory graphs. That way, trajectories from an initial condition to all the final states can be determined. In a model with $n$ nodes, the state transition graph can contain up to $2^n$ model state nodes; thus, if $n$ is too big, the construction and the visualization of the graph becomes difficult.

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/synchronous} 

}

\caption[A simple example of a logical model]{(ref:synchronous-caption)}(\#fig:synchronous)
\end{figure}
(ref:synchronous-caption) **State transition graph and synchronous updates.** Stable state (A) and limit cycle (B) attractors obtained for the example logical model with synchronous updates (all possible updates simultaneously). Figures above/below STG edges correspond to the number of nodes updated in each transition.
  
Based the simple logical model of Figure \@ref(fig:logical) it is nevertheless possible to represent the STG comprehensively. The idea for this is to start from a state of the system and track the successive states defined by the logical rules and the corresponding updates. The first strategy to construct this STG is to change simultaneously at each time step all the variables that can be changed (Figure \@ref(fig:synchronous)). This method is referred to as a **synchronous updating strategy**. In the second method, referred to as a **asynchronous updating strategy**, variables are changed one at a time (Figure \@ref(fig:asynchronous)) and therefore each state has as many successors as there are components whose state must be changed according to logical rules (Figure \@ref(fig:asynchronous)A). The latter asynchronous method will be used exclusively in the work presented thereafter

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/asynchronous} 

}

\caption[A simple example of a logical model]{(ref:asynchronous-caption)}(\#fig:asynchronous)
\end{figure}
(ref:asynchronous-caption) **State transition graph and asynchronous updates.** Stable state (A) and limit cycle (B) attractors obtained for the example logical model with asynchronous updates (one update at a time). Figures above/below STG edges correspond to the number of nodes updated in each transition.

We then define attractors of the model as long-term asymptotic behaviors of the system. Two types of attractors are identified: stable states, when the system has reached a model state whose successor in the transition graph is itself; and cyclic attractors, when trajectories in the transition graph lead to a group of model states that are cycling. For both synchronous and asynchronous updating strategies, the toy model shows the existence of **two types of attractors: a stable steady state and a limit cycle**, depending on the initial value of $C$. There are two disconnected components of the state transition graph for this example that correspond to the two possible values for the input $C$. If $C$ is initially equal to 0 (inactive), then there exists only one stable state: $A=B=C=0$. All the trajectories in the state transition graph lead to only one model state. If $C$ is initially equal to 1, then the attractor is a limit cycle. The path in the state transition graph cycles for any initial model state of this connected component. Note that for the asynchronous and synchronous graphs, the precise paths or limit cycles may vary. To conclude, it is important to emphasize and illustrate the characteristics of asynchronous updates in this toy example. In Figure \@ref(fig:asynchronous)A, the transition from the initial state ($A=C=0;B=1$) suggests two distinct possibilities, so it is necessary to **define additional rules or heuristics to choose between possible transitions**. We will come back to this by specifying the logical modeling implementation chosen in this thesis in section \@ref(maboss-section). 

### Tools for logical modeling

Numerous tools have been developed to build logical models and study the dynamics of the systems under inverstigation, each with its own specificity. They allow, for example, to represent reglation networks; to edit, modify or infer logical rules; to identify stable states; to reduce models; to visualize graphs of synchronous or asynchronous transitions. Some also allow to integrate temporal data; to discretize expression data; to simulate the model stochastically or to integrate delays; to identify existing models, etc. Among them, we can cite GINsim [@naldi2018logical], BoolNet [@mussel2010boolnet], pyBoolNet [@klarner2016pyboolnet], BooleanNet [@albert2008boolean], CellCollective [@helikar2012cell], bioLQM [@naldi2018biolqm], MaBoSS [@stoll2012continuous; @stoll2017maboss], PINT [@Pint], CaspoTS [@ostrowskiboolean2016], or CellNOptR [@terfvecellnoptr2012]. A detailed discussion and comparison of these tools is presented in an article incorporating many of these approaches. The interaction between all these tools, their interoperability and complementarity are highlighted in the form of a notebook jupyter [@naldi2018colomoto].

## The MaBoSS framework for logical modeling {#maboss-section}

In the present study, all simulations have been performed with MaBoSS, a **Ma**rkovian **Bo**olean **S**tochastic **S**imulator whose design is summarized in Figure \@ref(fig:maboss) and precisely described by @stoll_continuous_2012 and @stoll_maboss_2017. This framework is based on an asynchronous update scheme combined with a continuous time feature obtained with Gillespie algorithm [@gillespie_general_1976], allowing simulations to be continuous in time despite the discrete nature of logical modeling. 

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/maboss} 

}

\caption[Main principles of MaBoSS simulation framework and Gillespie algorithm]{(ref:maboss-caption)}(\#fig:maboss)
\end{figure}
(ref:maboss-caption) **Main principles of MaBoSS simulation framework and Gillespie algorithm.** (A) A logical model with regulatory graph, logical rules and transition rates. (B) A coresponding state transition graph with two possible transitions in asynchronous update for a given initial state; each transition has an associated probability. (C) Random selection of a specific transition and time by the Gillespie algorithm from two uniform random variables. (D)

### Gillespie algorithm

Gillespie algorithm provides a stochastic way to choose a specific transition among several possible ones and to infer a corresponding time for this transition. Thus, MaBoSS computation results in one stochastic trajectory as a function of time. To achieve this, transition rates seen as qualitative activation or inactivation rates, must be specified for each node (Figure \@ref(fig:maboss)A). They can be set either all to the same value by default, in the absence of any indication, or in various levels reflecting different orders of magnitude: post-translational modifications are quicker than transcriptions for instance. They can also be used to vary speeds depending on inputs or even to adapt multi-valued logical mechanisms in a binary framework [@stoll_continuous_2012]. These transition rates are translated as transition probabilities in order to determine the actual transition (Figure \@ref(fig:maboss)B). Indeed, the probability for each possible transition  to be chosen for the next update is the ratio of its transition rate to the sum of rates of all possible transitions. Higher rates correspond to transitions that will take place with greater probability, or in other words more quickly.  
  

Thus at each update, the Gillespie algorithm performs the procedure described in Figure \@ref(fig:maboss)C. Two uniform random variables $u$ and $u'$ are drawn and used respectively to select the transition among the different possibilities (with $u$) and to infer the corresponding time (with $u'$). Based on the described formula, time $\delta t$ follows an exponential law whose average is equal to the inverse of the sum of all possible transition rates (Figure \@ref(fig:maboss)C). In present work, except otherwise stated, all transition states will be initially assigned to 1. 

### A stochastic exploration of model behaviours

Since MaBoSS computes stochastic trajectories, it is relevant to compute several trajectories in order to get an insight of the average behavior by generating a population of stochastic trajectories over the asynchronous state transition graph (Figure \@ref(fig:maboss)D). The aggregation of stochastic trajectories can also be interpreted as a description of an heterogeneous population. In fact, in all the examples in next chapters, all simulations have consisted on thousands of computed trajectories. The larger the model, the larger the space of possibilities and the more trajectories are required to explore it. Since several trajectories are simulated, initial values of each node can be defined with a continuous value between 0 and 1 representing the probability for the node to be defined to 1 for each new trajectory. For instance, a node with a 0.6 initial condition will be set to $1$ in $60\%$ of simulated trajectories and to $0$ in $40\%$ of the cases.  
  

In the present work, we will focus on the "asymptotic"" state of these simulations instead of transient dynamics and we will call **node scores** the asymptotic agregated score obtained by averaging all trajectories at a given final time point. The simulation time should be chosen carefully to ensure that the asymptotic state is achieved, and the term "final state" may be considered as safer. Indeed, asymptotic states are more closely related to logical model attractors than transient dynamics and are therefore less dependent on updating stochasticity and more biologically meaningful [@huang2009cancer].  
  

All in all this modeling framework is at the intersection of logical modeling and continuous dynamic modeling. If the definition of time remains rather abstract and difficult to interpret experimentally, the stochastic exploration of trajectories makes it possible to refine the purely binary interpretation of the variables.

### From theoretical models to data models?

To sum up, logical formalism makes it possible to design fairly quickly and easily models that reflect a priori knowledge of the phenomena being studied. Thus, they allow answering questions for which there is little information on the precise mechanisms involved in a disease or when there is a lack of data related to the expression of genes or the quantity of key proteins, or on the speed of certain processes. Logical models confirm that a network is a good illustration of the underlying biological question. However, in order to propose a patient-specific mechanistic approach, it seems crucial to use the biological data available. How is this possible in a formalism that is by definition quite abstract?


## Data integration and semi-quantitative logical modeling

The use of biological data to support modelling is now widespread. However, it can occur at different stages of the modelling cycle described in Figure \@ref(fig:cycle)

### Data to prepare the model

### Data to define the rules

### Data to validate the model




