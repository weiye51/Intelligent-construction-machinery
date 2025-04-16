# Intelligent-construction-machinery
## 1.Introduction
Autonomous crane control faces challenges in dynamic disturbance handling and complex loading/unloading operation environments. This study proposes Residuals Long Short-Term Memory Transformer(RLSTM-Transformer), an end-to-end autonomous driving model to enhance the trajectory prediction capabilities of crane systems. The model pioneers a dual-branch deep learning network for jointly optimizing local and global features. The upper branch combines a computational neural network and a delayed residual long short-term memory network to extract local spatiotemporal features from semantic image sequences and enhance the feature relevance. The lower branch uses a ResNet-Transformer network to capture global spatial dependencies from depth image sequences and establish global dependencies. During training, RGB/RGB-depth sequences and control signals were input. In the prediction process, real-time images generated control signals. Validation was performed on simulation and physical platforms. The results demonstrated that the proposed model enables end-to-end motion control of crane systems under complex operating conditions and external disturbances.

The code of this algorithm will be made public after publication in the journal

## 2.Datasets
You can get the crane dataset on Baidu Netdisk through the following link
Link: https://pan.baidu.com/s/1AwNVi8YbgLVM46q2_20GlQ Extraction code: d29t


The loading and unloading tasks of a crane refer to the process of lifting, moving, and placing materials or goods using the crane system. These tasks are widely applied in environments such as ports, warehouses, and construction sites. The main objective is to efficiently and safely complete the loading and unloading of goods.This study created two end-to-end intelligent decision-making datasets for crane operations:the simulated dataset and the RealCrane dataset.

The simulated crane data acquisition device operated through crane simulation software developed using the Unreal Engine, with the crane's movements controlled by a joystick and buttons on the seat,video frames of crane operation scenes and the corresponding joystick output signals from the operator's console were collected using a simulated crane driving platform.The video frames were saved as images at a certain frame rate and named with the current timestamp. The SimCrane simulated crane dataset contained 41,891 RGB images, 41,891 corresponding semantic images, and the operation control command labels for the operation end of each image, with an image size of 210 × 160. The dataset included 100 groups (100 completed crane loading processes) of data. During training, 15 consecutive image frames were used as a single sample, and the dataset contained 2,793 image sequences.To enhance the model's robustness and generalizability, data was collected from two crane operation scenarios: container crane sand loading and unloading and container crane coal pile loading. The dataset contained comprehensive data for different materials, cranes, and relative positions of the materials and vehicle buckets. Figure 1 shows the simulated data collection device. During the data collection phase, controller output signals with time information were saved using serial monitoring software. The crane driving scene images and control quantities were aligned using timestamps, and the decision-making was based on the images that underwent semantic segmentation. During operation, the operator needed to simultaneously control the joystick and the grab control to complete the task. Figure 2 shows a schematic diagram of the RGB image sequence from the SimCrane dataset. Figure 3 shows a schematic diagram of the semantic label image sequence from the SimCrane dataset. Figure 4 shows a schematic diagram of the semantic overlay image sequence from the SimCrane dataset. Table 1 shows the label settings for the SimCrane dataset.

<div style="display: flex; justify-content: center; margin-bottom: 10px;">
    <img src="https://github.com/user-attachments/assets/3cd9917c-908f-46ea-88c9-7b48c24e5ec4" alt="Figure 1" style="height: 300px; width: auto;">
</div>
<div style="display: flex; justify-content: space-around;">
    <img src="https://github.com/user-attachments/assets/c2d29500-afa0-4646-9c4c-3ed71e2666f1" alt="Figure 2" style="height: 150px; width: auto;">
    <img src="https://github.com/user-attachments/assets/5492d6dd-7c55-4086-8e05-4edb428fa67a" alt="Figure 3" style="height: 150px; width: auto;">
    <img src="https://github.com/user-attachments/assets/ce271dc2-d975-4d7c-9356-3c3b8331a300" alt="Figure 4" style="height: 150px; width: auto;">
</div>


| Joystick Movement                                      | Label |
|---------------------------------------------------------|-------|
| Shift Right Gear 1 to 5, Increase Gear 1 to 5           | 0     |
| Shift Up Gear 1 to 5                                   | 1     |
| Hoist Lower                                             | 2     |
| Hoist Lift                                              | 3     |
| Shift Left Gear 1 to 5, Decrease Gear 1 to 5            | 4     |
| Hoist Lower                                             | 5     |
| Shift Right Gear 1 to 5, Decrease Gear 1 to 5           | 6     |
| Shift Left Gear 1 to 5, Increase Gear 1 to 5            | 7     |

The RealCrane dataset was collected on a gantry crane experimental platform, during which the crane's loading and unloading tasks on a sandpile were simulated. The image acquisition device used was a Kinect sensor. The crane detected operator commands through switches, and the PLC program controlled the relay based on input signals to achieve motor control. Figure 5 is a schematic diagram of the crane's real experimental scene.The motion control commands on the operation end included: C1—Ascend, C2—Descend, C3—Increase Speed, C4—Decrease Speed, C5—Rotate Left, C6—Rotate Right, C7—Grab, C8—Release, and C9—No Command Input, totaling nine categories.Table 2 shows the label settings for the RealCrane dataset.The RealCrane dataset captured and saved the switch state signals at 10 FPS while recording timestamps to ensure synchronization between image data and switch signals. The dataset included 33,277 RGB images, 33,277 corresponding depth images, 33,277 semantic segmentation images, and 33,277 fused depth images with semantics, as well as the corresponding motion control commands for the operation end. The image resolution is 210 × 160. The dataset contained 100 groups of data (100 complete crane loading and unloading processes). During training, 15 consecutive RGB image frames were used as a single sample, and the dataset included 2,218 image sequences. Each frame of the semantic images was labeled with four semantic categories: background, material pile, grab, and vehicle bucket.To improve the robustness and generalization ability of the end-to-end network, images were captured under different lighting conditions and varying wind speed levels, and multiple sets of data were collected by adjusting the relative positions of the sand pile and vehicle bucket to increase the data diversity. At the same time, the depth of the grab during each lowering process was varied to achieve different material extraction qualities. The dataset included 40 groups of data simulating the effects of different wind speed levels. Figure 6 shows a schematic diagram of the RGB image sequence from the RealCrane dataset. Figure 7 shows a schematic diagram of the semantic label image sequence from the RealCrane dataset. Figure 8 shows a schematic diagram of the semantic overlay image sequence from the RealCrane dataset. Figure 9 shows a schematic diagram of the depth image sequence from the RealCrane dataset. 

<div style="display: flex; justify-content: center; margin-bottom: 10px;">
    <img src="https://github.com/user-attachments/assets/b372b04d-57c3-49da-8fef-500ef4a4433a" alt="Figure 5" style="height: 300px; width: auto;">
</div>
<div style="display: flex; justify-content: space-around;">
    <img src="https://github.com/user-attachments/assets/103ffa52-4c8e-43d5-ab84-06ec1627e7c8" alt="Figure 6" style="height: 150px; width: auto;">
    <img src="https://github.com/user-attachments/assets/282f1f0e-81de-4983-81c2-8b3616c518a2" alt="Figure 7" style="height: 150px; width: auto;">
    <img src="https://github.com/user-attachments/assets/c7a27c08-e603-473c-b838-8d59289a9b37" alt="Figure 8" style="height: 150px; width: auto;">
    <img src="https://github.com/user-attachments/assets/d20675bd-0b1a-48a8-9703-ebf6c20334bf" alt="Figure 9" style="height: 150px; width: auto;">
</div>


| Motion Control Command | Label |
|------------------------|-------|
| Right Rotation         | 1     |
| Left Rotation          | 2     |
| Lifting                | 3     |
| Lowering               | 4     |
| Forward Amplitude      | 5     |
| Backward Amplitude     | 6     |
| Grab Bucket Closed     | 7     |
| Grab Bucket Open       | 8     |
| No Command State       | 0     |


