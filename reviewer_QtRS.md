We thank the reviewer for taking the time to review our paper and providing constructive comments regarding our work.  We appreciate how you have found our work to be "clear improvements". 
We acknowledge your concerns and questions and provide the clarifications in the response below.

**Computation of Patch-based NCC/SSIM is confusing**
We refer to Figure 1 in the rebuttal document to visualize how the patch-based score is computed between a training view and a nearby novel virtual view. 3D points are obtained by rendering the depth in the training view and unprojecting.  Then RGB values for rays through these points are obtained in the virtual view by rendering from the NeRF model.  The rendered RGB in the virtual view are compared to known RGB in the training view. Inaccuracies in the model could cause the rendered RGB to differ from the original.  Effects of occlusion are mitigated by ignoring a pixel if the angle is large from the training view origin to the corresponding unprojected training and virtual view depths. We will clarify this in revision.


**On per-image versus per-patch alignment of monocular depth**
Our key intuition is that in the monocular depths, the local ordinals are better preserved than global ordinals. 
For instance, comparing the depth at the left top part of the image, versus the right top part of the image (i.e, global ordinal), will be more challenging, than comparing two consecutive pixels (which is essentially solvable by surface normal). 
Density restriction via empty space pruning thus requires a large range (20% of the depth) since the per-image scale-shift is not as accurate. 


**Benefits of using NeRF over photogrammetry in sparse-view setting**
As described in the main response, NeRF can more easily incorporate information such as monocular cues and optimize over scene models, camera models, and priors. Regularizations on 3D surfaces, such as total variation prior, can be explicitly encoded, where priors in traditional MVS are often applied per view and more implicit, e.g. through PatchMatch propagation strategies.


**Incorporation of monocular priors to photogrammetry pipelines**
We believe that the monocular priors can be incorporated into photogrammetry pipelines. For instance, monocular surface normals can be used to guide the patch orientation in PatchMatch based depth / normal search. Similarly, monocular depths can be used to filter out search space in PatchMatch MVS or as an initialization (after fitting scale-shift) in iterative MVS pipelines. 

However, we find the monocular priors to be better incorporated in NeRF. For instance, analytical gradients of density can be regularized with the surface normal maps, which are not easy to incorporate in MVS models. For more response regarding the comparison to MVS, please refer to the corresponding section main response.


