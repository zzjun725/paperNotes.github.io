## Location Learning for AVs: LiDAR and Image Landmarks Fusion Localization with Graph Neural Networks

### Idea

Our main contributions are summarized as follows:

1. We introduce a new landmark map technique where roadside static landmark patches and the LiDAR points projected on them are organized in a graph for calibration.
2. We propose a learning-based localization method for AVs that consists of the localization neural network (LNN) and the landmark objects matching neural network (LOMNN), which is based on graph attention mechanisms.
3. We conduct comparisons to demonstrate that our learning-based localization framework achieves the state-of-the-art performance for the vehicular self-localization task.

More specifically, we use Resnet [14] to extract features from visual image patches and PointNet [15] to extract features from LiDAR points over the patches. The vehicle’s location is estimated from MLP regression layers by comparing the matched pairs of extracted features from the equipped sensors’ real-time measurements and the calibration landmark map.

**landmark map construction:** stable semantic segmentation masks for the camera images, such as static roadside landmark objects, including traffic lights, traffic signs, and poles.

**LOMNN:** Find the matching pair of landmarks(each is described as a graph, output is if a node is matched)

![image-20230313100412740](D:\Documents\honkitProjects\Papers\SLAM\figures\GATLocalization1)

**LNN:** our localization neural network ( $\mathrm{LNN}$ ) will compare the features extracted from the matched landmark object pairs in $\mathcal{G}_t^x$ and $\mathcal{G}_t^y$ to do the localization regression. 

### Shortcomings

Network is too complicated?

Still need rough localization techniques to identify which partition the vehicle is in. 