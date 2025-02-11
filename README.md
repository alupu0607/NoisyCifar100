# **Noisy CIFAR-100: Training Deep Networks with Noisy Labels**

## **Overview**
This repository contains the implementation of an **Ablation Study** on training deep learning models on the **Noisy CIFAR-100** dataset. The study evaluates four different frameworks that incorporate **ELRPlusLoss**, **co-teaching-like consistency losses**, and **data augmentations (Cut-Mix & Mix-Up)** to improve robustness against noisy labels.

The repository includes **four different .ipynb files**, each corresponding to a specific framework tested in this ablation study.

---

## **Objective**
The goal of this study is to **train a deep learning model on the Noisy CIFAR-100 dataset** while leveraging techniques to counteract label noise.

### **Rules & Constraints:**
✅ **Training or fine-tuning** must be performed on the **Noisy CIFAR-100 dataset**.  
❌ **Pretrained models on CIFAR-100 are NOT allowed.**  
✅ **Models pretrained on ImageNet or CIFAR-10 are permitted.**  

---

## **Dataset Analysis & Noise Characterization**
The **CIFAR-100N** dataset was analyzed to identify noise patterns:
- **Visual Inspection**: Found clear **mislabeling patterns**, especially between visually similar classes.
- **Noise Transition Matrix**: Revealed structured **asymmetric noise patterns**.
- **Top Asymmetric & Symmetric Noise Pairs**: Identified systematic label corruption (e.g., "worm" → "snake").

💡 **Findings**: The dataset has **predominantly asymmetric noise**, reinforcing the need for robust noise-handling methods.

---

## **Ablation Study Frameworks**
- 0️⃣ **Provided Baseline** (Provided by the teachers, not included here - One Network with no noisy-specific strategies) - 0.12%
- 1️⃣ **Baseline (One Network with ELRPlusLoss)** - 41.03%
  
  The training and validation accuracy plots for
this framework exhibit extremely chaotic behavior and obvious overfitting
- 2️⃣ **One Network with ELRPlusLoss + Cut-Mix/Mix-Up** - 46.58%
  
  The introduction of Cut-Mix or Mix-Up augmentations leads to an improvement in both training and validation accuracy, as seen in the
more stable and steadily increasing plots. Validation loss decreases more consistently, demonstrating
enhanced generalization. However, as a single-network setup, it still struggles with robustness in highly
noisy environments compared to multi-network approaches. It seems to be smoother than Framework
3, even though the results are worse.
- 3️⃣ **Two Networks with ELRPlusLoss + Cross-Entropy Co-Teaching** - 46.62%
  
  The plots for training accuracy show a notable improvement in stability compared to single-network frameworks. Validation
  accuracy stabilizes earlier and reaches higher values, while validation loss exhibits fewer fluctuations.
  The co-teaching mechanism effectively enforces consistency between the two networks, enhancing robustness
  against label noise and stabilizing learning dynamics. Significant drop in loss and accuracy
  are observed, followed by a sudden increase. This framework is unstable.
- 4️⃣ **Two Networks with ELRPlusLoss + Cross-Entropy Co-Teaching + Cut-Mix/Mix-Up** - 51.57%
  
  The most comprehensive framework achieves the best performance, as evidenced by the smooth and stable
  training accuracy curve and the highest validation accuracy across all frameworks. Validation loss
  reduces consistently and stabilizes at lower levels, demonstrating the synergistic effect of co-teaching
  and augmentations. This setup exhibits the greatest robustness to noise, with training and validation
  metrics reflecting high stability and generalization.

---

### 📊 **Key Results**
- **The most advanced framework (#4) demonstrated the highest accuracy and robustness**, proving its effectiveness in handling **40% asymmetric noise**.
- **ELR+ (Early Learning Regularization Plus)** is used as a primary loss function, inspired by its computational efficiency and success in previous research.
- **Cut-Mix and Mix-Up augmentations** significantly improved generalization and the ac.
- **Cross-Entropy consistency loss** was incorporated to mimic co-teaching while avoiding direct sample selection.


---

## **Future Work**
🔹 Integrating **semi-supervised learning** to utilize **both labeled and unlabeled data**.  
🔹 Using **GMM clustering** and more sophisticated **noisy-clean data separation**.  
🔹 Exploring additional **loss functions and augmentations** for noise mitigation.  

---


