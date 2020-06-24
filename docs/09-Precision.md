
# Causal inference for precision medicine

\epigraph{"Felix qui potuit rerum cognoscere causas."}{Virgil (Georgics, 29 BC)}




\initial{T}hroughout this manuscript, we first described the complexity of cancer mechanisms, through the diversity of genetic alterations or non-linear signaling pathways. This complexity naturally led to the choice of systemic modelling approaches and in particular mechanistic models whose explicit nature facilitates the study of the effects of new molecular perturbations such as treatments. The simple study of the response to BRAF inhibitors has thus required the consideration of many other genes and pathways.




  
This chapter proposes to take the complexity a step further by considering different treatments. The diversity of patients' molecular profiles suggests that the best treatment is not necessarily the same for all patients: this is what is known as precision medicine. This is already a clinical reality in oncology that could be reinforced in the future by the emergence of new computational models of cancer, whether mechanistic or not. How then can we assess the relevance of these models in their ability to guide patient treatment?

\BeginKnitrBlock{summarybox}<div class="summarybox">
#### Scientific content {-}

This chapter presents an extension of the causal inference framework to quantify the value of precision medicine strategies. This work is currently under revision and is available as a pre-print @beal2020causal.
</div>\EndKnitrBlock{summarybox}

## Precision medicine in oncology



### Starting from pre-clinical data: patient-derived xenografts

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{09-Precision_files/figure-latex/PDX-dense-1} 

}

\caption[Analysis on observed data without confounder]{(ref:PDX-dense-caption)}(\#fig:PDX-dense)
\end{figure}
(ref:PDX-dense-caption) **Analysis on observed data without confounder.** (A) Directed acyclic graphs

### Clinical trials and treatment algorithms

Many biomarkers, associated clinical trials and treatment algorithm
[@de2015pragmatic]

\begin{figure}

{\centering \includegraphics[width=0.8\linewidth]{fig/SHIVA_algo} 

}

\caption[An example of a precision medicine treatment algorithm: the SHIVA clinical trial]{(ref:SHIVA-caption)}(\#fig:SHIVA)
\end{figure}
(ref:SHIVA-caption) **An example of a precision medicine treatment algorithm: the SHIVA clinical trial.** Specific molecular alterations and their associated treatments, as proposed in the SHIVA clinical trial by @le2015molecularly.


### Models

Mechanistic models of cancer pathways are particularly well suited to study response to treatment. Their explicit representation of genes and proteins makes it possible to simulate the effect of different therapeutic interventions. On the basis of this observation, it is possible to imagine the following situation 




\begin{figure}

{\centering \href{http://jonasbeal.shinyapps.io/application_causal_pm/}{\includegraphics[width=0.9\linewidth]{09-Precision_files/figure-latex/Shiny-1} }

}

\caption[Bimodality criteria and their combinations]{(ref:Shiny-caption)}(\#fig:Shiny)
\end{figure}
(ref:Shiny-caption) **Schematic extension of PROFILE-personalized logical models to drug investigation.**
