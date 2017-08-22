# Kalibr


The toolbox Kalibr is from Github ethz-asl/kalibr, more details can be found on [Wiki](https://github.com/ethz-asl/kalibr/wiki). Here shows how to run the demo Camera-IMU calibration Using dynamic Dataset.


 
## Install
### Using the CDE package (only 64bit systems)

To remove the necessity of installing ROS and building the toolbox from source, a CDE package is provided that packs the toolbox and all its dependencies in a chroot-like environment. To install this package follow these steps:
1.Download the most recent package from the [Downloads](https://github.com/ethz-asl/kalibr/wiki/downloads) page.
2.Extract the archive using:
> tar xfvz kalibr.tar.gz

##  Run
###  Input
The tool must be provided with the following input:
>--bag filename.bag

1,ROS bag containing the image and IMU data
>--cam camchain.yaml

2. intrinsic and extrinsic calibration parameters of the camera system. The output of the multiple-camera-calibration tool can be used here. (see YAML formats) Make sure the frequency of imu is at least 100HZ~
    
>--imu imu.yaml

3.contains the IMU statistics and the IMU's topic (see YAML formats)
> --target target.yaml
    
4.the calibration target configuration (see Cailbration targets)
###  Output
The calibration will produce the following output files:

>report-imucam-%BAGNAME%.pdf

1.Report in PDF format. Contains all plots for documentation.
> results-imucam-%BAGNAME%.txt

 2.Result summary as a text file.
>camchain-imucam-%BAGNAME%.yaml

3.Results in YAML format. This file is based on the input camchain.yaml with added transformations (and optionally time shifts) for all cameras with respect to the IMU. Please check the format on the YAML formats page.

## Test
### Using dynamic Dataset
An example using a sample dataset

Download the dataset from the  [Downloads](https://github.com/ethz-asl/kalibr/wiki/downloads) page and extract **dynamic.rar**. The archive will contain the bag, calibration target and IMU configuration file.
Otherwise, you can create rosbag using your raw data, a combination of moving camera and static calibration target is preferred. Make sure current filefolder containing ./cam0 and ./cam1 with left and right images inside respectively and the image name is the same as timestamps in rostime format. And a imu0.csv file includes inertial sensor data as follows:

>timestamp, gyro.x,gyro.y, gyro.z,acc.x,acc.y,acc.z

Run command line below to create rosbag file.

>%RELATIVE PATH%/kalibr_bagcreater --folder cam0 --folder cam1 --output-bag ./dynamic.bag

The calibration can be started with:

>kalibr_calibrate_imu_camera --target april_6x6.yaml --cam camchain.yaml --imu imu_adis16448.yaml --bag dynamic.bag --bag-from-to 5 45

NOTE1: Because there are shocks in the dataset (sensor pick-up/lay-down), only the data between 5 to 45 s is used.
NOTE2: If **dynamic.rar** is extracted in other folder, add datasets'path before each extracted data.

NOTE3: If you want more detail information of projected error, add following python sparse option:

>--verbose

NOTE4: If you only want to choose part of video, for example, 5 seconds to 45 seconds, type below option

>--bag-from-to 5 45
 


 