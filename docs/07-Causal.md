
# (PART) Statistical quantification of the clinical impact of models {-}

# Clinical evidence generation and causal inference

\epigraph{"Felix qui potuit rerum cognoscere causas."}{Virgil (Georgics, 29 BC)}



\initial{T}he mechanistic models of cancer presented in the previous section have allowed us to integrate the omics data, to make them speak in order to better understand the clinical characteristics of cell lines or patients. But beyond their undeniable intellectual and scientific interest, do they have a direct clinical value? Given the abundance and complexity of patient data available to physicians, the use of computer tools and mathematical models is inevitable and increasingly frequent. Because of their explicit representation of phenomena, mechanistic models can provide a more easily understood alternative for doctors or patients. Is it therefore desirable and relevant to use these models in support of medical decision making? And how can their clinical validity and impact be rigorously measured?




  
Before studying mechanistic models in more detail, this chapter describes some general elements on how clinical evidence may be generated and the methods developed for this purpose. This presentation is intended as a pedagogical introduction to the causal inference methods that will be used thereafter. Many other methods can be used to answer similar questions, particularly by analogy to the evaluation of prognostic or predictive biomarkers, but they will not be discussed here.

\BeginKnitrBlock{summarybox}<div class="summarybox">
#### Scientific content {-}

This short chapter introduces the framework for causal inference based on the literature and the description of causal inference in @beal2020causal.
</div>\EndKnitrBlock{summarybox}

\newcommand{\indep}{\perp \!\!\! \perp}

## Clinical trials and observational data

### Randomized clinical trials as gold standards

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/trials} 

}

\caption[Bimodality criteria and their combinations]{(ref:trials-caption)}(\#fig:trials)
\end{figure}
(ref:trials-caption) **Schematic extension of PROFILE-personalized logical models to drug investigat**

### Dangers and opportunities of observational data

## Causal inference to leverage data

Now that we have defined what we want to estimate, we need to specify the method of estimation. In cases where it would be too difficult or too early to conduct a true clinical trial we propose methods using observational data to emulate them. Indeed, it is possible to derive estimates with a causal interpretation from observational data in the context of the potential outcomes framework [@rubin1974estimating]. We will first describe briefly the fundamentals of this framework..

### First notations and causal graph

We will use $j=1,...,N$ to index the individuals in the population. $A_j$ and $Y_j$ correspond respectively to the actual treatment received by individual $j$ and the outcome. In the most simple case, treatment takes values in $\mathcal{A}=\{0, 1\}$, $1$ denoting the treated patients and $0$ the control ones. $Y_j$ corresponds to the patient's response to treatment. In the case of cancer it may be  a continuous value (e.g size of tumour), a binary value (e.g status or event indicator), or even a time-to-event (e.g time to relapse or death). Only the first two cases will be discussed later. Finally, it is necessary to take into account the possible presence of confounders influencing both $A$ and $Y$ and denoted $C_j$ for individual $j$.


### Potential outcomes framework

One standard framework to estimate causal effects relies on potential outcomes [@rubin1974estimating]. This framework is sometimes described as counterfactual because it defines variables like $Y_j(a)$ to denote the potential outcome of individual $j$ in case he has been treated by $A=a$ which may be different from what we observe if $A_j\neq a$. These counterfactual variables make it possible to write the causal estimands. For instance, in this context, we can easily compute the difference in outcome between treated patients and control patients: 
$E[Y | A=1] - E[Y | A=0].$

However, this difference has no causal interpretation as it does not offer any guarantees as to the confounding factor, as an unbalanced distribution of $C$ can induce biases Thus we define another estimate:
$E[Y(1)] - E[Y(0)].$

In this case, we compare between two ideal cohort, one in which all patients have been treated (possibly contrary to the fact) and one in which all patients have been left in the control arm (once again, possibly contrary to the fact). Under certain assumptions of consistency, positivity and conditional exchangeability, the potential outcomes framework allows to estimate these counterfactual variables and therefore infer causal estimates from observational (non-randomized) data [@rubin1974estimating, @hernan2020causal]. 

*Consistency* means that values of treatment under comparison represent well-defined interventions which themselves correspond to the treatments in the data:
$\textrm{if} \: A_j=a,  \textrm{then} \: Y_j(a)=Y_j.$

*Exchangeability* means that treated and control patients are exchangeable, i.e if the treated patients had not been treated they would have had the same outcomes as the controls, and conversely. Since we usually observe some confounders we define conditional exchangeability to hold if cohorts are exchangeable for same values of confounding $C$. Therefore conditional exchangeability will hold if there are no unmeasured confounding:
$Y(a) \indep A | C.$

*Positivity* assumption states that the probability of being administered a certain version of treatment conditional on $C$ is greater than zero:
$\textrm{if} \: P[C=c] \neq 0, P[A=a | C=c] >0.$
Intuitively, this positivity condition is required to ensure that the defined counterfactual variables make sense and do not represent something that cannot exist.

### Identification of causal effects

Different methods provide estimators to evaluate causal effect from observational data. Throughout the article, we will describe essentially one method called standardization or parametric g-formula. Details on other types of estimators are available in Supplementary Materials, sections B and C. In this simple case (Figure~\ref{fig2_DAG_single}), the causal effect of treatment $A$ can be written with standardized means (formal proof in Supplementary Materials, section A):

$$
E[Y(A=1)] - E[Y(A=0)] = \sum_{c} \Big(E[Y | A=1, C=c]-E[Y | A=0, C=c]\Big) \times P[C=c].
$$

Computationally, non-parametric estimation of $E[Y | A=a, C=c]$ is usually out of reach. Thus, on real-world dataset, $E[Y | A=a, C=c]$ is estimated through modelling and explicit computation $P[C=c]$ is replaced by its empirical estimate.
