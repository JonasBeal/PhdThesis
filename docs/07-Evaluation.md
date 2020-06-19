
# (PART) Statistical quantification of the clinical impact of models {-}

# Information flows in mechanistic models of cancer

\epigraph{"Et l'effet qui s'en va nous decouvre les causes."}{Alfred de Musset (Poésies nouvelles, 1843)}



\initial{T}he mechanistic models of cancer presented in the previous section have allowed us to integrate the omics data, to make them speak in order to better understand the clinical characteristics of cell lines or patients. But beyond their undeniable intellectual and scientific interest, do they have a direct clinical value? Given the abundance and complexity of patient data available to physicians, the use of computer tools and mathematical models is inevitable and increasingly frequent. Because of their explicit representation of phenomena, mechanistic models can provide a more easily understood alternative for physicians or patients. Is it therefore desirable and relevant to use these models in support of medical decision making? And how can their clinical validity and impact be rigorously measured?




  
First of all, the purpose of this chapter is to outline some of the limitations of the previously presented evaluations of mechanistic models. These evaluations answered the question: are the models of clinical value? We will show that an additional question could be: **do mechanistic models have an added clinical value?**

\BeginKnitrBlock{summarybox}<div class="summarybox">
#### Scientific content {-}

This chapter is relying on original unpublished content. The exploratory analyses presented below have been the basis for the following chapters
</div>\EndKnitrBlock{summarybox}

## Processing of biological information

Mechanistic models, and their outputs in particular, have so far been considered and evaluated as biomarkers. A comprehensive appreciation requires that they be seen as information processing tools.

### Information in, information out

Indeed, the mechanistic models presented in this thesis (Figures \@ref(fig:fey), \@ref(fig:PROFILE-METABRIC-Survival) and \@ref(fig:BRAF-results)) can be schematically represented by Figure \@ref(fig:box-mech): inputs $X$ (often omics data) are processed through a mechanistic model (here the grey box) to result in an output $Y$. These models can thus be assimilated to a mathematical transformation, often non-linear, of $X$ in $Y$. Thus, when validating the biological or clinical relevance of $Y$, either by calculating a correlation with the ground truth or by using it to stratify survival curves, only the absolute value of $Y$ is checked. This is an important step and a prerequisite for a well-constructed model. On the other hand, it is not sufficient information to understand how the model works. Indeed, the inputs $X$ probably also have a predictive or clinical value. In short, measuring only the output value of the model does not necessarily reveal the model's ability to make sense of the data it uses. At the extreme, it is conceivable that a random function of some valuable inputs could be correlated to the biological reality.

\begin{figure}

{\centering \includegraphics[width=0.8\linewidth]{fig/box-mech} 

}

\caption[Evaluation of a mechanistic model]{(ref:box-mech-caption)}(\#fig:box-mech)
\end{figure}
(ref:box-mech-caption) **Evaluation of a mechanistic model.** Adapted from Figure \@ref(fig:boxes).

Therefore, the question of incremental value of the model can be explained as follows: what does the output of the model represent in relation to the inputs? If we restrict ourselves to cases where the absolute biological/clinical value of $Y$ is positive, we can then identify two families of situations. We can imagine a situation where the model has improved the value of the inputs. The outputs would then have a higher value than the inputs (better biological validation etc.), or in any case a complementary value, a value not present in the inputs. This would correspond to the capture by the model of emerging or non-linar effects. In the second situation, the output does not capture emergent properties but summarizes, totally or partially, the information present in the inputs. This would correspond to a knowledge-informed dimensionality-reduction. Even in the latter case, the scientific value of the model as a tool for understanding is not necessarily questioned. The analyses presented below are simply intended to supplement the understanding of models and how they process information.

### Emergence of information in artifical examples

These questions can be illustrated using a very simple artificial model represented in Figure \@ref(fig:model-simulation). On the one hand there are two latent biological variables called *Proliferation (P)* and *Apoptosis (A)* resulting in our biological groud truth, *Growth*. On the other hand, the modeler has access to three different random variables $N_1$, $N_2$ and $N_3$ respectively associated with the sign of *P*, the absolute value of *P* and the value of *A*. Two mechanistic models are defined, one linear (with its output $O_{linear}$) and one non-linear (with its output $O_{non-linear}$). We note that the two outputs are sufficiently well defined to be correlated with *Growth* but only the non-linear model makes use of $N_2$ by multiplying it with $N_2$.

\begin{figure}

{\centering \includegraphics[width=0.8\linewidth]{fig/model-simulation} 

}

\caption[Definition of two distinct mechanistic models]{(ref:box-mech-caption)}(\#fig:model-simulation)
\end{figure}
(ref:model-simulation-caption) **Definition of two distinct mechanistic models.** Green variables are true latent phenomena. Brown variables are values accessible to the modeler ($N_i$) and the outputs extracted from the models ($O$) Statistical analysis in Figure \@ref(fig:R2-artificial).

The ability of models to use inputs to create or summarize information through outputs will be studied using the explained variation metric $R^2$. If a linear model is defined as $y_i=\beta_0+\beta_1x_i+e_i$, linear coefficients $\beta$ are estimated by minimizing the sum of squared differences between predicted and real values of $y$. The fitted model is written $\hat{y_i}=\hat{\beta_0}+\hat{\beta_1}x_i$ and $R^2$ also called coefficient of determination is defined as:

$$R^2=\dfrac{\sum_{i=1}^{n} (\hat{y_i}-\bar{y_i})^2}{\sum_{i=1}^{n}  (y_i-\bar{y_i})^2}$$

Therefore $R^2$ measures the proportion of variation in $y$ that is explained by the regressors. Metrics with similar (but not identical) interpretations have been defined for logistic regressions or survival analysis [@choodari2012simulation]. In the case of regressions with several variables $x_i$, it is possible to decompose $R^2$ into different components associated with each of the variables. This decomposition is carried out here by  averaging over orderings according to the method proposed by @lindeman1980introduction and applied in R code [@gromping2006relative]. The precise formulas are detailed in appendix \@ref(appendix-decomp).  
  

Here is an example of schematic reasoning that can be carried out with $R^2$ about the two models in Figure \@ref(fig:model-simulation). Using only the outputs of the models to predict *Growth*, explained variations are $R^2_{O_{non-linear}}=0.455$ and $R^2_{O_{linear}}=0.379$. The models are thus correctly defined and partly recover the biological read-out. However, the inputs to the model also have an important predictive value since $R^2_{N_1+N_2+N_3}=0.514$. How can we understand the relationship between these values? First, the model including the $N_i$ inputs and the output $O$ as regressors show different performances with $R^2_{N_1+N_2+N_3+O_{linear}}=0.514$ and $R^2_{N_1+N_2+N_3+O_{non-linear}}=0.586$. This means that the $O_{linear}$ has no added value compared to the inputs. This was expected given its definition. On the other hand, $O_{non-linear}$ has allowed to extract an emergent information which improves the global prediction when combined with the inputs. We can go further in understanding by breaking down the $R^2$. In Figure \@ref(fig:R2-artificial)A and B (left columns), $R^2$ of the inputs' models are decomposed to show that $N_1$ and $N_3$ contribute most to the prediction in a linear model. By using the same strategies for decomposing the $R_2$ and calculating the incremental R2, it is also possible to decompose the $R^2$ of $O$ according to its origin: its component $N_1$ ($0.22$ in Figure \@ref(fig:R2-artificial)A) is the proportion of $R^2$ that is also explained by $N_1$, so it can be interpreted as being the part of the value of $N_1$ captured by $O$. In the non-linear case, we can see in the decomposition that $O$ also has a created component ($0.07$), it is the non-linear component that is not shared with any of the inputs.

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{07-Evaluation_files/figure-latex/R2-artificial-1} 

}

\caption[Decomposition of $R^2$ for inputs and output of example models]{(ref:R2-artificial-caption)}(\#fig:R2-artificial)
\end{figure}
(ref:R2-artificial-caption) **Decomposition of $R^2$ for inputs and output of example models.** (A) Results for the non-linear model inputs and output $O_{non-linear}$ as defined in Figure \@ref(fig:model-simulation). (B) Same with the linear model.  
  

In conclusion, if these two models generate meaningful outputs that are correlated with the biological read-out *Growth*, the analysis of their information processing classifies them into two different categories outlined in the previous sub-section. The linear model summarizes some of the information present in the inputs, without creating any. It can be likened to a relevant dimensionality reduction. The output of the non-linear model also fails to avoid some information losses, but at the same time it extracts new non-linear information. Thus, in combination with the inputs, it provides added value measured by the increase in total $R^2$.

## Reanalysis of mechanistic models of cancer

Using the tools presented above, it is possible to deepen the analysis of some mechanistic models already presented in this thesis.

### ODE model of JNK pathway by @fey2015signaling


\@ref(prognostic)

Survival --> Royston and [@choodari2012simulation]

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{fig/fey} 

}

\caption[Schematic example of logical and ODE modeling around MAPK signaling]{(ref:fey-caption)}(\#fig:fey)
\end{figure}
(ref:fey-caption) **Mechanistic modeling of JNK pathway and survival of neuroblastima patients, as described by @fey2015signaling.** (A) Schematic representation, as a process description, for the ODE model of JNK pathway. (B) Response curve (phosphorylated JNK) as a function of the input stimulus (Stress) and characterization of the corresponding sigmoidal function with maximal amplitude $A$, Hill exponent $H$ and activation threshold $K_{50}$. (C) Survival curves for neuroblastoma patients based on binarized $A$, $K_{50}$ and $H$; binarization thresholds having been defined based on optimization screening on calibration cohort.  

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{07-Evaluation_files/figure-latex/R2-Fey-1} 

}

\caption[Decomposition of $R^2$ for inputs and output for ODE model in @fey2015signaling]{(ref:R2-Fey-caption)}(\#fig:R2-Fey)
\end{figure}
(ref:R2-artificial-caption) **Decomposition of $R^2$ for inputs and output for ODE model in @fey2015signaling.** (A) Results for the non-linear model inputs and output $O_{non-linear}$ as defined in Figure \@ref(fig:model-simulation). (B) Same with the linear model.  

### Personalized logical models

#### Survival of breast cancer patients in METABRIC cohort

Mention AIC

[@kirk2013model]

#### Sensitivity to BRAF inhibition in melanoma and colorectal cancers
