#cGPRT
Code for the paper, [Face Alignment Using Cascade Gaussian Process Regression Trees](http://slsp.kaist.ac.kr/paperdata/Face_Alignment_Using.pdf). 
Note that because the code is re-implemented based on armadillo, the results are not exactly same with the results in the paper.

Contact: Donghoon Lee (iamdh@kaist.ac.kr) 

##Installation
The code is written in c++ using VS2013 and is tests on Windows 8.1 x64 machine.
####Dependencies
- [armadillo](http://arma.sourceforge.net/)
- [LAPACK](http://www.netlib.org/lapack/)

####Cropped data and pre-learned models
- cropped data [[down]] (http://143.248.157.13:8080/sharing/IRnxfrsb8) - original data can be found in [here](http://ibug.doc.ic.ac.uk/resources/300-W/)
- data list files [[down]] (http://143.248.157.13:8080/sharing/gsCgYWUcq)
- pre-learned models and performance

| Dataset         | Paper (full1*)  | Paper (fast)  | This (full1*)  | This (full2*)  | This (fast) |
| :---            | :---:         | :---:         | :---:         |  :---:        |  :---:      | 
| LFPW (29 pts)   | 3.51          | N.A.          | on-going | 3.41 [[down]](http://143.248.157.13:8080/sharing/fFWIHLSHN) | 3.59 [[down]](http://143.248.157.13:8080/sharing/9OGXZAdvx) |
| HELEN (194 pts) | 4.63          | N.A.          | on-going | 4.55 [[down]](http://143.248.157.13:8080/sharing/Te7Lhfb8s) | 4.85 [[down]](http://143.248.157.13:8080/sharing/FQUJxlmDD) |
| IBUG (68 pts)   | 5.71          | 6.32          | on-going | 5.79** [[down]](http://143.248.157.13:8080/sharing/FEzFBql11) | 6.32** [[down]](http://143.248.157.13:8080/sharing/mXfem3ria)|

\* The full1 configuration enables Gaussian smoothing while full2 does not. Current implementation of Gaussian smoothing is quite slow, and performance improvement is not comparatively small. Thus, we recommend disable Gaussian smoothing. <br>
\** We recommend these models for general purpose.

##Usage
####Data format
- data_list example
```
689                                     // # data
68                                      // # landmark points
ibug-cropped/ibug_crop_test/im0001.pgm  // image file path
0 0 600 600                             // x_start y_start height width
212.138741 272.980541                   // x_position y_position (landmark 0)
207.482508 312.712860                   // x_position y_position (landmark 1)
...
```
- config_file example
```
num_cascades 10                     // # cascades
num_forests 10                      // # forests
num_trees 10                        // # trees
tree_depth 5                        // tree depth
nu 0.3                              // shrinkage parameter
oversampling_ratio 20               // training data oversampling ratio
num_points 68                       // # landmark points
left_eye_idx ( 36 37 38 39 40 41 )  // left_eye_center = average of left_eye_idx landmarks
right_eye_idx ( 42 43 44 45 46 47 ) // left_eye_center = average of left_eye_idx landmarks
num_split_tests 200                 // # split tests for each split nodes
random_seed 1                       // random seed for random number generation
```
####Training
```
> cGPRT_training config tr_img_dir tr_data_list te_img_dir te_data_list model
```
####Prediction
```
> cGPRT_predict model img_dir data_list result
```
##Citation
Please cite the following [paper](http://slsp.kaist.ac.kr/paperdata/Face_Alignment_Using.pdf) in your publications if it helps your research:
```
@inproceedings{lee2015face,
  title={Face alignment using cascade gaussian process regression trees},
  author={Lee, Donghoon and Park, Hyunsin and Yoo, Chang D},
  booktitle={Computer Vision and Pattern Recognition (CVPR), 2015 IEEE Conference on},
  pages={4204--4212},
  year={2015},
  organization={IEEE}
}
```


