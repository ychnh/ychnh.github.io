#####################
# GOALS
##################### 
# Video: 4cwsd901-4
* Seems to be an interesting candidate for monocular depth

TODO:
 Rewrite to reuse code 
* track_pose_py rewrite as well

# 6/18
* Fix trackpose Robust_dataloader bug
  * Adjust coordinates on image tf, crop, and resize
  * Update this value in the batch aug return
  * Test
* https://towardsdatascience.com/can-you-remove-99-of-a-neural-network-without-losing-accuracy-915b1fab873b

* Work on the land cover proposal
  * Try reading the korean report but it is so difficult to understand
    * Tried translating the document but fragmenting
  * Outline and specify

* Fix trackpose robust_dataloader bug
  * Coordinate updated but still not correct
  * Issue with c,r notation not being reverted by after being imported to r,c
  * Issue with not fliping image
  * Adjust pad
  * Training model
    * Issues with training adjusting.
      * Find that in the beginning it helps to have pose coord off

* Continue working on landcover proposal again


# 6/17
* Meeting at Sejeong Environment Department
  * Decide on the main point
  * Organize points of meeting
* Meeting with Landcover TF
* Saup Suhang Geuhyuk Su documentation preparation


# 6/16
* Work on finishing up wrappers for the diff poses with pose_micro
  * Encountered bug while testing pose_net due to ['coords'] being wrt to large frame
  * Design Solution:
    * Apply tf to coord points and adjust for crop
    * Test by extracting dataloader and redrawing from coords
    * Robust_dataloader 198-217

* Meeting with President and Mr Han about landcover presentation at 930 tomorrow
  * Remake Instruction Manual
  * Create Demo
  * Refine Power Point

  * Inference with Analytics
    * Colormap
    * Load Model
    * Load Weights
    * Load Data
      * TIFF
      * SHP
    * Inference
      * Batch
      * Single
    * Output
      * Colormap
        * Display
        * Save as JPG
* Work until 9:10 pm on presentation


# 6/15
* Modify slides for landcover
* Meeting with president about BIO
  * Landcover WBS Plan diagram
* Collate some images from new cmap for landcover
* Fish eye discussion with Vasyl
* Implement pose-micro
* Debug pose-micro
* Train pose-micro model


# 6/12
* Identify timesink in joint extraction
  * need further testing with actual pose image
* Implement regression model
* Train regression model

* Meeting with president,HS,JW, for rdiscussion of improving performance of nozzle track AI
* Meeting with president about landcover and biochemistry


# 6/11
* Updated color map

* Prepare landcover resources
  * Layout
    * Comparison of different models
      * Architecture affects SAM
      * Speed
      * Accuracy
        * Prediction output
        * Confusion Matrix
      * Memory
  * Comparison of hyper parameters
  * Optimization framework
  * LSTM model

* Design and develop pose-micro
  * Debugging
* Testing
* Help finding resources for airpor project


# 6/10
* C based test of tensorrt
  * pip install onnx==1.6.0
  * Test small model
  * Issue with onnx-tensorrt convertor
    * Makefile
  * Verified that c also takes cuda context 

* Find the unsupported layers and see how to convert the model, and test
  * [supported layers](https://docs.nvidia.com/deeplearning/tensorrt/support-matrix/index.html)
  * 6. Supported Ops
  * What are the unsupported layers in YOLO and POSENET
  * POSENET
    * Warning: Encountered known unsupported method 
    * torch.nn.functional.interpolate
    * torch.Tensor.transpose
    * torch.bmm
    * torch.Tensor.expand

* 1 hour meeting with president about
  * Landcover future
  * 
* Land cover presentation
  * Change color of landcover map
    * c_road = (247,65,42)
    * c_indst = (255,0,0)
    * c_paddy = (255,255,191)
    * c_field = (247,249,102)
    * c_farm = (238,233,7)
    * c_orchid = (184,177,44)
    * c_wood = (42,75,45)
    * c_plain = (57,153,38)
    * c_swmp = (124,34,126)
    * c_brrn = (89,206,202)
    * c_water = (6,2,250)
    * cmap = ListedColormap([c_road, c_wood, c_indst, c_paddy, c_field, c_farm, c_orchid, c_plain, c_swmp, c_brrn, c_water])
    * ['road', 'frst', 'buld', 'pddy', 'fild', 'farm', 'orcd', 'plan', 'swmp', 'brrn', 'watr']

    * vmin=0, vmax=6
    * Colormap and normalization


# 6/9
* Research/Investigate memory issues
* Next step
  * Compile a simple model in PyTorch2TRT
    * See CUDA Context overhead and run
* Get TRT working on C++ or just python wihtout torch cuda overhead
  * Even in python tensorrt we have this overhead issue of 900mb for a single conv2d layer


# OPTIONS
  * Resolve Compatibility issues with tensor rt
    * Github track questions
  * Refit original algorithm to be more memory efficient
    * Design plan (Reduction of channels)
    * Remove bg dependency
    * Increase batch
    * ? Is it possible to use APEX AMP investigate if possible

# 6/8
* This seems to hint that the issue lies in interpolation
* Time to redesign
  * Yolo -> microYolo. set num classes to proper number
    * Pretrained layer?
  * Remove BG dependency and tone down posenet
  * Make interpolation more optimal

* Define and train micro yolo
  * Reduced it down quite alot with alright performance
    * yolov3-micro3
  * Investigate memory allocation issue
    * Even when I change the model the memory allocated seems to remain same. Why?
      * [feature request] Set limit on GPU memory use #18626
      * Overhead context
      * I need to calculate gpu used using other means


# 6/5
* Fininsh installing
* Install PyCuda
  * Issue with NVCC
* Install torch-to-trt
  * symbolic link issue
    * /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn.so.7 is not a symbolic link
    * Some issue with not finding tensorrt package
      * Manually reloated dist-package to site-package to detect due to debian install
* Test torch2trt on yolo
  * Incompatibility error. Need to investigate

* Test torch2trt on posenet
  * Crash on tensor conversion to ConvTranspose2d
    * Investigating issues on github similar 2 openissues (recent)
      * https://github.com/NVIDIA-AI-IOT/torch2trt/issues/323
      * https://github.com/NVIDIA-AI-IOT/torch2trt/issues/326

* Investigate whyPose is not set on eval

# 6/4
* Meeting
* Clean pc to prep for tensor rt
* install cudnn and dependencies
  * https://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html
* install tensor rt
  * https://docs.nvidia.com/deeplearning/tensorrt/install-guide/index.html
* Research alternate ways to improve performance
  * torch2trt
  * Downscale pose model by removing bg dependecy


# 6/3
* Rewrite im = vid[f,:,:,:] in spray extract
  * Performance increase of 1 frame .5 sec ->.1 sec 500% faster
  * Still slow so writing batch processing of model
* Batch handle yolo and pose wrappers

# 6/2
* Suckback refine
* Adjust to use batch Design
  * Issue with diff sized images from YOLO detection
* Short meeting about airport
* Performance evaluation of yolo algo
  * Ideas batch, improve image load


# 6/1
* Vacation

# 5/29
* Investigate additional ways to improve suckback
* Organize results of bubble experiment
* Write weekly and monthly report
* Design future steps in suckback bubble algorithm

# 5/28
* Training with additional data extract create to resolve issue with A1 overfitting on spray on noz 1
* Design: Use GAN to augment/remove spray data?
* Design: When taking larger crop, make sure to pad with black or reflect to make size the same
* Clean bubble dataset and extract
* Meeting with Vasyl to work on nozzle suckback
  * Work on cropping the central portion of nozzle
  * Use first line detection top determine nozzle tip start point
  * Sobel transformation
  * Visualization of results


# 5/27
* Write report and analyze issue with A1 extraction and find result
* Continue development of bubble feature extract
  * edge filtering
  * Clamp
  * step function filtering
  * Diliation
* Meeting with vasyl to develop feature classification
  * Test on small and large dataset

# 5/26
* IMAGE FLIP NOZZLE INDEX BUG
* Retrain model
* extract data for vasyl
* Inspect analyze issues with extraction of A1
* Experiment with feature extraction

# 5/25
* train yolo
* train posenet
* extravt dataset
* Design augmentation for yolo?

* Meeting for suckback/wolor

* Delete unused weights
* Remove background dependecy of pose
* Create data for different nozzles
* Train yolo
* train posenet to be not dependent on crop as much
  * Smart aug that preserves and crops accordingly


* Annotation of data



# 5/22
* Meeting about suckback plan
* Code cleanup of scattered resources
  * Combine notebook compilation scripts into one folder
  * Adjust data formatting and exporting 
* Debug posenet issue around frm 1000
  * Due to bad traiing data in one frame
  * Retrain representation model for nozzle B0
* Start training nozzle A1 to extract data for suckback

# 5/21
* Debug Yolo multiple classes and retrain model
* Research suckback resources
* Modify pose wrapper and UITEAM scripts for handling multiple classes
  * Debug and test

# 5/20
* handle multiple classes in wrapper
  * Build structure
* Create yolo dataset for multiple classes
* Train generalized pose with better dataset/augmentation
  * Create output videos of new arctecture

# 5/19
* Pose detection improve train
  * Design of cropping algo
  * Fix existing algorithm to extract a larger crop area
  * Implement/testing algo to image augment while preserving pose

# 5/18
* Meeting for landcover report
* Meeting for golf consortium
* Create LSTM optimization and forecasting report
* Suck back 
* Pose detection improve train
  * Design of cropping algo


# 5/15
* Research LSTM Landcover
* Create LSTM report
* Meeting for suckback, and project planning with president and mr. jaeho
* Train and build train spray detector
* Generate video for demo

# 5/14
* Create Landcover implementation, optimization report
* Research LSTM, GRU Landcover and time series

# 5/13
* Read and outline Landcover project proposal and specifications from BoDalChung
* Read Landcover material request by Eterra
* Meeting to outline landcover report and present Landcover Dec 2019

# 5/12
* Meetings to prepare for landcover report (President, Mr. Han, LH, YH)
* Meetings to outline landcover report (Mr. Han, LH, YH)
* Preparing material for landcover report
 

# 5/11
* NOZTRACK
* test functionality of scripts
* Test json script. Fix minor bug with module namespace overite and other json conversion issues
* Write documentation and installation instructions
* Framework to load and process other types of nozzles and process

* LANDCOVER
* Generate full res image for all x,y, and py
  * use cmap
  * upload to gdrive


# 5/08
* Script for B0
  * Yolo detect different nozzle types
  x Move json stuff
  x Familiarize with output input
  x Validate water spray data
    x Revalidate due to issue with continuing after crash
  * Train spray detector
  x Script file
    x Complete SPRAY_LIQUID_SCRIPT=LIQUID_VALID
    x Complete POSITION_VALID
    x Make core lib
  x Remove BG dependecy because I dont think it matters
    * TODO: remove as part of training in future
  * Load model based on class
  x Remove warning message on posenet load weights

* Recover crashed computer while processing spray data
  * Clean spray data that had bad writes

# 5/07
* Output result videos for B0 and spray data as well
* Issue with B2.avi due to reduced augmentation
  * Figured out issue was due to clamp upper bound set at w and h
* Design solution to yolo

* Why is the rep net not detecting nozzle even when parts of nozzle is visible?
* Why is our yolo so bad at centering the object?
  * Maybe has to with how we are augmenting a cropped image instead of aug the whole then crop
  * Solution: will we aug the image, need to get a larger outer frame when preserving the image and then crop from center
  * This is a more advanced form of cropping
  * Seems like the most recent problem is due to my pose net not being up to par to various variations in the nozzle frame capture. In otherwords, my posenet should and needs to be able to detect pose as well as the nozzle appears in the detection frame and we need to adjust the augmentation according to this
  * **We cut some corners** regarding augmentation and now we need to fix it
  * Also consider how we started training repnet from base and tranformation matrix. What is this base form.

* Design
  * We trained the pose detector with viewing the entire outer frame. If we want it to be more robust we should train pose detection with zoom and closer variation.
  * *POSE* Detection
    * Improve pose detection by training with non perfect crops and variations in crop
  * *SPRAY* detection
    * In a similar manner, sprat data should be collected to account for minor deficiencies in pose by sampling non perfect spray boxes



# 5/06
* YOLO issue solution
  * If we are continuing with B0 just add more frames to rep frames and adjust the saved B0savedata to fit the included frame size
  * Also just make  the pline points have no interval between the more frames noncontiguous frames 

* Do less augmentation
* Resolve issue with training yolo
* Update training data with complete range of motion of nozzle



# 4/29
* Landcover [Landcover](http://www.g2b.go.kr:8081/ep/invitation/publish/bidInfoDtl.do?bidno=20200436765&bidseq=00&releaseYn=Y&taskClCd=1)
  * Documents
    * Bidding procedure/process announcements
    * Reason for emergency bidding
    * Terms and Conditions
* Testing of model on B0 different videos
* Designing how to handle Yolo problem

# 4/28

* Debug troublesome pose by looking at py and connection with reflected border annotation
  * Try the yolo augmentor

* Test background aware pose predictor model

* Multiple predictions for pose in diff settings
  * Test time augmentation

* Ok our model still seems to have trouble
  * So the idea is to use both latent and non latent space to make the predictions
  * We'll take elements of our SBP and add it to predict pose during representation and pose training
  * We'll see how well it does with B0 and also how well it does with D0

* maybe bbox need to be manually annotated and then interpolated


# 4/27
* Finetuning to solve issues encountered during B0 training
  * Test yoloaug branch
  * Added more augmentation and validation routine
  * Identified potential issues with yolo
  * Increase batch size?

* Background aware pose predictor
  * I feel like part of representation learning invovles the background removal which is invalidated when presented with new examples not seen?

* **Spray Trainer**
  * /home/yhong/work/semicond/DaSiamRPN/code/spray_detect_MN 
  * Data loader/ augmentor
  * Test and validate with visual display

# 4/24
* Removed torch sigmoid warning
* posemodel printing 3 times remove

* Extract water spray from video
* Identified key weakness with YOLOv3 model overfitting
* Review architure of yolo module and see if we can write wrappers

# 4/23

* Verify training of representation
* Meeting 9:30-10:30 incheon airport
* Remove the potential strange case of shift or rotate duplicating the borders as we move
* [Construct wrappers around yolo and pose and join them outside]
* Extract spray


# 4/22
* Train and validation of yolov3 datapacker
* remove warning 
* add validation images to yolo
* Fix bug with datapacker needed centered points not TL
  * Lesson keep a clear documentation of the input output and data format
* Finish datapacker for rep net
  * Add visualize
* Adjust convention in annotation to handle just point

* Something wrong with BG
  * old shuffle code used
* Need to offset coords wrt to framed bbox
* Visualize and validated Repnet/posenet dataset
* Add options to train_encdec2D.py train_pose.py


# 4/21
* Compile Cuda report
* Clear up design and workflow

[
* Raw video
  * Extract key frames of interest per nozzle (Embedd spray data)
* Annotation of joint data from sub scene[crop]  (Innotator)
* Extract bbox with center point
* Use the following info to generate data for 
  * YOLO (Image and Bbox) -> Push as custom dataset format
  * REPNET and POSE (Cropped background and image) and (Coordinate data)
  * SPRAY DATASET (0,1 label with placeholder for image data)

  * Combine all workflow design and plan
  * Annotation  joint labeling workflow implement
  * Data packers for yolov3


[
* Train YOLO, REPNET, POSE
* View validation during training (A Collection of UTIL TO VISUALIZE, nozzle pose draw, annotation of draw, pose heatmap draw)
* Extract spray image and fill in SPRAY DATASET
* Train spray (ImageNet)
* FINAL LINK ALL (When Designing components make sure that they are linkable)
]



# 4/20
* During training some components not displaying
  * I think this is due to lower components being cut off
    * Make randius larger than 50?
    * Tone down augmentations that cut off
    * Make sure that all parts are being displayed by adjusting weights to heavily penalize if nothing is showing
    * Flip transformation
* Meeting with Haesol about homography
* Meeting with team at 2pm to talk about progress and what we are doing
* Creating readme/requirements for trackpose
* Nozzle spray
* Research and extract version validation for cuda 10.1 10.2 at same time

# 4/17
* This raises 2 questions test the validity of pose draw with test data
  * Verified validity need to update data 
  * Built pipeline to extract, interploate annotation and pack data for pose, background, and raw img

* Only train pose on nozzle ends and see if it can track better
  - posesprayfocus
  - Not as good as using all 6

* Train direct pose instead of representation
  * Trying does not seem promising

* Train pose on where water is actually coming out
  * On going


# 4/16
* Understand git merge/commit/branching
* Experiment with large rotation 40: Yes critical
* Experiment with larger batch: Not working as well
  * Trying with epoch 800 with larger batch
* Model seems to learn after 800 epochs any ways to make this faster?

* Multipile cuda https://medium.com/@peterjussi/multicuda-multiple-versions-of-cuda-on-one-machine-4b6ccda6faae

* Organize library of functions that were nice and useful
  * Under DASIAM/code/Tracker_test
* 2 Experiements
  * Only train pose on nozzle ends and see if it can track better
    - posesprayfocus
  * Train direct pose instead of representation
  * Train pose on where water is actually coming out


* Next steps is to train on other nozzle types
  * With the key question, can we extract spray region?
  * Gather pipeline in the interpolation library

* Future: What about using same model to work with multiple nozzles?
  * I think we need VAE at that point
  * Is this something that we want to do? I def. think so


# 4/15
Holiday

# 4/14
* Will commit code to git
* Test method on all nozzles and prepare to extract spray data and annotate for spray detection
* Possible to have 1 model to all?
* Append translation/scale to rotation
* Increase batch size (Not so good)
* Smoother? (RNN)?

* Can also hotwire transform 
  * so that model doesn't always predict identity
    * model(x,bg,hotwire_tf) == py_with_tf

* VAE
  * https://jaan.io/what-is-variational-autoencoder-vae-tutorial/
  * likelyhood P(X = x | θ) probabilty of an event given a model
  * ${\displaystyle {\mathcal {L}}(\theta \mid x)=p_{\theta }(x) = P_{\theta }(X=x | \theta)}$
  * Likelyhood of x over distribution of latent + KullbeckDivergence(encoder dist[qθ(z∣x)], p(z) )
      * where p(z) is normal dist with mean 0 std 1

* Seems like actually training the specificity of tf matrix is not as important

# 4/13
* Encode into single rotation
* Convert b['rot'] to torch
* get RotMat from rot degree Make sure to normalize
  * It seems like the matrix method works better since it can model alot of other transformations other than just rotation, (includeing translation)

* How would you have a *pipeline to test different* versions of code
  * Probably best way is to do the *github branch* idea
    * Need to manage my source
    * And save *common elments in a shared location* that makes sense

* Do we even care about rotation?
  * Maybe what is important is the latent space
    * Replace y with x and set rotation to 0
    * Setting rotation to 90 to enfore high level of rotations
      * maybe 90 too extreme try 45?

# 4/10
* Progressive difficult training example design
* Add aidashboard component for pose
* Document progress of training

* [TODO]: Join annotation and test
  * Need different ways of drawing joints
  * Debug issue with resizing post yolo detection
  * Bug with non-rotated nozzle in the actual video

* TODO: Fluid pipeline to annotate, then train (tracker and representation,pose) , and some way to validate
* TODO: Also need to think about how to extract water region

* CUDA Potential solution
  * https://blog.kovalevskyi.com/multiple-version-of-cuda-libraries-on-the-same-machine-b9502d50ae77

# 4/9
* Try with regression?
  * With joint extraction code on ypose img aug data
  * BN bug debugging
  * Monitoring progress code
* Progressive difficult training example design

#Potential Improvements
  * place emphasis near spray region
    * NAN error
  * Train for more after each adjustment
    * Running
  * Dataloader shifting is too much  that it cuts off sometimes
    * Runing with adjusted
* Issue with: why is it not learning with smaller joint size? (at 100 epochs)

# 4/8
* zoom_xy multiple channel
  * Convertto cv function from PIL functions
  * fix bug with neg index
* run y pose training
* Monitor pose training algo
* Train with regular/freeze/with diff label size

* Why is verything looking same for all channels
* Why are later 3 channels not learning?

# Labels
  * Radius of pose labels
  * Use discrete vars?
# Model
  * Freeze
  * Train at the same time?

# 4/7
* Validation of shift_scale augmentation training
  * Bug fix with mixed augmenation of training data
* Implement x and y scale
* prepare pose training by aug pose data
* Separate color and structure augmentation 
* Add flexible framework to augment any number of objects including ypose
* Bug with zoom_xy 
  * Multiple channel


# 4/6
* Extraction data workflow with interpolation classes
* Center and pose generation
* Rotation and crop image processing workflow
* New team meeting

# 4/3
* Designing tracking workflow
* 2.5 hour meeting about incheon

# 4/2
* Experiments with augmentation
  * In an attempt to get it to recognize
  * I feel like based on our pose experiments, it should know

  * PoseNet
    * Detect pose even during train/test split
  * NVS Net
    * Cannot detect pose during train/test split

  * Pose net uses feature based and it can pick up in the variations between the nozzle types
  * NVS net is having issues due to compressing info into latent space
  * [E] L [D] Out
  * Encoder needs better training
  * I propose that encoder needs to improve

  * I think we should work on tracker pipeline first
  because this is a hole without end
    * Fix weird bug with tracker

# 4/1
* Debug yhcuda compile issues
* Design and build annotator and data manipulator utility
* Experiment with projection
  * Adjust yolo
  * Output video
* Design and build nozzle tracking workflow

# 3/31
* Semi Eye meeting
* Compile rough time log for 3/31-1/10
* Projection Hom review and dev
* Request additional data
* Plan and design nozzle data extraction pipeline

# 3/30
* Use a very early model and pose estimation seems to work
* Bubble data collection and report creation

# 3/27
* Debug Pose 3d
* Over fitting issue. Models of NVS representation trained over 100 epochs seems to work really poorly to generalize

# 3/26
* Shift nozzle representation
* Nozzle pose detection not working well wioth regression
* Change model to heatmap generation

# 3/25
* Nozzle representation fix
* Generating represenation images well
* Build pose detection dataset and build pose dataset for nozzle D2

# 3/24
* Incheon airport research and document preparation
* Train and debug nozzle NVS generation

# 3/23
* Incheon airport research and document preparation
* Adjust loss to include feature error from resnet18

# 3/20
* Incheon airport meeting (Long meeting)
* Clean nozzle data to center and adjust with rotation and scaling
* Nozzle training with relative angle difference added.

# 3/19
* Issue with generating realistic image
* Working well

# 3/18
* Build and design 3D representation network
* data compile. Train

# 3/17
* Augment data to create data for flip angles
* Understand 3D rep posenet architecture

# 3/16
* 3D rep posenet collect data
* Align with 3d rotations
* Construct matrix

# 3/13
Research solution for nozzle occlusion
Research nozzle representation
논문: Unsupervised Geometry-Aware Representation for 3D Human Pose Estimation

# 3/12
Implement combining Yolov3 with nozzle pose detection
Add visualization of Yolov3-pose network
Debug poor results in some poses due to bounding box cutoff
Design additional augmentations to improve performance

# 3/11
Plan combining Yolov3 with nozzle pose detection
Modify nozzle pose detection model with BN and RELU and compare
Extract nozzle joints from heatmap naïve algorithm

# 3/10
Debug issue with nozzle data size variation and power of 2 downsampling
Implement training loop for nozzle pose
Implement image augmentation for nozzle pose

# 3/09
Validate Yolov3 arm detection
Task Force Meeting
Implement model and dataloader for nozzle pose

# 3/06
Convert joint annotation to gaussian point pose data
Convert bbox data to PyTorch-Yolov3 format
Debug and train Yolov3 arm detection

# 3/05
논문: 인간 포즈 추정 및 추적을 위한 간단한 기준선
논문: 인간 포세 추정을 위한 적층 모래망
Design nozzle pose detection architecture
Refactor old nozzle tracking script

# 3/04
Test optical flow in normal and motion blur sequence
Annotate A1,A2,A3 pose data with optical flow
Generate and validate bounding box from joint annotation

# 3/03
Optical flow arm joint propagation, debugging and visualization
Switch to cv library for pyramid optical flow
Extend innotator tool implement points
Extract annotation data to optical flow data

# 3/02
Setup VPN and remote desktop
Implement and debug Lucas-Kanade optical flow algorithm with gaussian weight
Research potential solutions to issues with Lucas-Kanade

# 2/28
* Water track script added to offset the normal tracking
* Python script build for backend

# 2/27
* Tinker with retrack adjust tresholds
* Python script design for backend
* Validation

# 2/26
* Tinker with retrack adjust tresholds
* Work on validation
* Paper conference contact closed due to coronavirus

# 2/25
* Tinker with retrack adjust tresholds
* Work on validation

# 2/24
* Retrack algorithm design and implement
* Work on testing retrack algorithm

# 2/21
* Review and understgand source code of SiamRPN and DaSiamRPN
* Begin adjusting the code I have to apply.

# 2/20
* Research and understand the workings of Siamrpn DaSiamRpn 
* instead of just blindly applying

# 2/19
* Loop over entire dataset to test the algorithm determined day prior
* Encountering additional issues

# 2/18
* Experiment with various full search algorithms and tresholds but isnt' working so well
* Read about VAE

# 2/17
* This approach is also failing on quick move
* Implement relocating object using a full search algorithm but isn't as good as we want

# 2/14
* Transfer annotations and begin testing

# 2/13
* Data annotator tool build

# 2/12
* Data design and build organizer 
* Data annotator tool design and build

# 2/11
* Sick but had to come to work
* Data annotation (Time stamp extraction of key points)
* Initial boxes ann

# 2/10
* Sick but had to come to work
* Data annotation (Time stamp extraction of key points)

# 2/3-7
* Design and build backend structure to extract and deal efficiently with model data
* Training nozzle data

# 1/31
* Understanding SiamRPN paper to see why issue is occuring
* Managing model state more efficiently

# 1/30
* Small nozzle issue with SIamRPN
* Investigating solutions
* Design approach to do nozzle spray detection

# 1/29
* Bugs/testing SiamRPN
* Design approach to do nozzle spray detection

# 1/28
* Investigate issue with lossing tracking when moving fast

# 1/27
Vacation
# 1/24
Vacation
# 1/23
Vacation

# 1/22
* SiamRPN research
* Wavelet transform?

# 1/21
* DaSiamRPN research

# 1/20
Vacation (SICK)

# 1/17
* Test and research OSVOS model on easy/difficult examples

# 1/16
* Test and research OSVOS model on easy/difficult examples
* Meeting wiht korean medical doctor

# 1/15
* OSVOS heatmap based approach 

# 1/14
* Research ai based approaches
  * OSVOS
  * Fast RCNN
  * Yolo

# 1/13
* Try Akaze feature based tracking method
* Compare different methods
* Determine that should go with ai approach

# 1/10
* R&D feature based nozzle tracking
  * Optical flow video tracking methods
# Following reports will be abbreviated because they were taken during crunch period time
###### End of quick time log

# 1/9
0900-1000
* Develop: Nozzle tracking
  * Issue with channel index mismatch
  * Trying feature extract for diff frames
    * Some frames have only 1-2 frames
1000-1100
* Try Gaussian blur remove noise ( Makes performance worse )
* Try harris corner detection (Not so good )
* Write report of current developements
* Investigate Greenia's water/nozzle tracking algorithm
  * Seems really chamber specific solution
1100-1200
* Develop feature tracking for nozzle box track
* Develop draw library for torch, np, index-universal drawing
* Feature matching 
* Debug wrong offset drift
1200-0100
* Lunch
0100-0124
* Code clean/ refactor
  * Move notebook code to semi.py
0124-0134
* Call with president
0134-0230
* Adjust code to detect with sequence of frames as input and continue 
0230-0314
* Create prereport
* Investigate NaN issue (probs len of goodmatch=0)
* Fixed img2 being set with img 1, better performance in tracking features
* Design: Need to add handling for NaN cases were no common features are detected between frames
  * Skip over next couple frames
  * Use momentum based approach
0314-0340
* Meeting with Vasyl at office to discuss current state
0340-0414
* Meeting with Vasyl to discuss improved feature extraction
0414-0600
* Harris corner exp
* Sobel xy dialation intersection feature extraction
* TODO: Need to design feature descriptior
  * Question: Hessian Blob detector
  * Question: Features at different scales?



# 1/8
0900-1020
* Analyze results of landcover SPADE Normalization
1020-1040
* Meeting with Vasyl
  * Yesterday's plan of developing 3 different approaches to edge detection
  * Change of plans by Junghwan to work separately on different subtasks Will work with Vasyl on Moving Nozzle Detection (MND) and Arm Position at Start (APS)
1040-1113
* Research: Hessian and Jacobian Matrix for edge feature (APS)
* Research:SURF feature (MND)
* Research:CNN Edge detection (APS)
  * Seems too imprecise and rough for use
1113-1200
* Research: Haar-Wavelet Transform
* Research: Integral table
1200-0100
* Lunch
0100-0200
* Research: Oneshot learning for nozzle detection (MND)
* Research: Laplace Matrix for edge feature (APS)
0200-0304
* Research Development: SIFT Feature detection. Patented method.
0304-0310
* Call with President
0310-0330
* Histogram approach study. Color variation between different lenghts of frames
0330-0335
* Meeting with JeongHwan
0335-0430
* Optical flow based approach
* Reduce feature selection range by looking at previous frame
0430-0500
* Time Logging 1/7 1/8 for daily report


# 1/7
0900-0930
* Email
* Meeting with Vasyl about SemiEye
0930-0950
* Landcover SPADE Normalization
0950-1000
* Resolve issue with vacation time hiworks
1000-1015
* Time logging  1/6
1015-1100
* Moving Semi Conductor machine
1100-1200
* SemiEye Meeting
1200-0100
* Lunch
0100-0200
* Debug SPADE Normalization and run training
0200-0222
* Meeting with Vasyl and Junghwan
0222-0245
* Meeting with Solution Team and JaeHo Team Leader
0245-0300
* Research modulation (Contrast) Transfer function
0300-0440
* Semiconductor record data Vasyl and Junghwan
0440-0510
* Meeting with President
0510-0600
* Research precise edge detection


# 1/6
0900-0910
* Setup / email
0910-0951
* Refactor image sequence class
  * remove unsqueeze outside of class
  * Analyze wafer securing
0951-1051
* Detect wafer securing and searching
* Plotting results
* Issue with wafer lock not showing. Debug
1051-1200
* Manually find wafer lock frames and view differences 
* The pixel average technique is not working well for wafer lock
0100-0200
* Histogram compare
* Design histogram distance
  * Earth mover's distance
0200-0241
* EM metric simplex linear programming problem setup
0241-0340
* Time logging 1/3, 1/2, 1/1, 12/31
0340-0423
* Test dan_IN_f64 at different epochs
0423-0450
* Semieye histogram experimentation and averaging techniques on edges
* Noise reduction
0450-0520
* Meeting with Vasyl
0520-0600
* Questions for meeting tommorrow
  * What methods have you tried
  * How many diff chamber environments
    * Is calibration each time ok?
  * noise and can change camera position
  * have to fine position or just detect deviation of 10mm
* High Precision Edge Detection Algorithm for Mechanical parts - Duan 2018



# 1/3
0900-1030
* Landcover interior loss
* Boundary loss
* Run 2 trianing on 32 and 64 float on a CKGPU and on yhongHP
1030-1143
* Organize information about SemiEye
1143-1230
* Meeting with president about landcover and SEMIEYE
1230-0154
* Lunch with president
0154-0300
* Reading papers about precise distance measurement and subpixel accuracy
0300-0330
* Meeting with Vasyl about future direction
0330-0430
* Semi-eye gate close searching and detection
* Semi-eye wafer secure detection
0430-0600
* Experimenting with average techniques to reduce noise
* Looking at different channels to see the presence of noise


# 1/2
0900-1030
* Check results of training DAN512v4
* Not much improvements over original method
1000-1100
* DAN focus HD
* Train
* Change logger to output validation data to exp_dir to run multiple on CKGPU
* Setup code to run aidash on CKGPU
1100-1200
* Shift focus to SEMIEYE semiconductor
* Inspect 4 video data sent
0100-0300
* Extract data of 1 video for all frames
  * Out of memory when loading all data to ram
* Construct external data handler to easily manage data
0300-0400
* Matplotlib video display and cropping
* Detect when the gate of the chamber is open using average of color
0500-0600
* Plot results of detect chamber open
* Design time dependant variable

# 1/1
0900-0600
* New Years Holiday

# 12/31
0900-1100
* Writing paper, All the auxilary sections
1100-1200
* Inspect and log results of training 512v3
* Compare. Not much improvements compared to original method
* Minor increase in validation .5% but not much improvement in test dataset
0100-0300
* Inspect and log results of training 512v4
* Not much improvement also. performs worse in certain cases
0300-0430
* Modify DANv4 512 size adjusted weights on plain for cross entropy
  * Corrector module training with ASPP
0430-0530
* Train and adjust oom errors
0530-0600
* Plan future direction
  * High resolution convolution?

# 12/30
0900-0920
* Time logging
0920-0945
* Paper: Inspect results of training 512v2
*   Minor improvements on certain categories
0954-1030
* Create 1024 dataset
  * OOM when testing on yhong
    * Moving to CKGPUSERV
    * Training on CKGPUServe
  * Inspect orchid sat data
1030-1200
* DANv3 dense feature pooling of 5 feature layers
* Training
0100-0300
* Implement DANv4 512 size
  * Multiple loss function with corrector after prediction
0300-0430
* Inspect training
0430-0700
* Company travel/meeting/dinner

# 13/27
0900-0920
* Time logging
0920-1040
* Incheon car detection documentation collection
1040-1200
* Landcover paper/research deepaggr2
0100-0230
* Finished modifying deepaggr2
0230-0330
* Test& Inspect deep aggr2 training
* Adjust aidash and add condition checking for folders
0300-0400
* Build 512x512 dataset
0400-0445
* Dev confusion matrix plot code with existing code
0445-0520
* Build batch evaluation code
0530-0600
* Inspect training of 512 size
* Design corrector module

# 12/26
0900-0920
* Time logging
0920-1145
* Paper ( Conf. matrix and wrong analysis )
1145 - 1200
* Translate tutorial
1200-0100
* Lunch
0100-0145
* Translate tutorial
0145-0245
* Paper, Conf matrix result analysis
* Paper. Generate graphs of conf matrix in matplotlib
0245-0300
* Brainstorm new ideas
0300-0320
* Paper research. Larger convolution layers? Features?
0340-0345
* Tutorial reupload and send to eterra
0345-0510
* Paper research ( PCA for determining shape )
0410-0600
* Test and log detailed 2048 vs 3072 
* Test and log non max  val for b32f16 b32f32
* Test and log max  val for b32f16 b32f32

# 12/25
0900-0600
* Christmas

# 12/24
0900-1000
* Timelogging 12/18, 12/19, 12/20
1000-1030
* Email and message about tutorial
1030-1100
* Landcover paper draft writing
1100-1115
* Meeting with president 
  * Tutorial and what to give and not give eTerra
  * Paper goals/outline
1115-1130
* Semi conductor summarize progress
* Future: Shift gears towards tutorial and paper
1130-1200
* Semi conductor research
0100-0230
* Tutorial Testing
* Tutorial writing instructions/prereq
0230-0443
* Tutorial writeup doc module and prediction
0443-0530
* Tutorial writeup dataset usesage
0530-0550
* Meeting with  president
  * Ettera verification
  * Seminconductor plan
0550-0600
* Landcover Paper

# 12/23
0900-0600
Vacation

# 12/20
0900-1100
* Semiconductor research
  * New Wafer Alignment Process Using Multiple Vision Method for Industrial Manufacturing 
    * https://journals.sagepub.com/doi/full/10.1177/0020294015602499
  * Technology and Innovation for the Future of Production. Accelerating Value Creation
1100-1200
* LithoGAN: End-to-End Lithography Modeling with Generative Adversarial Networks 
0100-0230
* Machine Learning in VLSI Computer-Aided Design - 2019 
* Summary so far
  * Domain
    * Fabs
    * IC fabrication process
    * Wafer
    * Random or systematic defects
  * Task
    * Automatic Process Control
    * FDC Interlock
    * Optical wafer inspection system
    * Machine Vision
  * Location
    * Spin/Coat, Develop, Etch
    * Lithography Track system
0230-0400
* Shift direction towards
* Anomaly Detection
  ALGORITHMS FOR SPECTRAL DECOMPOSITION WITH APPLICATIONS TO OPTICAL PLUME ANOMALY DETECTION
0400-0600
* Prepare small plan for Mr. Lee Kyoung Ki
  * Wafer disk
  * Wafer presence, location
  * Moving Nozzle and SWING location
  * Fixed nozzle spray location
  * Moving nozzle chemical discharge presence/abscence
  * Moving nozzle spray discharge presence/abscence
* Research Seminconductor

# 12/19
0900-0935
* Download the required drivers to print techincal report 
* Undo Meeting room computer security to download backup files
0935-1200
* Literature review Seminconductor. 
* Overview of simliar existing methods
* Vision Course pdfs http://webdiis.unizar.es/~neira/vision.html
  * Review additional slides
* Robotic handling systems
* Optical wafer inspection system
* APC methods such as RtR control and FDC
* Automatic Process Control
* Spin/Coat, Develop, Etch
0100-0230
* SYSEYE
  * Template Match (NCC, SSD),  edge detection algorithm, difference video.
  * Height detection by edge detection, water drop detection by differential image, other binarization, erosion / expansion.
  * Color distribution change image, erosions / swelling.
  * Calibration
* Greenia
  * wafer position, cup fume, nozzle suckback, nozzle dispense, nozzle leak, wafer coating, core size, bubble
0230-0500
* Fault detection and classification (FDC)
* Interlock stop the operation of machine
* Line Interlock
  * Recipe/Reticle/DCOP/FDC
* Flat panel display FPD
* robotic handling systems (RHS)
* an open cassette, FOUP, a process chamber, etc.
0500-0600
* Vision Course pdfs http://webdiis.unizar.es/~neira/vision.html
  * Review additional slides

# 12/18
0900-1030
* Technical report application
* Need Certificate of identity
* Calling the company because need to add a new item to the report and special case for new registeration
1030-1230
* Meeting with Wafer
* 2 months promise
* Suckback, Wafer Position, Arm position
* Hynix
0100-0200
* Research wafer
0200-0230
* Meeting with Lee Kyung Ki
  * Future progress
  * Reduction in work time from 2month to 1.5month
0230-0300
* Rezip and clean computer 
0300-0400
* Upload file 
  * Too big for hiworks
  * Too big for Outlook
  * Purchase google drive and upload
0400-0500
* Literature review Seminconductor monitoring
0500-0520
* Meeting with president about Wafer
0520-0600
* Literature review Seminconductor monitoring

# 12/17
0900-0920
* Time logging
0920-1100
* Combing report with Vasyl
1100-1130
* Report revise
1130-1200
* Meeting with CEO
  * Wafer Semiconductor
0100-0300
* Finish up report
* Download weights, dataset, and model definition remove comment
0300-0330
* Make file table of conents
0330-0430
* Computer crash
* Rezip files
* Delete more files from C: Drive
0430-0600
* Semiconductor research

# 12/16
0900-0920
* Time logging
0920-1020
* Writing report 4.7, 4.8. Change detection additional test data
1020-1109
* Writing report 4.8
1109-1140
* Meeting with president
  * Sign Language AI
  * ADD proposal
1140-1200
* Writing report
0100-0145
* Writing report section 3.2.2, 3.2.1
0145-0215
* Technical skill application
0215-0240
* Computer restarting and clean C drive out of memory
0240-0320
* Clean up code files for eterra
0320-0445
* Revise Landcover Report
0445-0600
* Research Sign Language AI


# 12/15
1100-0100
* Read DeepMind Quake paper
* Select key components for ADD project
0400-0600
* Write report
0600-0700
* Skim landcover proposal to understand format
0800-0900
* Revise report

# 12/14
0200-0400
* understand policy and RL concepts
0400-0500
* Q function?
* MDP theory
0500-0700
* Read DeepMind Quake paper
* Review concepts of RL
* Organize notes

# 12/13
0900-1200
* Section 4 Exp 4.1, 4.2, 4.3, 4.4, 4.5
0100-0210
* Section 4.6, 4.7
0210-0250
* Meeting ADD #1
* going to spend time working on ADD Proposal instead of Eterra report
0250-0407
* Research of ADD
0407-0600
* Meeting ADD #2

# 12/12
0900-0940
* Timelog 12-10, 12-11
0940-1215
* Business trip Ares ADD
0100-0130
* Email
* Organize notes
* Business trip forms
0130-00310
* Eterra report 1, 1.1, 1.2, 1.4
0310-0340
* 1.3
0340-0410
* Start section 3 outline
0410-0530
* OPenAI / Deeplab research
0530-0540
* Meet with Vasyl about ADD
0540-0600
* Eterra report


Business Trip Notes
3.2.3 45
weight speed
2v2 pilot, roll pitch yaw
shot plan
headon off
crank
pump
rule baesed
log and curr data
dog fighting
신ir missile diff baesd on effectuve
take off navigating
가시거리
원거리 flare chuaff gun, missile 공대공 
clouds
separation of role
escort
dca region protect 
 scenario and initial settings
 hot cold
 유관 현상정보  영상쟈료
 max g limit
 speed max 
 12-26
 금주 초안 12-20 16일 ?????!!!!


# 12/11
0900-1030
* Inspect training of swap better performing experiment
* Seems like adding the additional data worsens performance
* Prediction on training for these newly added dataset also doesn't do well
1030-1200
* Business Report compiling graphs and images

0100-0110
* Business report compiling
0110-0210
* Meeting with Ares comapny about reinforcement learning
0210-0500
* Finished compiling graphs with labels and predictions images and scores
0500-0600
* Start outlining and writing Business report from ETRI format


# 12/10
0900-0920
* Time logging 12/9
0920-1000
* Resolving issue with 10%~20% lower accuracy on 35616082, 35616061 additional data
  * 35616061 predicting grassland with forest 10% lower
1000-1100
  * Compile data of mislabled training data where grassland is set as forest
1100-1200
* Resolving issue with 10%~20% lower accuracy on 35616082, 35616061 additional data
  * Issue with 35616082 identifying orchid as plains and field/paddy as barren
  * Potentially with validation dataset having particular barren regions and our model optimized towards it
0100-0250
* Trying to identify the issue by combining classes
  * Compute conf matrix to see what is going on
* Refactor confusion matrix display code
0250-0350
* Meeting with 소장님 about Incheon Airport
  * Korean research papers organize
  * Computation requirements
  * Accuracy statements
0350-0500
* b32f32 testing on additional datas
* b32f32 Works well with other 2 additional data 34603027 35616034 with 10 classes
0500-0600
* Rebuilding experiemnt to swap better performming as test and worse performing as train


# 12/9
0900-0940
* Time logging 12-6 12-5
0940-0950
* Email
0930-1032
* Examine results of 512x512 extra data training on validation dataset
* prediction on test dataset
* Big issue with 512x512 having about 10% lower accuracy!
1032-1200
* Resume for 소장님 and ETRI

0100-0110
* Resume format adjust
0100-0500
* Test on val 2 and 3
* Comparison test with regular training without extra data
* Inspect of prediction results case by case
* training separate module
0500-0530
* Meeting with Vasyl about writing project report
0530-0600
* Plans to fix the 10% error in prediction issue
  * Reduce from prediction of 11 to 10 classes by combine paddie and field
  * Alternative model

# 12/6
0900-0930
* Check conference and format
  * 대한공간정보학회 (English okay)
  * 원격탐사학대 (english okay)
  * International Symposium on Remote Sensing (English okay. Feb28 deadline)
0930-1000
* Research on CRF (PydenseCRF)
1000-1130
* Compiling 512x512 dataset of new data
1130-1200
* Meeting with 소장님 about Incheon airport project
  * Incheon airport camera review
  * ETRI resume profile
    * Incheon work by 4pm
0100-0120
* Incheon airport homography research
0120-0140
* Resume meeting with Vasyl
0140-0410
* Incheon research
  * Homography transform
  * Field test aircraft ramp poeration (2018)
  * Deep learning bev(2019)
  * Orthographic feature transform (2019)
0410-0526
* Training 512x512 and seting up view for experiment
0526-0540
* WBS report
0540-0600
* Inspect ETRI report documnetation


# 12/5
0900-0910
* Email/ free space on realtimetech desktop
0910-0930
* Time logging
0930-1003
* Move large 3000x3000 prediction code to module
* Test with change detection
1003-1036
* New matrix size tile mismatch bug detection investigation
  * New code not calling format
1036-1200
* Change detection code
  * Mask formation to detect change
  * Implement first in GIMP
  * Then decide to just use process image in python and save
0100-0140
* Change detection report
0140-0200
* Inspect new dataset
0200-0250
* Planning future direction/code refactor
  * Passing option module into model (Try avoid chanining variables to property classes)
  * Make dataloader just load 1 sec of images and make another dataloader combine
  * I am not too comfortable with the bit complex construction of lbl and geo spatial image
  * with is prediction a complex process
0250-0500
* Refactor geoimg.py labelimg and geoimg construction workflow
  * Need to spend more time refactoring labelimg reprojections
0500-0600
* Refactor testing


# 12/4
0900-0915
* Conflict resolve util.py
0915-0925
* Timelog
* Generate and stitch prediction for 3000x3000
  * proj structure changes, move label.py, geoimg.py, examples.py to lulc
0925-1133
* Finish tiling and list of full 3000x3000 images
  * Overcoming memory issues
1133-1200
* Out of memory on secondary drive (SSD)
  * Inspect data composition
  * Move old data into 3d drive (HDD)
0100-0130
* Begin organizing experiments in report form 
0130-0154
* Organize report of 3000x3000 stitching
0130-0154
* Organize report for f32 vs f16
0154-0234
* Organize report for prediction test
0234-0300
* stitch prediction probabilities experiment
0300-0320
* Index based handling
0320-0333
* RAM memory error crash
* Cannot access computer
0333-0407
* Research on WLAN and reboot on solutions
  * Watchdog process?
0407-0417
* Research code for confusion matrix display
* Need to answer question of normalization
0417-0515
* Computer unfroze
* Finished combined prediction probability code
  * Key issue is solving memory is to use torch tensors instead of numpy because they are aobut 1/3 more effiecient in memory storage
  * Also serialization needs to be done with torch.save
0515-0600
* Prediction/change detection with tile 16
* Fix dataloader to handle data sources with 1 input (In case of prediction change we only have src)
  * TODO Need to make architecture change of making it handle just one type of data
* Issue with sq tile artifact appearing in tile prediction combine
* Issue resolved when using large 3000x3000 prediction
* Our tiles have different size, why?






# 12/3
0900-0920
* fixed conflict error in util
0920-0950
* Time logging/Review b32f32 f16 exp
0950-1007
* Research/Lit review
  * HRNet
1007-1019
* os.fork multiprocessing in python
1019-1200
* Refactoring tiling and stitching code to streamline testing accuracy of different sizes
0100-0223
* Finish streamline crop and mirror margin
0223-0500
* Finished tiling rewrite and invertible tileing refactor
* Verify the every odd tile stitching works
0500-0600
* Debugging. Verified that original image and tile->stitched image are the same


# 12/2
0900-0920
* Email/ organization
0920-0940
* Time logging
0940-1010
* Inspect new data. 
* Some issues with new data. Send email
1010-1030
* Start augmented test with fdn
1020-1030
* Issue with finger print scanner on 11/15
  * Says I admited on 11:16 but I was present at 9
  * Meeting with secretary kimgjunghee
1030-1200
* Planning and outlining paper and experiments
  * Pre-new data: Prediction train, 16fp vs 32 fp, test on full/512 size images
  * Post-new data: Train 512: change detection, domain knowledg
  * Separate (unpublished): FDN full
  * Paper: Abstract/Intro, Dataset, Method (models, loss), Implementation (hyper param), Experiments, Conclusion
0100-0120
* Research cuda() in separate scope to manage memeory issues
0120-0150
* Fix issue in the code with memeory issues in isolating Train/Val cuda()
0150-0213
* Run 16fp vs 32 fp experiment
0213-0249
* AIdash 2.0
  * Submodule updates
  * Learning gridspec API
0249-0317
* Loop display, aspect ration, prototpye
* Move sorted_listdir to util
0317-0352
* Understand git submodule update procedure
* Move listdir code and add parameters into ytil
0353-0433
* Test on full and 512 image
* Make code in lulc
* Test memory constraints. Can't run the entire size image but can run around 3000x3000
* Getting testing imgs of various size
0433-0500
* Fixed stitching bug by skipping parsing of every other row/col
0500-0533
* Additional issue with stiching, fixiing
* Planning development of prediction combining
  * Store predictions as pickle
  * Manage data on CPU
* Investigate RAM upgrade test order 8gb ddr registered server memory
0533-0600
* Investigation and preliminary report on predicting on 3000x3000
  * Seems to work better in certain cases


# 11/29
0900-0920
* time logging/email
0920-1029
* Inspect lbl data
  * 251 building farm greenhouse ->  combine with 230
  * 252 orchid/forest-like -> combine with 240
  * 140 rec includes building/fields -> combine with 100 - road category
1029-1100
* Compile fixed datase
* run test
1100-1200
* Plan experiment organization
* Data manager redesign
0100-0120
* Verify exp with fixed labels
* DAN trn aug has higher acc with new labels and wrong labels
0120-0215
* Migrating code to CK_GPU to test fdn_full
0215-0250
* Running FDN_full
  * Inspect data
0250-0400
* Add gpu options
* add options to organize experiment
* FDN_full epoch 2 same max score
0400-0500
* Add specify gpu functionality
* Add strbool parse for bool options
* Continuation
  * Load epoch continuation from train statistics
  * Load train stats when continuing training
0500-0600
* Modularize util into separate git module


# 11/28
0900-0920
* Email/timeloggin
0920-1000
* Batch prediction implementation. Speed up prediction 
1000-1100
* Ai-dash 2.0
* Fix naming issue
1100-1200
* Indvidual scoring implement
* Composition implement
0100-0120
* Found issue when combining tiles
0120-0200
* Individual scoring sorting and display
0200-0330
* Plot locations low scoring examples
  * Issue with symlink and PIL library
  * issue with subprocess with wildcard commands in bash
0330-0400
* Finished development made small report
* Meeting with Vasyl
0400-0530
* Planning and workflow breakdown
  * Promised expieriments
  * Bug fixes
  * Must do improvement
  * Paper writing and graphic types
0530-0600
* dataflow oraganization







# 11/27
0900-1210
* Presentation preparation
  * Tile output of different models
  * Setup demo script
1210-0150
* ETRI business trip
0150-0440
* Eterra meeting
0440-0500
* Email/ Organize workstation
0500-0520
* Time logging
0520-0530
* Business trip documentation
0530-0600
* Plan future steps


# 11/26
0900-0920
* Timelog/email
0920-0940
* Inspect training of FDN. New High score!
0940-1035
* Tile predictions
* Make presentation
* Debug Confusion matrix
1035-1135
* Contact Bioinformatics PhD
* Research paper on approaches A & B
   * Price of IDQ $53-82
1135-1145
* Clean workstation and files
1145-1200
* Debug conf. matrix
1200-0123
* Debug conf. matrix
  * Forgot to append rec label after creating keys examples.py
* Develop validation workflow
0123-0323
* Meeting with team leader for presentation
  * Reorder presentation 
  * Prepare demo
0323-0600
* Power point presentation create

# 11/25
0900-0930
* Timelogging and email
0930-1100
* Investigate issues with batch norm?
* NaN bias and weight at denseblock 2 lyr12 norm 1 & norm 2
* Nan bias and weight at denseblock 4 layer 26 norm 1 
1100-1200
* Debug FDN
  * Identified issue with aggr3  after ablation testing
0100-0230
* Reduced feature growth/size of aggr3 but NaN loss still happening
0230-0300
* Tried using multi-gpu dataparallel w/ apex amp but having issues need to investigate
0300-0330
* Found the FDN NaN loss issue
  * Problem was with branch 4 in aggr where ConvTranpose2D was outputting output padding of 0 causing some gradients to explode
0330-0400
* Fixed issue by replacing parameters in stride and padding for ConvTranpose2D
0400-0500
* Batch size is very small, 8, to train with the full model
* Reduce the model to FDN Mini by 
  * Reduce growth and layers in denseblock 5 & 6
  * Reduce feature aggr1 & aggr2 & aggr3
  * Reduce layers further and transition layer before deonseblock 5 & 6
* Create separate trainers and model for FDN Mini
0500-0520
* Train the FDN mini model
0530-0600
* Creating inverse of make_tiles to stitch together predictions

# 11/22
0900-0930
* Check boundary loss experiment
0930-1025
* Debug FDN Gradient
  * Issue with denseblock2 layer 4 norm 1
  * Printing out gradients
1025-1124
* Potential issue with vanishing gradeints after aggr1 and aggr2 working fine
* Implement multi-loss fnd_trainer.py to solve issues
1124-1200
* Investigate boundary loss attention function poly vs exp
  * Think exp is wrong in the paper
0100-0100
* Investigate batchnorm on multi-gpu sync
* TODO: Adjust code in dataloader.py to return cuda in main process
0140-0210
* refactor
* Create trainer for fdn adn deepaggr
0210-0220
* Plan future steps
  * test FDN
  * test exp attention w/ 4 dialation, baware loss
  * Additional channel 
  * generate prediction for entire map
0220-0310
* Design steps for exp attention. 
  * Need investigate something wrong with paper b/c exp doesn't decrease with correct prediction as apposed to poly
0310-0320
* Meeting for young adult business education 
0320-0530
* Power point creation 
* WBS weekly report
0530--0600
* FDN fully network debugging

# 11/21
0900-0921
* Time logging
0920-0953
* Inspect boundary aware loss training
* Compare conf. matrix
0953-1009
*  Adjusted boundary aware loss
* Testing
1000-1054
* Testing post processing with pix2pix
* Adjust model for single channel
* Out of Ram Issues while loading data
  * Solution, purchase more RAM/ Lower dataloader per training
1112-1200
* Running pix2pix. Not too promising
* Fix issue with clean_gan_data.py applying transfomration btw lbl and src
* Future: Add code to continue val.data and losses.data from crash
0100-0120
* Review GAN Clean. Not good
0120-0207
* Reading about CRF
0207-0250
* Meeting with President
* ETRI 11/27 Meeting (0100-0150)
* Report Sample from ETRI
  * list future development
  * remove code comments
0250-0500
* CRF (Conditional Random Fields) Research
0500-0600
* Fully Dense Net Vanishing gradient debugging



# 11/20
0900-0920
* Check Image Augmentation experiment (.5% Increase)
* Make report
0920-0935
* Time logging
0935-1110
* Test-time Augmentation design
  * work with PIL, NP, or Torch objects?
  * Decide on Torch to manipulate the whole batch since it is test time and memory shouldn't be an issue
  * Investiaate torch commands to transform D8.
* Testing torch commands to transform
1110-1130
* Meeting with Egor for Satellite image transform from orthographic to equiv-rect projection
  * Trying to pu the individual ortho maps into a unified coordinate system
1130-1200
* Debug D8 Augmentation
0100-0110
* Testing D4 and D4+S
  * 83.44% and 83.46%
* Fixed D8 inverse transformation increase about (.5%)
0110-0246
* GAN Post Processing
* Generate small dataset gan_data.create.py
0246-0300
* Read about boundary aware loss and image dilation
0300-0400
* Construct pipeline to compute boundary aware loss with masks
  * sum( weight*crossent( plbl*mask, lbl) )
0400-0416
* Freeze dialiation and sobel convolutions to prevent utility layers being backpropagated
0416-0504
* Inspect GAN post processing
  * Issue with GAUGAN outputting 3 channels
  * Need to display data separately since webviewer doesn't show masks
0504-0530
* Issue with GuaGan ignoring setting to output 3 channels
* Investigated code seems like issue goes deeper than intially expected
0530-0600
* Implement boundary aware loss


# 11/19
0900-0920
* Time logging
0920-0950
* Inspect results of training deeplabv3+
* Check email/respond
0950-1030
* Organize data report for deeplabv3+ max score 78%
* Construct a table report of all the experiments
1030-1200
* Implement Addaptive Aggregation 1 aggr.py
0100-0140
* Implement Addaptive Aggregation 2 & 3 aggr.py
0140-0300
* Finish build FDN
* Small issue with ConvTranpose2D
0300-0500
* Debugging layer channel mismatches
* Debugging  vanishing gradient/memory
  * Need to investigate further
0500-0600
* Integrate Image Augmentation into training pipeline dataloaders.py
* Fix small issue with ai-dash calling max on empty list aidash.py
* Run train aug training


# 11/18
0900-0600
* Vacation

# 11/15
0900-0910
* Check email
0910-0920
* results of experiment
0920-0940
* time logging/goal setting
0940-1000
* leaderboard for segmentation PASCAL
  * Dlabv3, pretrained on larger dataset (coco)
  * Fully Dense Neural Net  (FDN)
* leaderboard for segmentation COCO
1000-1100
* Setup dlabv3 for testing
1100-1140
* Debugging network/oom & adjust configuration
1140-1200
* Run dlabv3+ segmentation test
* Read FDN
0100-0112
* Option for mixed trianing added 
0100-0300
* Read FDN and dense net paper
0300-0340
* write report on preliminary design choices fdn.py
0340-0350
* Initial report on dlabv3+ train results
0350-0600
* Implement FDN


# 11/14
0900-0910
* Read email from prof JoYoel
  * What process led you to decide the biomarkers that you decided to use for the multivariate index assay?
    * Our long experience and test about 15 markers by MRM and then 5 by ELISA using antibodies developed by our group in-house.
  * Did you consider using the raw MS data to train the model?
    * We have not tried but it would be also worth to try. We used ELISA ans Kit quantified data to train the model.
  * What was the architecture of the deep learning model that you used?
    * Deep learning was helped by Dr. Sung-ho Won in SNU.  He is the one who can answer. 
0910-0930
* Time logging
0930-0936
* Print pdf from professor
0936-1029
* Investigate diff types of confusion matrix
1029-1133
* Split confusion matrix code into separate class, 
* Calculate from conf. matrixrecall and precision
1142-1200
* Display conf matrix with row col print
0100-0123
* Pretty print and format matrix print
0123-0241
* Meeting with 대표님
* Discussion goals
  * 1 Find out the cost of 180metabolite kit
  * 2 Contact biomarker research jung seung hyun
  * 3 prostate cancer other approaches
  * 4 literature review
0241-0318
* Plan future stages of Glycan project
0318-0441
* Train with full dataset
0440-0450
* Add try-catch for aidash for loading pickle exception
0450-0500
* Reporting for large experiment
0500-0530
* Meeting with Vasyl
0530-0540
* Debug issue with latest loss fix
0540-0600
* Plan future steps
  * GAN Clean
  * Domain Knowldedge
  * Alt models/ diff backbone
  * Test time Aug
  * Pre/Post processing
  * Select problematic examples

# 11/13
0900-0913
* Setup/email
0913-0925
* Time/logging module in training
0925-0940
* Time/logging/printing workflow testing
0940-1000
* Add progress class to keep track of batch, epoch and time remaining
1000-1015
* Issue with Guest profile on machine
1015-1040
* Meeting with Vasyl about plan/steps for project
1040-1100
* Combining Time/logging/printing/progress module into workflow
1100-1200
* Tested refactoring. Finished. Committing
0100-0300
* Glycan Research. Contact professors at ARGS conference
  * Je-Yoel Cho (Vetinary) jeycho@snu.ac.kr
  * Lung Cancer
  * MS analysis (Glyco-library)
  * Clinical trial (AUC .90)
  * Questions asked
    * What model used?
    * Initial considerations of biomarkers ?
    * Feed MS data direct ?
  * Taesung Park (Stats) tspark@stats.snu.ac.kr
  * Stats model
  * Oncology
  * Use some kit to find 188 metabolites and run various models
  * Questions asked
    * Considered using MS
    * What model ?
    * Overfitting ?
0300-0320
* Meet with Vasyl for testing train.py on cpu
  * Some issue with multiprocess dataloader
0320-0510
* Finish refactoring datasets
* Streamline data splitting into train/val
* Testing and committing
0510-0600
* Developing confusion matrix metric

# 11/12
0900-0913
* Timelogging
0913-0920
* Email
0920-0946
* Run half precision weights in full precision
  * Works fine
* Different procedure for reloading mixed training, amp.state, optimizer state, model state
0946-1009
* Investigating degeneration issues with mixed precision
1009-1100
* Code cleanup
  * train.py: refactoring all image processing code to util
  * testing changes
1100-1200
* Code cleanup
  * train.py: refactoring respective code to dataloader.py and option.py
  * testing changes
0100-0110
* Code cleanup
  * train.py: refactoring respective code to logger, evaluation
  * testing changes
0115-0124
* Meeting with Vasyl about issues in GeoImg data extraction library
0124-0207
* Debugging with Vasyl. Located issue in geoimg.py-margin_remove
* Problem 
  * Rasterio can't read localization tranformation from tiff image, setting it to identity
* Potential Causes
  * Version differences
* Check version differences with Vasyl and my env.
0207-0333
* Continuing to debug
  * Code works fine if it can find the correct transform
  * Reinstalling GDAL library to see if this is the cause
* Debugging matplotlib not showing on windows terminal
  * Need to add plt.show()
* Solution
  * Tiff file has additional file that was missing in Vasyl's env
0333-0500
* Code cleanup
  * train.py: refactoring respective code to evaluation.py
0500-0600
* Code cleanup
  * train.py: refactoring respective code to logger.py


# 11/11
0900-1000
* Time logging
1000-1013
* Goals for the week
  * Baseline mIOU, pixel accuracy
  * Confusion Matrix
  * Top 3 prediction accuracy
1013-1040
* One hot encoding and sum reduce
* Add validation scoring for entire batch per epoch
1040-1133
* mIOU testing and graphing for AI dashboard
* mIOU bit misleading due to giving high scores for labels that are not present
1133-1200
* Debugging and testing mIOU
0100-0140
* Amp scale investiate high loss when rescaling
  * Potential solution to ignore loss graphing when scaling loss?
0140-0300
* Debugging mIOU loss
* Implemented/testing pixel accuracy
* Implemented per class mIOU
* Added graphing title option to AI dashboard
0300-0400
* Code cleanup and refactoring
* Creating global util class with
  * pickle, visual, metrics, conversion of tensors to specific formats
0400-0510
* design some possible way of debugging and visualizing tensors
  * pickle-save and load
* Debug issue with one hot encoding
0510-0600
* Inspect training with validation graph
* Add ylim parameter for AI dashboard
* Issue with mixed precision

# 11-8
900-935
* Investigating half precision issues
* crossentropyloss = NLLLoss(logSoftmax())
  * But one doesn't work in half precision
935-1010
* reduce=True is broken in NLLLoss
1010-1147
* F1 Score
* ROC/AUC
1147-1200
* Why is ROC a function of threshold?
100-209
* Dice vs IOU
  * Advantage that DICE is a metric
  * Deepglobe paper uses IOU
* Implement IOU
209-400
* Debug/fix issue with clamping labels
400-420
* implement mIOU and test
420-500
* Mixed precision training, cut memory by /2
* Increased batch size by x4 with multi gpu and half prec
* Establish baseline with mIOU
500-600
* Train GauGan/SPADE with mixed precision
* Small issue with custom function returning float
  * Fixed
* Running/Test training

# 11-7
900-915
* Business trip to glycoscience conference
915-600
* Papers presented:
* Regulatory Considerations for Development of Biotherapeutics
* Rapid Low-level Identification and Quantitation of Host Cell Proteins
* MS-based Structural Characterization for Biotherapeutics
* Improved Glycan Analysis for Characterization of Glycoproteins
* The Role of Advanced Technologies in the Detection and Management of Protein Aggregation During mAb Development and Manufacturing
* Advances and Roadblocks in Glycomic and Glycoproteomic analysis
* Sialylation and Fucosylation Changes of GGTA1/CMAH Knockout Pig Erythrocyte Membranes
* High-Valued Bioactive Ingredients Development using Glycosylation Technology
* Protein Metrics_BYOS platform
* Lung Cancer Biomarkers by Glycoproteome Analysis and IVD-MIA Development
* Tracing Human Brain Development using Integrated Multiomics Approach
* Statistical modeling and Data Mining for Disease Diagnosis using Biomarkers
* Evaluation and Utilization of Healthcare Technology

# 11/6
900-920
* Email
* KTX reciept
920-1020
* Fixe loss rate of cross entropy
* Adjust ignore label
* Testing. Still having issues with roads not displaying
* The distincting between medium & large buildings not as useful due to small window size 128?
  * The paper uses 128x128 and has a smaller resolution (30cm per pixel) than our (1m per pixel) so 2 things are true
    * Their 128x128 are more high resolution allowing a distinction btw medium/large
    * Our 128x128 contains more spatial information since it is low resolution
1020-1200
* Out of memory issue
* Investigating half precision
100-408
* Debugging
* Fixed issue with roads not showing
* Experiments with multi task conclusion
  * I think small, med, large distiction doesnt work so well in our dataset
  * Also, the loss suggested in the paper is not so good since it doesn't directly penalize for over-predicting since there isn't a direct gradient adjust other than a softmax
  * Perhaps I need to traing for a longer duration
408-427
* Multi-GPU training.
  * Incrased batch size by x2
427-600
* Debugging half precision training
* Issue with NaN loss
* See like NLLLikelyhood loss's reduction has issues in f16
  * Odd since nn.mean() reduces fine in f16 but doesn't respond well the backward()

# 11/5
900-915
* Email/planning
* Paper review
  * Guage equivalence condition, Neural ODE, NP
915-930
* GauGan check training/testing
930-1200
* Create small/medium/large building dataset and label
* Analyze distribution of building size
100-125
* Create a report of the building distributions
* Fix issue with GPUCKServer while training GauGan
125-207
* Future steps:
  * shadow adjust?
  * metric F1
  * graph based post processing
207-221
* Meeting with Vasyl for landcover project
221-302
* Added 4 branches in MultiTask Unet for buildings
300-400
* Not enough memory while training model. Finding solutions
  * Half precision training
  * Reduce batch size
  * Use smaller input 256x256->128x128
400-600
* Implement reduce batch, smaller input
* Added ignore index to training labels
* One hot encode and cross entropy loss

# 11/4
900-930
* Read glycan-Genomic report
930-1000
* Work trip report & reimbursement forms
1000-1113
* weekly time logging report
1113-1140
* Investigate and fix pylint ignoring settings on new buffer
1140-1200
* Email professor Yang from conference
  * Spatial transfomration networks
100-200
* GauGan download and start training
200-230
* GauGan check training/testing
* ResNext investigation
230-330
Test building detection net
* Issue with 2 positional input in a layer
400-447
* GauGan check training/testing
* resolve issue with loading saved state dict
* generate small report
447-510
* Plan future goals for landcover project
510-600
* Investigate segmentation

# 11/1
0900-0910
* GPUKServer 3.5T out of storage
  * Need to move code to NVME for now
0910-1000
* Homology recovery of motion
1000-1134
* Building detection neural network
1134-0100
* Meeting with president
0100-0200
* Lunch
0200-0244
* Planning business trip with Vasyl
* Meet 11:20  -> KTX -> Seoul Station -> Samseong Station 2:00
* Purchase tickets and grab contact information
0244-0300
* Registration card fill out
0300-0400
* Building detection network develop decoder
0400-0430 
* Last output prediction (Issue with Unet)
0430-0512
* Weekly report Eterra
0512-0540
* Completed building model need to test
0540-0600
* Print and review papers to be presented in conference
