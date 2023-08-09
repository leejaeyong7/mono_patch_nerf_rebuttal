We thank the reviewer for taking the time to review our paper and providing constructive comments regarding our work.  We appreciate how you have found our work to be "technically sound" and "non-trivial". 
We acknowledge your concerns and questions and provide the clarifications in the response below.

**Performance gap versus the MVS approaches**

Please see the discussion in the overall rebuttal. 

**Speed of NeRF based models is slower compared to MVS systems**

As stated in the Supplementary material, our model trains within 2.25 hours per scene, which is slower than the MVS methods, but faster than most of the existing NeRF methods. 
We note that although the MVS methods are faster, NeRF-based approaches provide other benefits like novel view synthesis, and the speed can likely be improved

**Incorporating Semantic Segmentation**

Thank you for the suggestion.  We tried incorporating semantic segmentation, but found it gave only a marginal benefit with much larger memory and computation time. Future work might make better use of semantic segmentation, e.g. by using it to inform material models for whether a surface is likely to be glossy or transparent.

**Handling of complex lighting effects is lacking**

We believe that radiance field representation partly resolves the complex lighting effects, yet we agree that incorporation of complex lighting effects as additional priors may improve our system further.

**Handling of floaters and background collapse**

Our patch-wise smoothness terms applied in depth and normal loss enforces neighborhood continuity, partly resolves the background collapse (similar to how it is done in the non-local priors for volumetric reconstruction paper).
For instance, in Figure 4, compared to our base configuration w/o mono-patch prior termed as "None", we have a smooth surface that avoids local optimum on texture-less surfaces on our ablation settings with monocular geometry distillation only "Mono". 
Moreover, we believe density restriction partly resolves both floaters and background collapse.
In density restriction, we prune out the search space of density which will remove all the floaters that do not belong to the restricted volume. Furthermore, the restriction enforces background collapses to happen within narrower range, potentially alleviating the problem as shown in Figure 3.

**Reliability and robustness of the priors**

Reliance on sparse reconstructions is common in multiview approaches, e.g. to set the range of depth per view, or to initialize depth estimates.  Typically, this does not create problems, as long as the information is used conservatively. Our restriction is conservative, as shown in Fig 3, and will be robust to noise, as that will tend to increase the area of plausible density. If the sparse reconstruction is consistently off in some way, that likely indicates a significant misregistration from which existing MVS methods would not recover.

**Computational cost of additional loss functions**

We find novel view patch sampling increases the optimization time by around an additional hour (due to the additional rendering time for the novel view patches). 
Other loss functions do not directly influence the optimization time, but have marginal influence in the convergence time.
