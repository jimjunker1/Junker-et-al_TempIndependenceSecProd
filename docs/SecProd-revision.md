---
title: "SecProd revision"
author: "James R Junker"
date: "01 July, 2020"
knit: (function(inputFile, encoding) { 
      out_dir <- 'C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs';
      rmarkdown::render(inputFile,
                        encoding=encoding, 
                        output_file=file.path(out_dir, 'SecProd-revision.html')) })
output: 
  html_document:
      keep_md: true
      toc: true
      toc_float: true
      toc_depth: 3
      numbered_sections: true
---


# Primer

The main thrust of the paper stands on these equations (which I know y'all are familiar):
If 2$^\circ$ Production is the product of population biomass and biomass turnover (P:B)

$$2^\circ Production= B * P:B$$
And MTE predicts biomass as:
$$ B = [R] M^{0.25}*e^{E_a/kT}$$
and biomass turnover as:
$$ P:B = M^{-0.25}*e^{-E_a/kT}$$
This leads to the prediction that:
$$2^\circ Production=[R]$$
where, *[R]* is a generic resource term. We assume this to mean resource supply (energy) and that 2$^\circ$ production scales linearly with resource supply. As such, we should be able to account for the vast majority of the variation in 2$^\circ$ production by accounting for resource supply. Further, we expect no systematic variation associated with temperature at either timescale. A true measure of resource supply is hard to nail down, ideally it would be resource production, rather than a standing stock. Second, it would also include only production that is available to consumers. This is generally unreasonable to measure at the level of the ecosystem for all consumers, so we make some simplifying assumptions.

# Review outline

The most substantive comments revolved around the use of chlorophyll *a* as a proxy, which would apply to both timescales. The reviewers seemed okay with mean chlorophyll *a* at the annual scale. It has good explanatory power and 2$^\circ$ production scales with an exponent of ~1. This fits well with the model that *P* ~ *[R]* linearly. This suggests that integrating the monthly chlorophyll *a* biomass measurements captures the differences in resource production across streams at the annual scale. This is also supported if we use published models to estimate [GPP](#morin_annual). 

The main criticism from reviews was reconciling the apparent temperature dependence of secondary production at seasonal time scales. Here, the differences in resource turnover due to seasonal temperatures and light availability make chlorophyll *a* poor proxy for resource production. Since we do not have production across the gradient, we make a weak inference in the paper that the temperature dependence of secondary production falls within the range probable for the temperature dependence of basal resource production. This leaves the reader to question the results and weakens the conclusions in the title and abstract that secondary production is temperature independent on seasonal and annual timescales. This is likely a problem of my explanation lacking clarity, but it is also not straightforward as presented because reviewers were expecting us to show a slope of zero with temperature at both timescales. 

Given the data we have, I think there are a few ways forward that might make it easier to grasp. These include:

1) [Comparing empirical whole-ecosystem primary production measurements from st7 and oh2](#warming_emp)

2) [Estimating within-stream temp. dependence from st7 & oh2 and corrected estimate across warming](#Ea_corr)

3) [Building a predictive GPP model from st7 and oh2 and applying across the gradient](#warming_pred)

4) [Using a GPP model in Morin 1999 with chlorophyll and temperature](#morin_pred)

Each have their shortcomings, which I discuss a bit below. But generally some of these analyses suggest something different than what we argue in the paper. I am still trying to wrap my head around how to reconcile some of it. 

## Empirical warming: GPP ~ 2$^\circ$ Production {#warming_emp}

This approach is an ideal one, it is a flux, so we are comparing a flux to a flux. But it does have its shortcomings. Whole system GPP captures primary producer compartments that are not accessible to consumers. So the distribution of biomass between accessible/non-accessible producers might alter how well this captures true resource supply.

### Main Take-aways
- GPP scales with 2$^\circ$ Production, but there are important deviations
- Temperature is associated with these deviations
- An apparent temperature dependence of 2$^\circ$ Production even after accounting for GPP

--

Here are the temporal patterns between GPP, chla, and 2$^\circ$ production and their bivariate relationships. Take note GPP is in grams and is 2$^\circ$ production milligrams in the first figure of patterns over time.

![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/warming-1.png)<!-- -->![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/warming-2.png)<!-- -->

There is a hint of evidence that Secondary production scales linearly with GPP, albeit these patterns are messy, as to be expected with real data. Some of these deviations at low measured GPP coincide with higher than expected 2$^\circ$ Production, but this also coincides with relatively high chlorophyll *a* biomass. Also, chlorophyll a has a messy relationship with GPP which again is expected considering the different biological components captured and wide environmental variability. But I continue with the test that P ~ [R] linearly. Below are some model attributes. And residual variation around GPP ~ 2$^\circ$ Production. For further details see [Model Output](#models). 



AIC of GPP ~ 2$^\circ$ Production =73.77

AIC of GPP + temp ~ 2$^\circ$ Production = 63.42

AIC of GPP * temp ~ 2$^\circ$ Production = 63.77

Selecting among these models suggests that temperature does add information to the model, but temperature doesn't have any interactive effect with GPP. 



![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/warming v gpp-1.png)<!-- -->

Some of the residual variation suggests unaccounted for temperature dependence of 1.3 eV. This should in theory be 0 eV.


```
##                  2.5 %    97.5 %
## .sig01       0.0000000 0.6145809
## .sigma       0.6320731 1.1479167
## (Intercept)  0.1919256 3.4379792
## tempkt_stand 0.1716663 2.5034944
```

## Modeling GPP in st7 & oh2

This option is another way to capture the seasonal dynamics of resource production and compare estimated flux with flux and it has the advantage of being applicable across the temperature gradient. It assumes we can apply the temperature and light dependencies in st7 and oh2 across the whole gradient. But it looks like we can do a decent job of capturing the patterns of GPP in st7 and oh2 with temperature and light. I am hesistant to not include a model with chlorophyll *a*, but it appears to not do much. Further, when chlorophyll is included, the estimated GPP across the gradient is unrealistically high in Hver, peaking at ~1000 g C m^{-2} d^{-1}.

![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/gpp model-1.png)<!-- -->![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/gpp model-2.png)<!-- -->

This model suggests the temperature dependence of GPP, after accounting for light is ~1.7, right in line if not a bit steeper, than the estimated activation energy of secondary production from the mixed-model presented in the paper (1.3 eV). 

I had two ideas about how to go from here:

## Correctin within-stream Ea_{2P} by estimated within-stream Ea_{GPP} {#Ea_corr}

In this case, we model the temperature dependence of GPP from st7 & oh2. We then correct the slope of 2$^\circ$ production by this value as a resource-corrected temperature dependence.

### Main Takeaways
- This supports temperature independence of secondary production 
- It allows us to clearly show a zero slope for seasonal 2P

--

Here I simulated variability around daily GPP by randomly generating some values based on assumed posterior distributions fit to the estimated GPP percentiles

Then I estimated mean daily interval GPP for simulated daily GPP series and fit the same linear model above to estimate variability in the within-stream temperature dependence of GPP. These extracted coefficients were then used to 'correct' the estimated temperature dependence of secondary production within all streams (Ea[GPP] - Ea[2P]). This leaves the following estimates of temperature depdendence of secondary production after we account for resource turnover. 

![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/EA correcting-1.png)<!-- -->

Here is an evolving look at Resource-corrected 2P ~ temperature, this essentially shows the estimated fixed effects of temperature 

![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/temp Ea corr-1.png)<!-- -->

## Predictive model from Warming streams {#warming_pred}

Another possible way is to extend this model to the whole gradient, giving:

![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/gradient warming model-1.png)<!-- -->![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/gradient warming model-2.png)<!-- -->![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/gradient warming model-3.png)<!-- -->![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/gradient warming model-4.png)<!-- -->

Here, if we test that GPP ~ 2$^\circ$ Production linearly, we see that we estimate a slightly sublinear scaling of 2$^\circ$ Production with GPP 


```
## Linear mixed model fit by REML ['lmerMod']
## Formula: log(prod_d_new/1000) ~ log(EstGPP_gCm2d_warming) + (1 | SITE)
##    Data: warming_intdf
## 
## REML criterion at convergence: 170.8
## 
## Scaled residuals: 
##      Min       1Q   Median       3Q      Max 
## -2.37508 -0.62540  0.07367  0.73529  2.04967 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  SITE     (Intercept) 1.1231   1.060   
##  Residual             0.7191   0.848   
## Number of obs: 61, groups:  SITE, 6
## 
## Fixed effects:
##                           Estimate Std. Error t value
## (Intercept)               -5.14106    0.44699 -11.501
## log(EstGPP_gCm2d_warming)  0.58294    0.08601   6.777
## 
## Correlation of Fixed Effects:
##             (Intr)
## l(EGPP_C2_) -0.057
```

However, we find that after we acccount for resources, we cannot detect any systematic relationship with temperature across streams.

![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/warming_resids-1.png)<!-- -->

But there does seem to be a pattern within streams. 

![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/within centered-1.png)<!-- -->

If we run a test on this to see how different models do. We see that there is some information added if we add temperature.

AIC of GPP ~ 2$^\circ$ Production:178.75

AIC of GPP + temp ~ 2$^\circ$ Production = 171.64

AIC of GPP * temp ~ 2$^\circ$ Production = 175.89




```
## Linear mixed model fit by REML ['lmerMod']
## Formula: .resid ~ tempkt_center + (1 | SITE)
##    Data: a
## 
## REML criterion at convergence: 146.1
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.4428 -0.6374  0.1044  0.6766  2.5209 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  SITE     (Intercept) 0.0000   0.0000  
##  Residual             0.6259   0.7911  
## Number of obs: 61, groups:  SITE, 6
## 
## Fixed effects:
##               Estimate Std. Error t value
## (Intercept)   -0.02543    0.10219  -0.249
## tempkt_center  0.49263    0.26231   1.878
## 
## Correlation of Fixed Effects:
##             (Intr)
## tempkt_cntr -0.132
## convergence code: 0
## boundary (singular) fit: see ?isSingular
```

```
##                     2.5 %    97.5 %
## .sig01         0.00000000 0.2475402
## .sigma         0.65803081 0.9395385
## (Intercept)   -0.22535724 0.1747241
## tempkt_center -0.02105204 1.0063055
```

## Estimated GPP with Morin {#morin_pred}

The Morin model predicts daily GPP with just temperature and chlorophyll *a*. It has the advantage of including chlorophyll, resource data we have across the entire gradient. I am a little skeptical about that lack of inclusion of light availability. It seems that because the model is built across latitudes, the temperature coefficients (dependence) would reflect the covariance in temp & light that exists across latitude. I wonder if this has the potential to over estimate GPP in the winter in warmer streams here because the decoupling of the temp-light covariance. Alex suggested this might not be an issue. Further, this is just one of many variables that are not accounted for in such a simple model. So here it goes: 

![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/GPP plot-1.png)<!-- -->![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/GPP plot-2.png)<!-- -->

There is some discrepancy between GPP measured and GPP modeled with Morin, as to be expected. We overestimate in the winter (light?) and underestimate some parts of the summer in one stream (Other producers more important?). 

![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/morin-warming-1.png)<!-- -->

These differences show some clear bias with both temperature and light

![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/Morin bias-1.png)<!-- -->![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/Morin bias-2.png)<!-- -->

And these discrepancies might be really important. 

![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/Morin -1.png)<!-- -->


![](C:/Users/james/Documents/Projects/Junker-et-al_TempIndependenceSecProd/docs/SecProd-revision_files/figure-html/seasonal-1.png)<!-- -->

This suggests an unaccounted for temperature-dependence of:


```
## Linear mixed model fit by REML ['lmerMod']
## Formula: .resid ~ tempkt_center + (1 | SITE)
##    Data: b
## 
## REML criterion at convergence: 145.1
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.1900 -0.5859  0.2377  0.8430  1.6863 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  SITE     (Intercept) 0.000    0.0000  
##  Residual             0.615    0.7842  
## Number of obs: 61, groups:  SITE, 6
## 
## Fixed effects:
##               Estimate Std. Error t value
## (Intercept)    -0.1008     0.1013  -0.995
## tempkt_center   1.9536     0.2600   7.513
## 
## Correlation of Fixed Effects:
##             (Intr)
## tempkt_cntr -0.132
## convergence code: 0
## boundary (singular) fit: see ?isSingular
```

```
##                    2.5 %     97.5 %
## .sig01         0.0000000 0.33414575
## .sigma         0.6522922 0.93134488
## (Intercept)   -0.2992200 0.09754863
## tempkt_center  1.4444454 2.46284349
```

<!-- ## Secondary production model selection -->

<!-- ```{r model selection, echo = FALSE, warning=FALSE, message=FALSE} -->

<!-- gpp_sum_narm = gpp_sum %>% select(SITE, prod_mg_m_y, tempkt_stand, gpp_ann_Morin, gpp_ann_warming) %>% na.omit -->
<!-- full.model = lm(log(prod_mg_m_y/1000)~log(gpp_ann_Morin)*tempkt_stand, data = gpp_sum_narm, na.action = 'na.fail') -->
<!-- MuMIn::dredge(full.model, extra = c("R^2", F = function(x) summary(x)$fstatistic[[1]])) -->

<!-- full.model = lm(log(prod_mg_m_y/1000)~log(gpp_ann_warming)*tempkt_stand, data = gpp_sum_narm, na.action = 'na.fail') -->
<!-- MuMIn::dredge(full.model, extra = c("R^2", F = function(x) summary(x)$fstatistic[[1]])) -->

<!-- ``` -->

<!-- ## GPP ~ Secondary production -->

<!-- ```{r gpp-secprod, echo = FALSE, warning=FALSE, message=FALSE} -->

<!-- ggplot(gpp_sum, aes(x = log(gpp_ann_Morin), y = log(prod_mg_m_y/1000)))+ -->
<!--   # geom_errorbar(aes(ymin = rel_2p_l95, ymax = rel_2p_u95), width = 0)+ -->
<!--   geom_smooth(method = "lm", se = FALSE) + -->
<!--   geom_abline(intercept = 0, slope = 1)+ -->
<!--   geom_point(aes(fill = SITE), shape = 21, size = 3)+ -->
<!--   scale_x_continuous(name = expression("Annual GPP (g C"~m^-2~y^-1*")"), expand = c(0.03,0), -->
<!--                      breaks = breaks_in_logprod, labels = breaks_in_prod) + -->
<!--   scale_y_continuous(name = expression("Secondary Production (mg "~m^-2~yr^-1~")"), -->
<!--                      breaks = breaks_in_logprod, labels = breaks_in_prod, expand = c(0.03,0))+ -->
<!--   scale_fill_manual(values = ocecolors[['temperature']][oce_temp_pos], labels = stream_temp_labels) + -->
<!--   theme(legend.position = c(0.1,0.7), legend.title = element_blank(), -->
<!--         legend.justification = c(1,0)) -->

<!-- # ggplot(gpp_sum, aes(x = rel_gpp_Morin, y = rel_2p, group = SITE))+ -->
<!-- #   # geom_errorbarh(aes(xmin = rel_gpp_l95, xmax = rel_gpp_u95), height = 0.0)+ -->
<!-- #   geom_errorbar(aes(ymin = rel_2p_l95, ymax = rel_2p_u95), width = 0)+ -->
<!-- #   geom_abline(intercept = 0, slope = 1)+ -->
<!-- #   geom_point(aes(fill = SITE), shape = 21, size = 3)+ -->
<!-- #   scale_x_continuous(name = expression("Relative"~Delta~"in Annual GPP [g C"~m^-2~y^-1*"]"), expand = c(0,0),  limits = c(0, 5)) + -->
<!-- #   scale_y_continuous(name = expression("Relative"~Delta~"Secondary production [g AFDM "~m^-2~y^-1*"]"), expand = c(0,0), limits = c(0, 60))+ -->
<!-- #   scale_fill_manual(values = ocecolors[['temperature']][oce_temp_pos], labels = stream_temp_labels) + -->
<!-- #   theme(legend.position = c(0.15,0.6), legend.title = element_blank(), -->
<!-- #         legend.justification = c(1,0)) -->

<!-- ggplot(gpp_sum, aes(x = log(gpp_ann_warming), y = log(prod_mg_m_y/1000)))+ -->
<!--   # geom_errorbar(aes(ymin = rel_2p_l95, ymax = rel_2p_u95), width = 0)+ -->
<!--   geom_smooth(method = "lm", se = FALSE) + -->
<!--   geom_abline(intercept = 0, slope = 1)+ -->
<!--   geom_point(aes(fill = SITE), shape = 21, size = 3)+ -->
<!--   scale_x_continuous(name = expression("Annual GPP (g C"~m^-2~y^-1*")"), expand = c(0.03,0), -->
<!--                      breaks = breaks_in_logprod, labels = breaks_in_prod) + -->
<!--   scale_y_continuous(name = expression("Secondary Production (mg "~m^-2~yr^-1~")"), -->
<!--                      breaks = breaks_in_logprod, labels = breaks_in_prod, expand = c(0.03,0))+ -->
<!--   scale_fill_manual(values = ocecolors[['temperature']][oce_temp_pos], labels = stream_temp_labels) + -->
<!--   theme(legend.position = c(0.1,0.7), legend.title = element_blank(), -->
<!--         legend.justification = c(1,0)) -->

<!-- ``` -->

## Model Output {#models}


```
## Linear mixed model fit by REML ['lmerMod']
## Formula: log(prod_d_new/1000) ~ log(EstGPP_gCm2d_med/days) + (1 | SITE)
##    Data: warming_df
## 
## REML criterion at convergence: 65.8
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -1.9659 -0.6368 -0.1013  0.8344  1.3765 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  SITE     (Intercept) 0.8288   0.9104  
##  Residual             0.9861   0.9930  
## Number of obs: 22, groups:  SITE, 2
## 
## Fixed effects:
##                            Estimate Std. Error t value
## (Intercept)                 -4.2380     0.7076  -5.990
## log(EstGPP_gCm2d_med/days)   0.4188     0.1432   2.924
## 
## Correlation of Fixed Effects:
##             (Intr)
## l(EGPP_C2_/ 0.288
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: log(prod_d_new/1000) ~ tempkt_center + (1 | SITE)
##    Data: warming_df
## 
## REML criterion at convergence: 51.7
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -1.9226 -0.6401 -0.0025  0.6362  1.7296 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  SITE     (Intercept) 0.6603   0.8126  
##  Residual             0.5617   0.7494  
## Number of obs: 22, groups:  SITE, 2
## 
## Fixed effects:
##               Estimate Std. Error t value
## (Intercept)    -4.7954     0.5964  -8.040
## tempkt_center   2.8342     0.5201   5.449
## 
## Correlation of Fixed Effects:
##             (Intr)
## tempkt_cntr 0.012
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: log(prod_d_new/1000) ~ log(EstGPP_gCm2d_med/days) + tempkt_center +  
##     (1 | SITE)
##    Data: warming_df
## 
## REML criterion at convergence: 53.4
## 
## Scaled residuals: 
##      Min       1Q   Median       3Q      Max 
## -1.87520 -0.65170 -0.04028  0.59903  1.70240 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  SITE     (Intercept) 0.6474   0.8046  
##  Residual             0.5917   0.7692  
## Number of obs: 22, groups:  SITE, 2
## 
## Fixed effects:
##                            Estimate Std. Error t value
## (Intercept)                -4.84598    0.63401  -7.643
## log(EstGPP_gCm2d_med/days) -0.03682    0.16487  -0.223
## tempkt_center               2.96591    0.79336   3.738
## 
## Correlation of Fixed Effects:
##             (Intr) l(EGPP
## l(EGPP_C2_/  0.357       
## tempkt_cntr -0.257 -0.740
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: log(prod_d_new/1000) ~ log(EstGPP_gCm2d_med/days) + tempkt_center +  
##     log(EstGPP_gCm2d_med/days):tempkt_stand + (1 | SITE)
##    Data: warming_df
## 
## REML criterion at convergence: 51.8
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -1.6736 -0.5692 -0.1363  0.6101  1.7599 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  SITE     (Intercept) 0.9556   0.9775  
##  Residual             0.5730   0.7569  
## Number of obs: 22, groups:  SITE, 2
## 
## Fixed effects:
##                                         Estimate Std. Error t value
## (Intercept)                              -4.8718     0.7445  -6.544
## log(EstGPP_gCm2d_med/days)                0.8366     0.7859   1.065
## tempkt_center                             3.0431     0.7847   3.878
## log(EstGPP_gCm2d_med/days):tempkt_stand   0.5606     0.4946   1.133
## 
## Correlation of Fixed Effects:
##               (Intr) lg(EGPP_C2_/) tmpkt_
## lg(EGPP_C2_/)  0.029                     
## tempkt_cntr   -0.217 -0.056              
## l(EGPP_C2_/): -0.034  0.978         0.098
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: log(prod_d_new/1000) ~ log(EstGPP_gCm2d_warming) + (1 | SITE)
##    Data: warming_intdf
## 
## REML criterion at convergence: 170.8
## 
## Scaled residuals: 
##      Min       1Q   Median       3Q      Max 
## -2.37508 -0.62540  0.07367  0.73529  2.04967 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  SITE     (Intercept) 1.1231   1.060   
##  Residual             0.7191   0.848   
## Number of obs: 61, groups:  SITE, 6
## 
## Fixed effects:
##                           Estimate Std. Error t value
## (Intercept)               -5.14106    0.44699 -11.501
## log(EstGPP_gCm2d_warming)  0.58294    0.08601   6.777
## 
## Correlation of Fixed Effects:
##             (Intr)
## l(EGPP_C2_) -0.057
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: log(prod_d_new/1000) ~ tempkt_center + (1 | SITE)
##    Data: warming_intdf
## 
## REML criterion at convergence: 162.9
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.0600 -0.6333  0.1225  0.8037  1.5515 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  SITE     (Intercept) 1.7860   1.3364  
##  Residual             0.6239   0.7899  
## Number of obs: 61, groups:  SITE, 6
## 
## Fixed effects:
##               Estimate Std. Error t value
## (Intercept)    -5.0828     0.5552  -9.154
## tempkt_center   2.0315     0.2655   7.650
## 
## Correlation of Fixed Effects:
##             (Intr)
## tempkt_cntr -0.027
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: log(prod_d_new/1000) ~ log(EstGPP_gCm2d_warming) + tempkt_center +  
##     (1 | SITE)
##    Data: warming_intdf
## 
## REML criterion at convergence: 161.6
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.1775 -0.6855  0.2518  0.6919  1.7826 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  SITE     (Intercept) 1.2289   1.1085  
##  Residual             0.6167   0.7853  
## Number of obs: 61, groups:  SITE, 6
## 
## Fixed effects:
##                           Estimate Std. Error t value
## (Intercept)                -5.1212     0.4644 -11.027
## log(EstGPP_gCm2d_warming)   0.2593     0.1332   1.946
## tempkt_center               1.3519     0.4358   3.102
## 
## Correlation of Fixed Effects:
##             (Intr) l(EGPP
## l(EGPP_C2_) -0.044       
## tempkt_cntr  0.016 -0.796
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: log(prod_d_new/1000) ~ log(EstGPP_gCm2d_warming) * tempkt_center +  
##     (1 | SITE)
##    Data: warming_intdf
## 
## REML criterion at convergence: 163.9
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.1730 -0.6980  0.2504  0.6808  1.8637 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  SITE     (Intercept) 1.2451   1.1159  
##  Residual             0.6264   0.7914  
## Number of obs: 61, groups:  SITE, 6
## 
## Fixed effects:
##                                         Estimate Std. Error t value
## (Intercept)                             -5.10616    0.46956 -10.874
## log(EstGPP_gCm2d_warming)                0.25531    0.13475   1.895
## tempkt_center                            1.39771    0.45894   3.046
## log(EstGPP_gCm2d_warming):tempkt_center -0.04227    0.12236  -0.345
## 
## Correlation of Fixed Effects:
##              (Intr) lg(EGPP_C2_) tmpkt_
## lg(EGPP_C2_) -0.052                    
## tempkt_cntr   0.042 -0.784             
## l(EGPP_C2_): -0.093  0.087       -0.291
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: log(prod_d_new/1000) ~ 1 + (1 | SITE)
##    Data: warming_intdf
## 
## REML criterion at convergence: 202.1
## 
## Scaled residuals: 
##      Min       1Q   Median       3Q      Max 
## -2.32174 -0.65389  0.06839  0.78683  1.76682 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  SITE     (Intercept) 1.485    1.219   
##  Residual             1.284    1.133   
## Number of obs: 61, groups:  SITE, 6
## 
## Fixed effects:
##             Estimate Std. Error t value
## (Intercept)  -4.9676     0.5185   -9.58
```
