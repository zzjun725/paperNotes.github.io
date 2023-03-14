## Keys

SLAM not require integrating IMU data and solely rely on 3D point clouds.

Simple, Accurate, and Generalized(same parameter for different LiDAR sensors) Registration for Point-to-Point ICP.

![image-20230313234031147](.\figures\kissICP.jpg)



## Idea

**Step 1: Motion Prediction and Scan Deskewing**

The point cloud registration for mobile robots should not be considered as registration in two arbitrary point clouds. We use constant velocity model(assume accl can be ignored in a short time interval) to estimate the robot motion.

Within the acquisition time $\Delta t$ of one LiDAR sweep, multiple 3D points are measured by the scanner. The relative timestamp $s_i \in[0, \Delta t]$ for each point $\boldsymbol{p}_i \in \mathcal{P}$ describes the recording time relative to the scan's first measurement. This relative timestamp allows us to compute the motion compensation resulting in a deskewed point $\boldsymbol{p}_i^* \in \mathcal{P}^*$ of the corrected scan $\mathcal{P}^*$ reading by
$$
\boldsymbol{p}_i^*=\operatorname{Exp}\left(s_i \boldsymbol{\omega}_t\right) \boldsymbol{p}_i+s_i \boldsymbol{v}_t
$$
 **Step 2: Point Cloud Subsampling**

Downsampling is done using a voxel grid. As we will explain in Sec. III-C below in more detail, we use a voxel grid as our local map, where each voxel call has a size of $v \times v \times v$ and each cell only store a certain number of points. Every time we process an incoming scan, we first downsample the point cloud of the scan to an intermediate point cloud $\mathcal{P}_{\text {merge }}^*$, which is later used to update the map when the relative motion of the robot has been determined with ICP. To obtain the points in $\mathcal{P}_{\text {merge }}^*$, we use voxel size $\alpha v$ with $\alpha \in(0.0,1.0]$ and keep only a single point per voxel.

**Step 3: Local Map and Correspondence Estimation**

**Adaptive Threshold for Data Association**

**Step 4: Alignment Through Robust Optimization**