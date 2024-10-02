# Modular YOLOv8 Optimization for Real-Time UAV Maritime Rescue Object Detection

This repository contains the configuration files and core code for the paper *Modular YOLOv8 Optimization for Real-Time UAV Maritime Rescue Object Detection*, which is currently under peer review. The study is based on the YOLOv8 framework and proposes a modular optimization approach designed to improve real-time detection performance in UAV-based maritime rescue tasks. The provided code and configuration files can be used to reproduce the experimental results and support further research and extensions.

This project uses the **SeaDronesSee Object Detection** dataset, which is specifically designed for UAV-based maritime rescue scenarios. For more detailed information about the dataset, including download links and annotations, please refer to the following resources:

- [SeaDronesSee GitHub Repository](https://github.com/Ben93kie/SeaDronesSee)
- [SeaDronesSee Official Website](https://macvi.org/)

This project is built upon the YOLOv8 framework. For more information on the official YOLOv8 implementation, including installation instructions, pre-trained models, and documentation, please visit the official YOLOv8 repository:

- [YOLOv8 GitHub Repository](https://github.com/ultralytics/ultralytics)

The **YAML configuration files** for the YOLOv8 models presented in the paper can be found in the `cfgs` folder. These configurations are designed to support the modular plug-and-play architecture proposed in this project. The code for the **GAM module** (refer to the paper: https://arxiv.org/abs/2112.05561) and the **Swin Transformer module** (for the latest details, see https://github.com/WongKinYiu) is located in the `code` folder. The **CBAM module** has been integrated into the official YOLOv8 framework and can be utilized directly by modifying the YAML configuration files in this project.



**Usage Guide**

1. Import the `GAM` and `SwinTransformer` modules in `ultralytics/nn/modules/tasks.py`. 
2. Modify the `parse_model` function in `ultralytics/nn/modules/tasks.py` by updating the code under the `"if m in ..."` condition to include the `GAM` and `SwinTransformer` modules. The modified code should look like:
   
   ```python
   if m in {
       ...
       GAM,
       SwinTransformer,
       ...
   }
   ```
   
   This ensures that these modules defined in the YAML configuration files are correctly converted to PyTorch models. 
3. The **CBAM** module is already integrated into the official YOLOv8 framework and can be referenced directly in the YAML configuration without additional code changes.
4. YAML configuration files that support the ablation experiments in the paper, incorporating the **GAM**, **CBAM**, and **SwinTransformer** modules, are provided in the `cfgs` folder. These files can be used for training and evaluating models by following the standard instructions provided in the YOLOv8 documentation.