# Human Feedback!

Do you really believe the changes in bikes against temperature slopes over months? I didn't understand why the slope doesn't vary smoothly.



# Feedback: bike sharing regression exercise

Excellent work. Your numbers match the model answer exactly, and your write-up is a model of how to report regressions. Every estimate has its 95% CI, $t$, degrees of freedom, and $p$ value. You also put the "fewer" estimates the right way round: "87.5 fewer rentals, 95% CI [61.1, 113.9]".

The other things that stand out:

* A short methods paragraph before the results, so the reader knows exactly what was done
* Table 1 puts all three models side by side, which makes the comparison in questions 8 to 12 easy to see
* Your explanation of why the wind estimate shrinks is concrete: each extra mph went with a temperature 0.26 degrees C lower, so the wind only model was picking up part of the temperature effect
* You tested the temperature $\times$ month interaction, $F(11, 707)=7.38$, rather than just looking at the monthly slopes one at a time
* As in week 1, your write-up knits from its own `.Rmd`, so nothing is retyped. That is the standard to aim for

## Things to work on

**Say how you converted the units.** "Converted back from their normalised values" is fine, but give the conversions you used (for example, temperature $\times$ 47 $-$ 8, wind speed $\times$ 67, treating 67 as mph). Other students treated 67 as km/h and got quite different wind slopes, so it matters.

**Take your discussion one step further.** You rightly point out that rentals grew a lot from 2011 to 2012, and that the models leave this out. You could add `yr` to the model and see whether the temperature estimate changes. And the negative slopes in June and July suggest the relationship with temperature is curved, so you could try a quadratic term. Neither is required here, but both would follow naturally from what you wrote.
