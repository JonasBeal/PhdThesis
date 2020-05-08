# Test part {#test}

This is a test

## Abc

Bla bla ref @MBMH19 and [@MBMH19].

But in @BMTBC19 we have the Figure \@ref(fig:nice-fig) as referenced in Chapter \@ref(test)


```r
par(mar = c(4, 4, .1, .1))
plot(pressure, type = 'b', pch = 19)
```

<div class="figure" style="text-align: center">
<img src="10-Test_files/figure-html/nice-fig-1.png" alt="Here is a nice figure!" width="80%" />
<p class="caption">(\#fig:nice-fig)Here is a nice figure!</p>
</div>

And an external figure \@ref(fig:test)

<div class="figure" style="text-align: center">
<img src="cover/pictures/back-bg.png" alt="Example pic" width="45%" />
<p class="caption">(\#fig:test)Example pic</p>
</div>

