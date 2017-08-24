##Camera model

###Projective model for Omni camera.
euclidean point (x,y,z),  key point(x',y'), image point (u,v),$x_{i}=1.0$ by default
$$d=\sqrt{x^{2}+y^{2}+z^{2}}$$
$$r_{z}=1/(z+d*x_{i})$$
 $$x'=r_{z}x $$
$$ y'=r_{z}y$$
$$(x'',y'')=Distort(x',y')$$
$$u=fu\cdot x''+cu$$
$$v=fv \cdot y''+cv$$
###Unrojective model for Omni camera.
euclidean point (x,y,z),  key point(x',y'), image point (u,v),$x_{i}=1.0$ by default
$$x''= (u-cu)/fu$$
$$y''=(v-cv)/fv$$
$$(x',y')=Undistort(x'',y'')$$
$$r=\sqrt{x''^{2}+y''^{2}}$$
$$ z'=1-x_{i} (r+1)/(\sqrt{1+(1-x_{i}^{2})r}+x_{i})$$

###Projective & unprojective model for pinhole camera.
these two models can be found on [OpenCV](http://docs.opencv.org/2.4/modules/calib3d/doc/camera_calibration_and_3d_reconstruction.html) 
##Distortion model
###Distortion model for equidistant camera.
keypoint(x',y'),  and (x'', y'') are corresponding distorted keypoints.
$$r=\sqrt{x'^{2}+y'^{2}}$$
$$ \theta=atan(r)$$
$$\theta_{d}=\theta(1+k_{1}\theta^{2}+k_{2}\theta^{4}+k_{3}\theta^{6}+k_{4}\theta^{8})$$

$$
s=
 \begin{cases}
   1 &\mbox{if r=0}\\
   \theta_{d}/r &\mbox{if r>0}
   \end{cases}
$$
$$x''=sx' $$
$$ y''=sy'$$

###Undistortion model for equidistant camera.
keypoint(x',y'),  and (x'', y'') are corresponding distorted keypoints.
$$r=\sqrt{x''^{2}+y''^{2}}$$
$$ \theta=\theta_{d}$$
for(i=20;i>0;i--){$$\theta=\theta_{d}/(1+k_{1}\theta^{2}+k_{2}\theta^{4}+k_{3}\theta^{6}+k_{4}\theta^{8})$$}
$$s=tan(\theta)/\theta_{d}$$
$$x'=sx''$$
$$y'=sy''$$
###Distortion model for FOV camera.
keypoint(x',y'),  and (x'', y'') are corresponding distorted key points.$w=1.0$ by default
$$r=\sqrt{x''^{2}+y''^{2}}$$
$$\upsilon =tan(w/2)$$
$$ \eta =atan(2\upsilon \cdot r)$$

$$
s=
 \begin{cases}
   1 &\mbox{if w=0}\\
   2 \upsilon /w&\mbox{if w>0,r=0}\\
  \eta /(r \cdot w)&\mbox{if w>0,r>0}
   \end{cases}
$$
$$x''=sx'$$
$$ y''=sy'$$
###Undistortion model for FOV camera.
keypoint(x',y'),  and (x'', y'') are corresponding distorted key points.$w=1.0$ by default
$$\nu=2tan(w/2)$$
$$r=\sqrt{x''{2}+y''^{2}}$$
$$
s=
 \begin{cases}
   tan(rw)/(r \nu) &\mbox{if $\left | rw \right |$  $\leqslant$  MaxAngle}\\
   invalid&\mbox{if $\left | rw \right |$ > MaxAngle}
   \end{cases}
$$
$$x'=sx'' $$
$$ y'=sy''$$

###Distortion & undistortion  model for FOV camera.
these two models can be found on [OpenCV](http://docs.opencv.org/2.4/modules/calib3d/doc/camera_calibration_and_3d_reconstruction.html)  using distortion coefficients $$ [k_{1},k_{2},p_{1},p_{2}]$$