# crct_med
Crct_med is a function to perform mediation analysis in cluster randomised controlled trials. It can also handle observational data, but the user should pay close attention to confounders and specifying those correctly. The function estimates direct and indirect effects and can allow for cluster level interference and unmeasured cluster level confounding which are assumptions that are usually required for unbiased estimates. Latent cluster level mediator and covariate adjustment can also be handled. 
Clustered bootstrap percentile confidence intervals are calculated for the mediation effects that are produced. A sensitivity analysis is also conducted in the scenario where no unmeasured upper-level confounding is assumed, and interference is present to test the robustness of the provided estimate to residual correlation between the mediator and the outcome at the higher level. 

# Function description
The function first prepares the data by standardising where requested and then decomposing the mediator and outcome variables into cluster-level averages and individual deviation terms. A structural equation model is then constructed and estimated using lavaan.
Depending on the analysis option and the assumptions that the user makes regarding interference and unmeasured upper level confounding, the function can estimate:
+	The action effect;
+	The conceptual effect;
+	The direct effect;
+	The interference effect;
+	The natural contextual indirect effect (NCIE); in the presence of interference the mediated effect via other cluster members mediator
+	The natural within indirect effect (NWIE); mediated effect via individual mediator
+	The between indirect effect (BIE);
+	The combined indirect and direct effect;
+	The overall effect (OE) or average treatment effect (ATE).

Confidence intervals and standard errors for all effects are calculated using a cluster bootstrap procedure, a seed is set in order for these results to be reproducible within the session. Clusters are sampled with replacement, and duplicated clusters are assigned unique cluster identifiers before refitting the model. Percentile confidence intervals are then calculated and presented. 
When interference = “TRUE”, unmeasured_confounding = “FALSE”, and averages_only = “FALSE”, a sensitivity analysis is conducted over the values specified in rho_values. The sensitivity analysis examines how the NCIE changes as the assumed residual association between the cluster level mediator and outcome is varied. A line is plotted to show the value of rho required for this effect to become 0.

