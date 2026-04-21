<div align="center">
  
  ## Open-Set Writer Identification
  ### AC-GANs, Pressure Maps & Anomaly Detection

  <p align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/1/10/PyTorch_logo_icon.svg" alt="PyTorch" width="45"/> &nbsp;&nbsp;&nbsp;
    <img src="https://upload.wikimedia.org/wikipedia/commons/3/32/OpenCV_Logo_with_text_svg_version.svg" alt="OpenCV" width="40"/> &nbsp;&nbsp;&nbsp;
    <img src="https://upload.wikimedia.org/wikipedia/commons/0/05/Scikit_learn_logo_small.svg" alt="Scikit-Learn" width="60"/> &nbsp;&nbsp;&nbsp;
    <img src="https://upload.wikimedia.org/wikipedia/commons/e/ed/Pandas_logo.svg" alt="Pandas" width="80"/>
  </p>

  <p align="center">
    <a href="https://www.kaggle.com/"><img src="https://img.shields.io/badge/Kaggle_Rank-27th-20BEFF?style=for-the-badge&logo=kaggle&logoColor=white" alt="Kaggle Rank"></a>
    <img src="https://img.shields.io/badge/Macro_F1_Score-0.42593-4CAF50?style=for-the-badge" alt="F1 Score">
    <img src="https://img.shields.io/badge/IIT_Patna-AI_%26_DS-E53935?style=for-the-badge" alt="IIT Patna">
  </p>
  
  <i>A metric learning approach to identifying biometric handwriting signatures and rejecting forgers.</i>
  <br><br>
</div>

This repository contains the code, experiments, and architectural progression for my submission to the **Writer Identification Competition**. The challenge required classifying handwritten text into one of 44 known writer identities, while simultaneously identifying and rejecting forged or unknown writers (the `-1` class). 

Achieved **Rank 27** on the private leaderboard with a Macro F1 Score of **0.42593**

---

### The "Stranger Problem" & Open-Set Recognition

> **The Core Challenge:** *How do you teach a neural network to recognize someone it has never seen before?*

Standard deep learning classifiers are fundamentally designed for **closed-world problems**-they are forced to put every input into a predefined box.

| The Flaw of Standard CNNS | Our Anomaly Detection Paradigm | 
| :--- | :--- | 
| When faced with an unknow writer (`-1`), a standard CNN confidently **forces the stranger** into whichever known class has the most similar geometric shapes (e.g., *"They both draw loops, so it must be writer 14"*). | We engineered our pipeline to act as an **Anomaly Detector**. Instead of trying to memorize strangers, we mapped the strict biometric boundaries of our 44 known writers and treated anything outside those bounds as an anomaly. |

<br>
<div align="center">
  <img src="https://img.shields.io/badge/Paradigm_Shift-Spatial_Shapes_to_Biometric_Physics-FF9800?style=for-the-badge" alt="Paradigm Shift">
</div>
<br>
