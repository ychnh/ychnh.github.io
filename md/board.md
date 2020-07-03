* Should I use np or torch or python arrays
* What are advantages of each?
  * torch comes on top vs np
  * Python arrays allows you to append


Diff model
* Image segmentation Competitions
  * FDN16 Learning Fully Dense Neural Networks for Image Semantic Segmentation
  * Deeplabv3 pretrained on COCO is much higher?

* Deciding to go with https://github.com/jfzhang95/pytorch-deeplab-xception
  * With pretrained weights
  * 1 load model
  * Fit model for our use
  * Train/Test


* What are Dilated Residual Networks that is being used in deeplabv3+


*Experiments*
* Train 512x512
* Test 512x512, Full
* Change detection
* Prediction on train dataset
* Additional data 2 train/2 val
* 16 vs 32 fp same batch compare
* FDN_full
* Domain Knowledge

*Paper*
* Graph labels
* Conf. Mat
* Composition
* wrong highlight
* Tables
* Technical diff btw models
* Paper Abstract/Intro/Dataset/Method (models, loss, pre,postprocess)/Implementation detail/Experiments/Conclusion

*Bugs*
* Combine predictions
