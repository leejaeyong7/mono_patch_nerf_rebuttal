We thank the reviewer for taking the time to review our paper and providing constructive comments regarding our work.  
We appreciate how you have provided a lot of potential improvements of our system. 
We acknowledge your concerns and questions and provide the clarifications in the response below.


**The constraint of photometric consistency is not new**

We agree that photometric consistency is a core principle of multiview estimation, and, as such, has been used in both traditional MVS and NeRF. However, different from Self-Calibrating NeRF, our goal is not to make the training images more consistent but to regularize the geometry. Different from traditional MVS, our method computes photometric scores between virtual views and training views, providing more robustness when views are sparse.  Different from DietNeRF and RegNeRF, we use simpler traditional MVS photoconsistency measures rather than deep network features or GAN-based likelihood, which reduces computation, and, as our results show, leads to more accurate geometric models.

**I think the writing could be improved… How are the angle difference computed, is there a threshold and what is it exactly?**

Thank you for these suggestions.  We will revise accordingly.  Currently, some of these details are included in the supplementary material, e.g. the method to compute the angle and threshold of 10 degrees is specified in lines 4-7 of supplementary.  

**The paper demonstrates a few tricks that could make NeRF work better, some of which have been explored before with minor modification, e.g. the relative depth and normal losses.**

As indicated by Reviewer eybE (“design choice is non-trivial…”), while the high-level ideas of incorporating monocular cues, patch-based constraints, and regularization based on virtual views are not entirely new, adapting them for effective geometric modeling in NeRF is non-trivial and lead to large gains in accuracy of geometry. While the degree of modification required is somewhat subjective, the improvements due to our contributions is well validated. 

**The figures could be made better. For example, I couldn't see directly that 'ours' is better than other methods by comparing it with GT.**

We are unclear which figure the reviewer is referring to. When viewed on the screen, we believe the differences in Figure 5 are clear.  Consider the stairs and lamppost.  For our method, the normals are more smooth and accurate, depth is more complete, and the generated point cloud (“Geometry”) is less noisy, compared to FreeNeRF and RegNeRF, and much more complete compared to MonoSDF. This might be less clear in a grayscale print-out.   


**It would be better to evaluate the method on other MVS datasets too, not only ETH3D**

We note that we evaluate our method on other MVS dataset, Tanks and Temples, in Table 3 and Figure 6 in the main text.  Regarding the comparison of the Tanks and Temples with other MVS models, we provide qualitative results on the subset of the Tanks and Temples advanced sets used in the MonoSDF paper in Figure 1, 2 of the supplementary material, and provide Table 1 in the rebuttal document.


**In Section 3.2, where does the depth come from? …Why is it important to handle the issue of scale and shift?**

The depth referenced in Section 3.2 is derived from the monocular depth prediction network (Omnidata [4]), following the prior work [19, 6, 32]. This is distinct from the ground truth depth map, given that the monocular depths are not on the same scale or shift as the perfect depth. Since the monocular depth is predicted for individual views, these predictions are not guaranteed to have consistent scales. As a result, when the model is trained by distilling these inconsistent scales, it can result in unaligned geometry. Therefore, addressing the issues of scale and shift is necessary to solve the scaling problem. Once the scale and shift issues are resolved, local depth values are translated into patches, which can improve geometry. 

We additionally point to the response to the reviewer QtRS, *On per-image versus per-patch alignment of monocular depth* for additional details on how solving scale and shift per patch can help.
