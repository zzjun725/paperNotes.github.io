# Differentiable SLAM-net: Learning Particle SLAM for Visual Navigation

(cvpr, 2021)

## Key

Concretely SLAM-net encodes the particle filter based FastSLAM algorithm and learns mapping, transition and observation models.

Learns RGB and RGB-D observation models for the encoded FastSLAM algorithm

Feature extractors can learn be more robust against domain specific challenges

CVPR Habitat 2020 PointNav challenge;  KITTI visual odometry data; simulation + three real-world indoor scene datasets



## Idea

Our algorithm is based on **FastSLAM**, and our differentiable implementation is built on **PF-nets**. The key feature of SLAM-net is that it is end-to-end differentiable. The **mapping**, **transition** and **observation** models are neural networks.

The algorithm works as follows. The particle filter maintains $K$ weighted particles, where each particle represents a trajectory $s_{0: t}^k$. At $t=0$ all particle trajectories are set to the origin; particle weights are constant, and the local map collection is empty. In each time step a mapping model predicts a local map $m_t$ from the input observation $o_t$, and $m_t$ is added to the collection. Particle trajectories are extended with samples from a probabilistic transition model that estimates the relative motion given $o_t$ and $o_{t-1}$. Particle weights are then updated using an observation model which measures the compatibility of $m_t$ and the past local maps $m_{1: t-1}$ assuming the particle trajectory $s_{0: t}^k$ was correct. The pose output is obtained by taking the weighted sum of particle trajectories. Optionally, a global occupancy grid map is obtained with simple 2D image transformations that combine local maps along the mean trajectory.