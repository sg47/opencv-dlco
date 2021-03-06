**OpenCV DLCO (Descriptor Learning Using Convex Optimisation)**


* Workflow for the DLCO training process:

(01) *01-export.sh* will convert M. Brown [1] image patch dataset to local
HDF5 layout. See `dataset` folder for preparation and details.

(02) *02-genpoolregs.sh* will generate `filter.h5` containing the layout
of rings, ring parameters & pooling-region gaussians.

(03) *03-compdist.sh* will precompute initial high dimension distances given
descriptors of patch-pairs constructed by `filter.h5` full layout.

(04) *04-prlearn.sh* will learn low dimensional efficient pool-regions over
the `filter.h5` using precomputed distances. This may take very long time
even using GPU, up to ~1 week given actual 256 combinations of mu and gamma
regularization parameters over the three datasets. Results and logs will be
stored within `pr-learn` folder.

(05) *05-prstats.sh* will compute and log performance statistics for all
learnt pool-region filters like: false positive rate, area under curve and
dimensionality.

(06) *06-pr-top.sh* will display top 10 performing learnt pooling-region
given false positive rate and dimensionality criteria. Final selection is
done by hand.

(07) *07-compunproj.sh* will precompute lower dimensional distances given
descriptors of patch-pairs constructed by `filter.h5` layout and stripped
down by best learnt pool-region filter. Used pooling-regions are manually
selected at step (6) and hardcoded in this very script.

(08) *08-pjlearn.sh* will learn low rank projection matrices over the
unprojected distances from step (07). This may take very long time even
using GPU, up to ~1 week given actual 16 combinations of mu and gamma
regularization parameters over each 3x3 distances datasets. Results and
logs will be stored within `pj-learn` folder.

-----------------------------------------------------------------------------

[1] "Learning Local Image Descriptors Data", Matthew Brown
URL: http://www.cs.ubc.ca/~mbrown/patchdata/patchdata.html
