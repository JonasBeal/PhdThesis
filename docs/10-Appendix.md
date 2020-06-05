# (APPENDIX) Appendix {-}

# About datasets

## Cell lines

## Patient-derived xenografts

## Patients

# About logical models

## Description of logical models used in this thesis

### Generic logical model of cancer pathways {#appendix-fumia}

For this thesis, a published Boolean model from [@fumia2013boolean] has been used to illustrate our PROFILE methodology. This regulatory network summarizes several key players and pathways involved in cancer mechanisms such as RTKs, PI3K/AKT, WNT/$\beta$-catenin, TGF-$\beta$/Smads, Rb, HIF-1, p53 and ATM/ATR. An input node *Acidosis* has been added, along with an output node *Proliferation* used as a readout for the activity of any of the cyclins (*CyclinA*, *CyclinB*, *CyclinD* and *CyclinE*). This slightly extended model contains 98 nodes and 254 edges and its inputs are *Acidosis*, *Nutrients*, *Growth Factors* (GFs), *Hypoxia*, *TNFalpha*, *ROS*, *PTEN*, *p14ARF*, *GLI*, *FOXO*, *APC* and *MAX*. Its outputs are *Proliferation*, *Apoptosis*, *DNA_repair*, *DNA_damage*, *VEGF*, *Lactic_acid*, *GSH*, *GLUT1* and *COX412*.

\begin{figure}

{\centering \includegraphics[width=0.8\linewidth]{fig/Fumia2013} 

}

\caption[Graphical abstract of PROFILE method to personalize logical models with omics data]{(ref:Fumia-caption)}(\#fig:Fumia)
\end{figure}
(ref:Fumia-caption) **GINSIM representation of the logical model described in @fumia2013boolean.**

# About causality

## Theoretical fraework


