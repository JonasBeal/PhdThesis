<!-- Inserting TOC, LOT and LOF -->

\renewcommand{\contentsname}{Table of contents}
\maxtocdepth{subsection}

\tableofcontents*
\addtocontents{toc}{\par\nobreak \mbox{}\hfill{\bf Page}\par\nobreak}
\newpage

<!-- List of tables -->

\listoftables
\addtocontents{lot}{\par\nobreak\textbf{{\scshape Table} \hfill Page}\par\nobreak}
\newpage

<!-- List of figures -->

\listoffigures
\addtocontents{lof}{\par\nobreak\textbf{{\scshape Figure} \hfill Page}\par\nobreak}
\newpage


\blankpage

\pagenumbering{arabic}
