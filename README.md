# The Best of Both Worlds: Combining CNNs and Geometric Constraints for Hierarchical Motion Segmentation
This is the implementation of the paper [The Best of Both Worlds: Combining CNNs andGeometric Constraints for Hierarchical Motion Segmentation (CVPR 2018)](http://vis-www.cs.umass.edu/motionSegmentation/website_CVPR18/cvpr18-bideau.pdf). The code generates motion segmentation masks segmenting multiple independently moving objects. In addition an approach to estimate the camera's rotation and translation diretion is provided.


<p align="center">
  <img height="450" src="/utils/videos/video.gif">
</p>


The code is documented and designed to be extended. If you use it in your research, please consider citing this paper (bibtex below).

## Requirements
* [VLFeat](https://www.vlfeat.org/) (the code was tested using vlfeat-0.9.20)
* miniconda
* [sharpmask](https://github.com/facebookresearch/deepmask)
* [fully conneted CRF](https://papers.nips.cc/paper/4296-efficient-inference-in-fully-connected-crfs-with-gaussian-edge-potentials.pdf). The implementation used in this work can be downloaded [here](https://github.com/AruniRC/crf-motion-seg/archive/master.zip).

## Getting Started

1) install miniconda (from your home directory on swarm2):
```
wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh
bash Miniconda2-latest-Linux-x86_64.sh
```

2) setup the conda environment:
```
conda create --prefix ~/dense-crf-conda python=2.7
source activate ~/dense-crf-conda
pip install pydensecrf     [this takes a long time ... without any output messages!]
conda install numpy
conda install scipy
conda install scikit-image
```

3) download and compile [VLFeat](https://www.vlfeat.org/) with MATLAB support *OR* alternatively download the pre-compiled version (for Ubuntu Linux):
```
cd [PATH]/hierarchical-motion-segmentation/utils
wget /usr/local/webdocs/httpdocs/motionSegmentation/CVPR18-paper/vlfeat-0.9.20.zip
unzip vlfeat-0.9.20.zip
```

4) download python code for conditional random fields (crf):
```
wget https://github.com/AruniRC/crf-motion-seg/archive/master.zip
unzip master.zip
```

5) start matlab inside you virtual environment that you created with conda:
```
/usr/local/MATLAB/R2019b/bin/matlab
```

## Moving Object Segmentation
A demo version of the code can be run in MATALB by simply executing
```
cd [PATH]/hierarchical-motion-segmentation
demo
```
This will run the motion segmentation code on the first three frames of the *forest* video sequence of the [complex background dataset](http://vis-www.cs.umass.edu/motionSegmentation/reportDef/report.html). Resuls can be found in the folder *./samples/results*. 

### Running code without "objectness" knowledge
You can also run the code only based on optical flow - without using "objectness" knowledge. In that case no precomputed results from an object proposal algorithm are required.
To do so run:
```
demo-motion
```

## Camera Motion Estimation
You can can run the camera motion estimation code alone as follows:

```
[ rotation_ABC, translation_UVW] = CameraMotion( flow, motionSegmentationMask, rotation_ABC_prev, focallength_px )
```
Input:
* *flow* is the the flow matrix with the size [H, W, 2], 
* *motionSegmentationMask* is a binary mask (size [H,W]) where static areas are labeled with ones and moving objects with zero, 
* *rotation_ABC_prev* is the estimated rotation of the previous frame and 
* *focallength_px* defines the focallength in pixel of the camera used.

This method outputs the three camera rotation angles [A, B, C] and the translational motion direction [U, V, W] (unit vector).

## Download precomputed paper results
To reproduce the paper's results we provide
* precomputed optical flow files that were generated using [Optical Flow Matlab Code](http://cs.brown.edu/~dqsun/research/software.html) and
* object segmentation masks generated by an object proposal algorithm [sharpmask](https://github.com/facebookresearch/deepmask).

Precomputed input data (flow and object proposal masks) as well as final segmentation masks computed using this code can be downloaded under the following links:
* flow of all three datasets (FBMS, camouflaged animals and complex background): [download (XXXMB)](/bla/bla)
* object proposal masks of all three datasets (FBMS, camouflaged animals and complex background): [download (XXXMB)](/bla/bla)
* final motion segmentation masks used for evaluation: [download (17.6MB)](/usr/local/webdocs/httpdocs/motionSegmentation/CVPR18-paper/CVPR18-results-png.zip)

## Differences from the Official paper
Commit abcdef follows the implementation of the hierarchical-motion-segmentation paper. Later on further improvments have been made mostly for camera motion estimation. Deviations from the main paper are the following:
* **Improved rotation compensation in 3D:**
* **More robust (but slower) optimization procedure:**


## Citation
Use this bibtex to cite this repository:
```
@InProceedings{Bideau_2018_CVPR,
author = {Bideau, Pia and RoyChowdhury, Aruni and Menon, Rakesh R. and Learned-Miller, Erik},
title = {The Best of Both Worlds: Combining CNNs and Geometric Constraints for Hierarchical Motion Segmentation},
booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
month = {June},
year = {2018}
} 
```

## Projects using this Code
