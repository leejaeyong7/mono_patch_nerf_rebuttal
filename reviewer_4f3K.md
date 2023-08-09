We thank the reviewer for taking the time to review our paper and providing constructive comments regarding our work. We appreciate how you have found our work to be "valuable" and "well motivated". 
We acknowledge your concerns and questions and provide the clarifications in the response below.


**Question regarding the foreground fattening**

Foreground fattening in patch-based MVS is largely caused by plane-based propagation of depth candidates and a patch-wise planar assumption in computing photometric scores. Our method does not suffer from foreground fattening because we do not make planar assumptions (current depth estimates are projected into other views to compute photometric scores), and the rendering loss discourages such artifacts. As suggested, Figure 2 in the rebuttal document shows the alignment of RGB image and the depth images. The image and the depth are aligned precisely, indicating that our method does not suffer from the foreground fattening.

**Using learned similarity metrics**

We agree that the use of learned similarity metrics are quite common, and have been used widely. However, in our experience, we find such learned losses to provide a marginal benefit especially in the challenging sparse view setups like ETH3D dataset. In the ETH3D benchmark, the best performing methods still use NCC for the photometric score. 

**Occlusion awareness in the loss function**

Our novel view patch sampling is occlusion aware, as we explicitly mask pixels that are occluded when computing NCC and SSIM. The masking is given by rendering a novel view patch, unprojecting it into the world space using the rendered depth, projecting back to the training camera view, and comparing the angle of projection and the original patch rays with the threshold. We let Figure 1 in the rebuttal document to visualize this process.
We will clarify this in revision.

We thank the reviewer for the suggestion in the novel multi-patch synthesis; we find it interesting and will try it on our next project.

**Why not use MVS as a supervision?**

As detailed in our main response, we believe that NeRF has long-term potential to surpass traditional MVS, due to its ability to optimize over more camera/scene properties, regularize, and incorporate monocular cues more easily.  Incorporating MVS estimates into NeRF could improve results in the short-term, but is likely not the best long-term solution due to complexity and computational cost. Since MVS is not fully reliable, it is also non-trivial to incorporate it in a way that retains the more accurate portions but replaces the inaccurate estimates.


**Comparison to Neural Rerendering in the Wild**

While our approach is similar to the [Neural Rerendering in the wild](https://arxiv.org/pdf/1904.04290.pdf) in that we are both solving for large scale complex scene reconstruction, we aim to recover accurate geometry unlike [Neural Rerendering in the wild](https://arxiv.org/pdf/1904.04290.pdf) which targets appearance modeling.