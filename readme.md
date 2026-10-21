# DOA Estimation: No need for retraining! New breakthrough in geometrically invariant DOA estimation with microphone position encoding and progressive training, achieving both precision and efficiency leaps. [Python code attached]

Personal Blog: https://www.cnblogs.com/EWFrontier  
✿GI-DOAEnet: A New Breakthrough in Geometric Invariant DOA Estimation with Gradient-based Incremental Training  
1. Article Title: Geometry-Invariant Waveform Directivity Estimation Based on Deep Neural Networks: Microphone Position Coding and Gradient-based Incremental Training  
2. Abstract: In recent years, deep neural network (DNN)-based waveform direction of arrival (DOA) estimation methods have shown stronger robustness compared to traditional methods. However, most DNNs are designed for specific microphone arrays and require retraining when changing the geometric structure. Although some geometric invariant methods use traditional features, they suffer from high computational costs and susceptibility to interference. This paper proposes a geometry-invariant waveform direction of arrival estimation network (GI-DOAEnet), which is based on microphone position encoding (MPE) - modulating the spherical coordinates of the microphone by a sine function to provide unique geometric information. The network combines MPE with channel-level latent features, leveraging geometric invariant modules to capture spatiotemporal correlations and ultimately generate spatial spectra. To achieve effective training under multiple geometric structures, this paper introduces a complexity-gradual training (CGT) strategy, integrating deep supervised curriculum learning with a novel multi-stage geometric learning method, and gradually adjusting soft labels and array geometry (from fixed to dynamic) to increase task difficulty. Experiments show that GI-DOAEnet outperforms baseline methods in terms of angle error and accuracy across different acoustic environments, while reducing floating point operations (FLOPS) and inference time by abandoning pairwise features and adopting channel-level aggregation.
III. Introduction to DoA Estimation (DOA)
In recent years, DNN-based DOA estimation models have demonstrated stronger robustness in complex scenarios such as noise, reverberation, and simultaneous speech from multiple speakers. However, these models are typically designed for specific geometric structures of microphone arrays (fixed number and position of microphones), and fail to function when switched to different geometric structures. Due to the diverse geometric structures of microphone arrays in applications such as vehicles and wearable devices, and the urgent need for adaptive beamforming, such models require repeated training, which is time-consuming and laborious.
In tasks such as speech enhancement, separation, and recognition, researchers have proposed geometrically invariant DNNs that adapt to different microphone arrays through channel-invariant structures and batch processing, along with invariant operations (mean, summation, multi-head self-attention, etc.). However, these methods rely solely on the collected signals and cannot be directly used for DOA estimation—the microphone coordinates, serving as key geometric information affecting TDOA, are crucial for DOA estimation. Existing geometrically invariant DOA methods based on DNNs that incorporate geometric information, or reliant on traditional features like SRP-PHAT, or require the computation of GCC-PHAT features for microphone pairs, all face issues of quadratic growth in computational complexity with an increase in the number of microphones and susceptibility to interference.
For this purpose, this paper proposes GI-DOAEnet, which introduces geometric information through MPE without traditional pairwise features. At the same time, CGT strategy is designed to solve the convergence problem of multi-geometry structure training, and finally realizes high accuracy, high efficiency and strong generalization of DOA estimation.
IV. Method Introduction 1. Geometric Invariant DOA Estimation Network (GI-DOAEnet) GI-DOAEnet is a causal geometric invariant DOA estimation architecture, including core modules:
•  
STFT domain signal representation: Convert the signals from each channel into the STFT domain, concatenate the real and imaginary parts to obtain real-valued features, indirectly preserving the phase relationship related to TDOA.
•  
Channel Independent Feature Extractor (CIFE): By processing independently the latent features of each channel through batch processing, it avoids the high computational cost and interference issues of traditional pairwise feature extraction. The core consists of a normalization layer, convolutional block (CB), and residual convolutional block (RCB).
•  
Microphone Position Encoding (MPE): Vectorizes the spherical coordinates of a microphone (distance, azimuth, elevation) through sinusoidal function modulation (phase modulation PM, frequency modulation FM), without requiring learnable parameters, ensuring uniqueness and linear correlation for different microphone positions.
•  
Space-Time Dual Path Module (STDPB): Integrating MPE and CIFE output features, it captures channel correlation through Channel-wise Multi-Head Attention (CW-MHSA), and time correlation through Frame-wise Gated Recurrent Unit (FW-GRU). Coupled with Channel-wise Softmax Aggregation (CWSA), it enhances computational efficiency.
•  
Space Spectrum Mapping Block (SSMB): Using a deep supervision method, the spatial spectrum is generated through residual convolution blocks and Sigmoid function, with peaks corresponding to candidate DOA.
2. The complexity incremental training (CGT) strategy is designed to address the convergence difficulties of training with multiple geometric structures, gradually increasing the task complexity:
•  
Multi-stage Geometric Learning (MSGL): Divide into three stages of training - Stage 1: fixed a single microphone array, Stage 2: keep the number of microphones constant and dynamically adjust their positions, Stage 3: dynamically adjust the number of microphones (4-12 channels) and their positions, gradually adapting to complex geometric structures.
•  
Deep Supervised Learning (DSCL): Integrating Deep Supervision (different beam widths for different network layers with soft labels) and Course Learning (gradually narrowing the soft label beam width during training), guiding the model from vague to precise learning of spatial spectrogram.

Conclusion: This paper proposes GI-DOAEnet and CGT strategies, providing new solutions for geometrically sensitive tasks. The core innovation lies in microphone position encoding (MPE), which encodes spherical microphone coordinates into sinusoidal vectors, achieving the natural integration of geometric information and multichannel audio latent features for the first time, bridging the gap between DNN and array signal processing. The CGT strategy significantly enhances the model's robustness and generalization by progressively increasing the complexity of labels and array geometry, and this strategy also improves performance when applied to other baseline models, offering a new direction for geometrically sensitive learning tasks.
Experimental validation shows that GI-DOAEnet outperforms traditional methods and existing DNN methods in terms of estimation accuracy and computational efficiency under various microphone array configurations and acoustic scenarios, demonstrating its practical application value. Future work will extend the model to 3D sound source localization and mobile sound source tracking, and promote MPE and CGT strategies to other array signal processing tasks such as beamforming, further verifying their universality and effectiveness.
★
Permanent access to more relevant materials and code.

## Images

![(DOA Estimation)No need to retrain! New breakthrough in geometric invariant DOA estimation: microphone position encoding + progressive training, leaps in both accuracy and efficiency. [Includes Python code]](01.jpg)
![(DOA Estimation)No need to retrain! New breakthrough in geometric invariant DOA estimation: microphone position encoding + progressive training, leaps in both accuracy and efficiency. [Includes Python code]](02.jpg)
![(DOA Estimation)No need to retrain! New breakthrough in geometric invariant DOA estimation: microphone position encoding + progressive training, leaps in both accuracy and efficiency. [Includes Python code]](03.jpg)
![(DOA Estimation)No need to retrain! New breakthrough in geometric invariant DOA estimation: microphone position encoding + progressive training, leaps in both accuracy and efficiency. [Includes Python code]](04.jpg)
![(DOA Estimation)No need to retrain! New breakthrough in geometric invariant DOA estimation: microphone position encoding + progressive training, leaps in both accuracy and efficiency. [Includes Python code]](05.jpg)
![(DOA Estimation)No need to retrain! New breakthrough in geometric invariant DOA estimation: microphone position encoding + progressive training, leaps in both accuracy and efficiency. [Includes Python code]](06.jpg)
![(DOA Estimation)No need to retrain! New breakthrough in geometric invariant DOA estimation: microphone position encoding + progressive training, leaps in both accuracy and efficiency. [Includes Python code]](07.jpg)
![(DOA Estimation)No need to retrain! New breakthrough in geometric invariant DOA estimation: microphone position encoding + progressive training, leaps in both accuracy and efficiency. [Includes Python code]](08.jpg)

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->
