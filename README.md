

<p align="center">
    <h4 align="center"><a href="https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10679361">📑 IEEE Access</a>  
    
</p>

## BEVSeg2GTA: Joint Vehicle Segmentation and Graph Neural Networks for Ego Vehicle Trajectory Prediction in Bird's-Eye-View




Accurate detection and trajectory prediction of moving vehicles are essential for motion planning in autonomous driving systems. While traffic regulations provide clear boundaries, real-world scenarios remain unpredictable due to the complex interactions between vehicles. This challenge has driven significant interest in learning-based approaches for trajectory prediction. We present \textit{\textbf{MMTraP:}} \textbf{M}ulti-Sensor and \textbf{M}ulti-Agent \textbf{Tra}jectory \textbf{P}rediction in BEV. This method integrates camera, LiDAR, and radar data to create detailed Bird's-Eye-View representations of driving scenes. Our approach employs a hierarchical vector transformer architecture that first detects and classifies vehicle motion patterns before predicting future trajectories through spatiotemporal relationship modeling. This work specifically focuses on vehicle interactions and environmental constraints. Despite its significance, multi-agent trajectory prediction and moving object segmentation are still underexplored in the literature, especially in real-time applications. Our method leverages multisensor fusion to obtain precise BEV representations and predict vehicle trajectories. Our multi-sensor fusion approach achieves the highest vehicle Intersection over Union (IoU) of 63.23\% and an overall mean IoU (mIoU) of 64.63\%, demonstrating its effectiveness in utilizing all available sensor modalities. Additionally, we demonstrate vehicle segmentation and trajectory prediction capabilities across various lighting and weather conditions. The proposed approach has been rigorously evaluated using the nuScenes dataset. Results show that our method improves the accuracy of trajectory predictions and outperforms state-of-the-art techniques, particularly in challenging environments such as congested urban areas. For instance, in complex traffic scenarios, our approach achieves a relative improvement of 5\% in trajectory prediction accuracy compared to baseline methods.. This work advances vehicle-focused prediction systems by integrating multi-sensor BEV representation and interaction-aware transformers. Our approach shows promise in enhancing the reliability and accuracy of trajectory predictions for autonomous driving applications, potentially improving overall safety and efficiency in diverse driving environments.

## Our Overview 📑
The BEVSeg2GTA framework aims to enhance ego vehicle trajectory prediction by integrating an encoder-decoder transformer and a GNN. The framework begins with a projection module, which transforms the input multi-camera views and map information into a BEV perspective using an encoder-decoder transformer. The segmentation output from this module is then fed into the GNN, which is utilized to construct a graph representing spatial information. This graph is subsequently employed as input into an STPN, which produces predictions of the ego vehicle's trajectory.

<img src="https://github.com/user-attachments/assets/ba98c000-debc-44a3-bc9b-2865923b900c" width ="850">



## Our Contribution  ⚙️


-  Our  proposal architecture (\textbf{BEVSeg2GTA}) offers an approach to accomplish vehicle segmentation and ego vehicle trajectory prediction tasks jointly, thereby achieving state-of-the-art results in both segmentation and trajectory prediction compared on the nuScenes dataset.
-  Our proposal integrates GNNs into the BEV architecture to capture the spatial relationships of the host vehicle and nearby objects, where the weights of the connections are inverses of the distances.
-  STPN is then integrated for trajectory estimation, so our network proposal considers both spatial and temporal aspects of the problem.


    

## Our proposed architecture ⛓️
Our proposed BEVSeg2GTA architecture: Our method for jointly segmenting vehicles and predicting the trajectory of the ego vehicle consists of several stages. Initially, we extract image features across different scales and integrate a camera-aware positional embedding to address perspective distortion. Following this, we employ map-view positional embedding and cross-attention layers to gather contextual insights from various viewpoints and enhance the segmentation accuracy of the ego vehicle. The segmented results are then passed through a $k$NN to generate embeddings representing the surrounding environment. These embeddings are further utilized as input to a probabilistic layer for trajectory prediction, leveraging contextual information from the surrounding scene. Stars are used to indicate the novel contributions of this work (\textcolor{red}{red} and \textcolor{green}{green} indicating major and minor component contributions, respectively.

<img src="https://github.com/user-attachments/assets/f2287b30-3123-4085-8455-05eab78b23d1" width ="850">



    

## kNN Algorthim Analsis ⛓️
Exploring how changes in the parameter k, representing the number of nearest neighbors analyzed in the kNN algorithm, impact the connectivity and layout of nodes and edges in a graph. In the visualization, the red box indicates the ego vehicle, the blue boxes represent other agents in the scene, and the red dots denote the nodes.

<img src="https://github.com/user-attachments/assets/68ea478f-88bb-40e7-b3c6-97ec33042d47" width ="850">




## 📊 Vehicle Segmentation Results on nuScenes Dataset
We compare the performance of different methods for vehicle segmentation on the nuScenes dataset, including our proposed approach. The results are evaluated using Intersection over Union (IoU) for the BEV segmentation task.

| **Method**        | **Surround-View Camera** | **Input Image Size (px)** | **Feature Extractor** | **Grid Scale / Unit Size** | **FPS** | **Vehicle IoU (%) ↑** |
|-------------------|---------------------------|----------------------------|------------------------|-----------------------------|--------|-----------------------|
| PanSeg         | ✗                         | 448 × 768                  | EfficientDet           | -                           | -      | 35.06                |
| GitNet         | ✗                         | -                          | ResNet50               | 200×200 / 0.25m             | -      | 35.90                |
| M2BEV          | ✓                         | 900 × 1600                 | ResNeXt-101            | 200×200 / 0.5m              | -      | -                    |
| LSS            | ✓                         | 128 × 352                  | EfficientNet-B0        | 200×200 / 0.5m              | 25     | 32.1                 |
| CVT            | ✓                         | 200 × 200                  | EfficientNet-B4        | 200×200 / 0.5m              | 35     | 36.0                 |
| CoBEVT         | ✓                         | 200 × 200                  | EfficientNet-B4        | 200×200 / 0.5m              | 35     | 37.1                 |
| **Ours**       | ✓                         | 200 × 200                  | EfficientNet-B4        | 200×200 / 0.5m              | 35     | **37.9**             |



## 🚗 Trajectory Prediction Results on nuScenes Dataset
Evaluation of competing methods on the nuScenes dataset, analyzing Minimum Average Displacement Error (MinADE) and Final Displacement Error (MinFDE) over a 6-second prediction horizon.

| **Method**               | **MinADE₅ ↓** | **MinADE₁₀ ↓** | **MinADE₁₅ ↓** | **MinFDE₅ ↓** | **MinFDE₁₀ ↓** | **MinFDE₁₅ ↓** | **MissRate₍₅,₂₎ ↓** | **MissRate₍₁₀,₂₎ ↓** |
|--------------------------|---------------|----------------|----------------|---------------|----------------|----------------|----------------------|-----------------------|
| Constant Velocity & Yaw | 4.61          | 4.61           | 4.61           | 11.21         | 11.21          | 11.21          | 0.91                 | 0.91                  |
| Physics Oracle           | 3.69          | 3.69           | 3.69           | 9.06          | 9.06           | 9.06           | 0.88                 | 0.88                  |
| CoverNet             | 2.62          | 1.92           | 1.63           | 11.36         | -              | -              | 0.76                 | 0.64                  |
| Trajectron++         | 1.88          | 1.51           | -              | -             | -              | -              | 0.70                 | 0.64                  |
| MTP                  | 2.22          | 1.74           | 1.55           | 4.83          | 3.54           | 3.05           | 0.74                 | 0.67                  |
| MultiPath          | *1.78*        | 1.55           | 1.52           | **3.62**      | 2.93           | 2.89           | 0.78                 | 0.76                  |
| MHA-JAM             | 1.85          | *1.24*         | **1.03**       | 3.72          | *2.23*         | *1.67*         | *0.60*               | **0.46**              |
| **Ours**                 | **1.63**      | **1.19**       | *1.06*         | *3.63*        | **2.13**       | **1.65**       | **0.56**             | *0.51*                |

Bold = Best result, Italics = Second best
Missing values are marked with -

## Qualitative results 📈

Qualitative outcomes of our model (BEVSeg2GTA): The six camera perspectives of nuScenes surrounding the vehicle are shown, with the top three facing forward and the bottom three facing backward. Ground truth segmentation is displayed on the right. Our trajectory prediction approach integrates improved map-view segmentation with ego vehicle trajectory (second from the right), and it is compared to the LSS method  and the CVT method  (third and fourth from the right)

<img src="https://github.com/user-attachments/assets/39775418-9558-4fd0-80e5-c322c9e92c74" width ="650">



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





