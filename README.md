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
<h2 align="center">🚀 Architectural Evolution & Methodology</h2>
<p align="center"><i>Progressing from physical feature engineering, through metric learning autopsies, to our highest-scoring adversarial architecture.</i></p>
<br>

### 🔹 Phase 1: Physical Biometrics (Pressure Maps)
> **Objective:** Prevent forgers from fooling the model by tracing spatial shapes.

<table width="100%">
  <tr>
    <th width="33%"><div align="center">🚧 The Hurdle</div></th>
    <th width="33%"><div align="center">🛠️ The Engineering Approach</div></th>
    <th width="33%"><div align="center">📈 The Impact</div></th>
  </tr>
  <tr>
    <td>Strangers and forgers can easily trace the geometric <i>shape</i> of a letter to fool a standard spatial CNN.</td>
    <td>Engineered <b>Kinematic Pressure Maps</b> via OpenCV to extract grayscale ink intensity, distance transforms (thickness), and stroke velocity.</td>
    <td>Proved that while forgers can fake shapes, they <b>cannot fake the biomechanical pressure</b> and speed of the original writer.</td>
  </tr>
</table>
<br>

### 🔹 Phase 2: Frequency Domain & Metric Learning
> **Objective:** Build a unified neural network to natively act as a biometric bouncer.

We converted the handwriting images into **2D Fourier Spectrograms** to isolate pure biomechanical "vibrations" (slant, tremors). We passed these through a **Siamese Network** to build 128-dimensional biometric "Islands" for known writers.

* **The Autopsy:** Standard Dense networks collapsed due to high-frequency scanner noise overpowering the biometric signal.
* **The Fix:** We engineered a **Multi-Scale Pyramidal Attention Network** that simultaneously looked at 16x16 (core), 32x32 (mid), and 64x64 (full) frequency lenses. It used an attention layer to dynamically route erratic vs. smooth writers into perfectly isolated clusters. 

<br>
<div align="center">
  <img src="https://img.shields.io/badge/The_Winning_Breakthrough-AC--GAN_Discriminator_Extraction-8A2BE2?style=for-the-badge" alt="The Breakthrough">
</div>
<br>

### 🔹 Phase 3: The Winning Architecture (AC-GAN Discriminator)
> **Objective:** Achieve the tightest possible open-set decision boundary to catch strangers.

While the Pyramidal Metric Network successfully built distance-based boundaries, our **highest Kaggle score** came from an advanced adversarial technique: **Extracting the Discriminator from an Auxiliary Classifier GAN (AC-GAN).**

<table width="100%">
  <tr>
    <td width="50%"><b>1. The Training</b><br>We trained an AC-GAN where the Generator learned to synthesize highly realistic handwriting conditioned on the 44 specific <code>writer_id</code>s.</td>
    <td width="50%"><b>2. The Adversarial Crucible</b><br>The Discriminator was forced into a brutal game. To survive, it had to learn the exact, imperceptible distribution of what makes Writer 14's handwriting <i>real</i> versus a hyper-realistic <i>fake</i>.</td>
  </tr>
  <tr>
    <td colspan="2">
      <b>3. The Extraction & Inference (Why it won)</b><br>
      Once training was complete, we discarded the Generator and deployed the <b>standalone Discriminator as our final Kaggle classifier</b>. Because it was trained to catch hyper-realistic fakes, its mathematical boundary around the 44 classes was incredibly tight. When a <code>-1</code> stranger was passed through the network, the Discriminator instantly recognized that the image fell outside the true learned manifold, yielding low auxiliary confidence and beautifully rejecting the unknown writer.
    </td>
  </tr>
</table>
<br>
