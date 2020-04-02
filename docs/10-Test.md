# Test part {#test}

This is a test

## Abc

Bla bla ref @MBMH19 and [@MBMH19].

But in @BMTBC19 we have the Figure \@ref(fig:nice-fig) as referenced in Chapter \@ref(test)


```r
par(mar = c(4, 4, .1, .1))
plot(pressure, type = 'b', pch = 19)
```

\begin{figure}

{\centering \includegraphics[width=0.8\linewidth]{10-Test_files/figure-latex/nice-fig-1} 

}

\caption{Here is a nice figure!}(\#fig:nice-fig)
\end{figure}

And an external figure \@ref(fig:test)

\begin{figure}

{\centering \includegraphics[width=0.45\linewidth]{cover/pictures/back-bg} 

}

\caption{Example pic}(\#fig:test)
\end{figure}
