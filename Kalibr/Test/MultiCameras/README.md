# Kalibr


The toolbox Kalibr is from Github ethz-asl/kalibr, more details can be found on [Wiki](https://github.com/ethz-asl/kalibr/wiki). Here shows how to run the demo multi-cameras calibration Using dynamic/static Dataset.


 
## Install
### Using the CDE package (only 64bit systems)

To remove the necessity of installing ROS and building the toolbox from source, a CDE package is provided that packs the toolbox and all its dependencies in a chroot-like environment. To install this package follow these steps:
1.Download the most recent package from the [Downloads](https://github.com/ethz-asl/kalibr/wiki/downloads) page.
2.Extract the archive using:
> tar xfvz kalibr.tar.gz

##  Run
###  Input
The tool must be provided with the following input:
1,ROS bag containing the image data
>--bag filename.bag

2,the calibration target configuration (see [Calibration targets](https://github.com/ethz-asl/kalibr/wiki/calibration-targets)) 
> --target target.yaml
 
###  Output
The calibration will produce the following output files:
1.Contains all plots for documentation.

>report-cam-%BAGNAME%.pdf 

2.Result summary as a text file.

>results-cam-%BAGNAME%.txt

3.Results in YAML format. This file can be used as an input for the camera-imu calibrator. Please check the format on the YAML formats page.

>camchain-%BAGNAME%.yaml

## Test
### Using dynamic Dataset
If it's only for camera calibration, a combination of static camera and moving calibration target is preferred. Make sure current filefolder containing ./cam0 and ./cam1 with left and right images inside respectively. Run command line below to create rosbag file.
>%RELATIVE PATH%/kalibr_bagcreater --folder cam0 --folder  cam1 --output-bag ./static.bag

 Choose your camera model correctly(pinhole projection / equidistant distortion/ omni projection / radial-tangential distortion are supported). Then the calibration can be started with:

>kalibr_calibrate_cameras --target target.yaml --bag static.bag --models pinhole-equi pinhole-equi --topics /cam0/image_raw /cam1/image_raw 

NOTE1: If you want more detail information of projected error, add following python sparse option:

>--verbose

NOTE2: If you only want to choose part of video, for example, 5 seconds to 45 seconds, type below option

>--bag-from-to 5 45
 


 