

<p align="center">
    <h4 align="center"><a href="https://ieeexplore.ieee.org/abstract/document/11016806">📑 IEEE OJVT</a>  

    
</p>

## MMTraP: Multi-Sensor Multi-Agent Trajectory Prediction in BEV





Accurate detection and trajectory prediction of moving vehicles are essential for motion planning in autonomous driving systems. While traffic regulations provide clear boundaries, real-world scenarios remain unpredictable due to the complex interactions between vehicles. This challenge has driven significant interest in learning-based approaches for trajectory prediction. We present MMTraP: Multi-Sensor and Multi-Agent Trajectory Prediction in BEV. This method integrates camera, LiDAR, and radar data to create detailed Bird's-Eye-View representations of driving scenes. Our approach employs a hierarchical vector transformer architecture that first detects and classifies vehicle motion patterns before predicting future trajectories through spatiotemporal relationship modeling. This work specifically focuses on vehicle interactions and environmental constraints. Despite its significance, multi-agent trajectory prediction and moving object segmentation are still underexplored in the literature, especially in real-time applications. Our method leverages multisensor fusion to obtain precise BEV representations and predict vehicle trajectories. Our multi-sensor fusion approach achieves the highest vehicle Intersection over Union (IoU) of 63.23\% and an overall mean IoU (mIoU) of 64.63\%, demonstrating its effectiveness in utilizing all available sensor modalities. Additionally, we demonstrate vehicle segmentation and trajectory prediction capabilities across various lighting and weather conditions. The proposed approach has been rigorously evaluated using the nuScenes dataset. Results show that our method improves the accuracy of trajectory predictions and outperforms state-of-the-art techniques, particularly in challenging environments such as congested urban areas. For instance, in complex traffic scenarios, our approach achieves a relative improvement of 5\% in trajectory prediction accuracy compared to baseline methods.. This work advances vehicle-focused prediction systems by integrating multi-sensor BEV representation and interaction-aware transformers. Our approach shows promise in enhancing the reliability and accuracy of trajectory predictions for autonomous driving applications, potentially improving overall safety and efficiency in diverse driving environments.


## Our Overview 📑
Overview of an autonomous driving pipeline using multi-sensor input. Data from camera, radar, and LiDAR sensors is processed through perception, prediction, and planning stages to understand the environment, predict object motion, and generate a safe driving plan, followed by vehicle control decisions.

<img src="https://github.com/user-attachments/assets/b5946a03-0c43-4f82-b12a-e8610f596a83" width ="850">



## Our Contribution  ⚙️


- We introduce MMTraP, a multi-sensor fusion architecture for BEV perception in autonomous driving. MMTraP combines data from cameras, LiDAR, and radar using a transformer-based framework to improve multi-vehicle trajectory prediction.

- Our approach effectively enhances moving object segmentation (vehicles only) accuracy in BEV space by combining data from multiple sensors. We conduct a detailed ablation study comparing unimodal and multimodal sensor configurations for vehicle segmentation at various distances. 
    
- We integrate a hierarchical attention mechanism \cite{zhou2022hivt} that captures both local and global context in the BEV representation, improving multi-vehicle trajectory predictions.

- MMTraP achieves state-of-the-art results in vehicle segmentation and trajectory prediction across diverse conditions.
    


    

## Our proposed architecture ⛓️
The MMTraP architecture integrates data from multi-view cameras, LiDAR, and radar to produce a unified BEV representation. Camera features are transformed into BEV. LiDAR and radar data are processed into voxel-based features and flattened into BEV representations. These BEV features are fused, encoded, and used for motion segmentation to identify moving agents. A hierarchical attention mechanism models interactions between agents and the ego vehicle. Finally, a decoder predicts multi-agent trajectories for safe and efficient autonomous navigation.


<img src="https://github.com/user-attachments/assets/e96a96f3-4c37-4c98-94e0-cc12d0479d85" width ="850">








## 📊 Ablation Study 
Comparison of various methods for vehicle segmentation on the nuScenes dataset, including our proposed approach. The evaluation is based on IoU scores (\%) for the BEV segmentation task. $\dagger$ Methods marked with a symbol are originally designed for different tasks (e.g., object detection), but are included here for comparison in the context of segmentation performance.
- ### BEV Performance Comparison


| **Method**         | **Sensor Modality** | **Vehicles ↑** | **Drivable Area ↑** | **Lane ↑** | **mIOU ↑** |
|--------------------|---------------------|----------------|----------------------|------------|-------------|
| OFT                | C                   | 30.1           | 72.2                 | 16.9       | 39.7        |
| LSS                | C                   | 32.1           | 74.1                 | 18.8       | 41.7        |
| FIERY              | C                   | 35.8           | -                    | -          | -           |
| CVT                | C                   | 36.0           | 74.3                 | 29.4       | 46.6        |
| CoBEVT             | C                   | 37.1           | -                    | -          | -           |
| **MMTraP (Ours)**  | C                   | **37.9**       | **75.5**             | **30.5**   | **47.9**    |
| CenterFusion†      | C+R                 | 46.5           | -                    | -          | -           |
| FUTR3D†            | C+R                 | 46.6           | -                    | -          | -           |
| Simple-BEV         | C+R                 | 55.7           | -                    | -          | -           |
| **MMTraP (Ours)**  | C+R                 | **58.16**      | **70.23**            | **39.20**  | **53.88**   |
| PointPainting†     | C+L                 | 60.2           | 75.9                 | 41.9       | 59.3        |
| Simple-BEV         | C+L                 | 60.8           | -                    | -          | -           |
| BEVFusion          | C+L                 | -              | 85.5                 | 53.7       | -           |
| **MMTraP (Ours)**  | C+L                 | **62.86**      | **85.67**            | 43.24      | **62.51**   |
| BEVMOSNet          | C+R+L               | 61.82          | -                    | -          | -           |
| **MMTraP (Ours)**  | C+R+L               | **63.23**      | **85.78**            | **44.90**  | **64.63**   |


- ### Vehicle Class Segmentation Performance under Varying Conditions

Our proposed method (MMTraP) performs reliably under varying lighting and weather conditions due to multi-sensor learning.  
The table shows vehicle class segmentation IoU (%) for Camera, Radar, and Lidar.  
`Abs. Diff.` refers to the absolute difference between conditions.

| **Sensor Modality**         | **Day** | **Night** | **Abs. Diff.** | **Sunny** | **Rainy** | **Abs. Diff.** |
|-----------------------------|---------|-----------|----------------|-----------|-----------|----------------|
| Camera                      | 39.8    | 21.1      | 18.7           | 37.8      | 28.3      | 9.5            |
| Camera + Lidar              | 62.8    | 47.5      | 15.3           | 61.8      | 54.4      | 7.4            |
| **Camera + Lidar + Radar**  | **63.8**| **52.3**  | **11.5**       | **64.3**  | **57.7**  | **6.6**        |



- ### nuScenes Evaluation – 6-Second Prediction Horizon

**Metrics:** Minimum Average Displacement Error (**MinADE**) and Final Displacement Error (**MinFDE**).  
Best results are marked in **bold**, second-best in *italics*.

| **Method**          | **MinADE₅ ↓** | **MinADE₁₀ ↓** | **MinADE₁₅ ↓** | **MinFDE₅ ↓** | **MinFDE₁₀ ↓** | **MinFDE₁₅ ↓** | **MissRate₅,₂ ↓** | **MissRate₁₀,₂ ↓** |
|---------------------|---------------|----------------|----------------|----------------|-----------------|-----------------|--------------------|---------------------|
| Const. Vel and Yaw  | 4.61          | 4.61           | 4.61           | 11.21          | 11.21           | 11.21           | 0.91               | 0.91                |
| Physics oracle      | 3.69          | 3.69           | 3.69           | 9.06           | 9.06            | 9.06            | 0.88               | 0.88                |
| CoverNet            | 2.62          | 1.92           | 1.63           | 11.36          | -               | -               | 0.76               | 0.64                |
| Trajectron++        | 1.88          | 1.51           | -              | -              | -               | -               | 0.70               | 0.64                |
| MTP                 | 2.22          | 1.74           | 1.55           | 4.83           | 3.54            | 3.05            | 0.74               | 0.67                |
| MultiPath           | *1.78*        | 1.55           | 1.52           | *3.62*         | 2.93            | 2.89            | 0.78               | 0.76                |
| MHA-JAM             | 1.85          | *1.24*         | **1.03**       | 3.72           | *2.23*          | *1.67*          | *0.60*             | **0.46**            |
| **MMTraP (Ours)**   | **1.59**      | **1.14**       | *1.09*         | **3.59**       | **2.09**        | **1.59**        | **0.53**           | *0.48*              |








## Qualitative results 📈

Qualitative outcomes of our model (BEVSeg2GTA): The six camera perspectives of nuScenes surrounding the vehicle are shown, with the top three facing forward and the bottom three facing backward. Ground truth segmentation is displayed on the right. Our trajectory prediction approach integrates improved map-view segmentation with ego vehicle trajectory (second from the right), and it is compared to the LSS method  and the CVT method  (third and fourth from the right)

<img src="https://github.com/user-attachments/assets/cf023e34-fbc3-46dd-9ad8-bd5ac6efb9af" width ="650">




## 📄 Citation

If you find this work useful, please cite:

```bibtex
@ARTICLE{10679361,
  author={Sharma, Sushil and Das, Arindam and Sistu, Ganesh and Halton, Mark and Eising, Ciarán},
  journal={IEEE Access}, 
  title={BEVSeg2GTA: Joint Vehicle Segmentation and Graph Neural Networks for Ego Vehicle Trajectory Prediction in Bird’s-Eye-View}, 
  year={2024},
  volume={12},
  pages={132159--132174},
  doi={10.1109/ACCESS.2024.3459595}
}





