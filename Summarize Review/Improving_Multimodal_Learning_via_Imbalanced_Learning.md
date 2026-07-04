# Improving Multimodal Learning via Imbalanced Learning
ARL (Asymmetric Representation Learning) modulates multimodal training so that 
each modality’s contribution is inversely proportional to its variance, reducing 
bias-variance error and achieving state-of-the-art performance on diverse multimodal 
benchmarks.
Shicai Wei1, 2 Chunbo Luo1* Yang Luo1 1University of Electronic Science and Technology of China 
2 National and Local Joint Engineering Research Center for Cloud Operating System 
shicaiwei@std.uestc.edu.cn, {c.luo
2026
## Key concepts
• Multimodal Learning
• multimodal model
• action recognition
## Abstract
Multimodal learning often encounters the under-optimized problem and may perform worse than unimodal learning. 
Existing approaches attribute this issue to imbalanced learning across modalities and tend to address it through 
gradient balancing. However, this paper argues that balanced learning is not the optimal setting for multimodal 
learning. With bias-variance analysis, we prove that imbalanced dependency on each modality obeying the inverse 
ratio of their variances contributes to optimal performance. To this end, we propose the Asymmetric Representation 
Learning(ARL) strategy to assist multimodal learning via imbalanced optimization. ARL introduces auxiliary 
regularizers for each modality encoder to calculate their prediction variance. ARL then calculates coefficients via the 
unimodal variance to re-weight the optimization of each modality, forcing the modality dependence ratio to be 
inversely proportional to the modality variance ratio. Moreover, to minimize the generalization error, ARL further 
introduces the prediction bias of each modality and jointly optimizes them with multimodal loss. Notably, all auxiliary 
regularizers share parameters with the multimodal model and rely only on the modality representation. Thus the 
proposed ARL strategy introduces no extra parameters and is independent of the structures and fusion methods of the 
multimodal model. Finally, extensive experiments on various datasets validate the effectiveness and versatility of ARL. 
Code is available at https://github.com/shicaiwei123/ICCV2025-ARL
## Builds on previous research
The training and validation split of the dataset follows [27]. Here, we extract frames from event-localized video 
segments and capture corresponding audio clips, creating a labeled multimodal classification dataset. . 
Page 6
Implementation details. To ensure a fair comparison, we utilize ResNet18 as the encoder backbone for all 
datasets, as is common in previous methods [21, 10]. Page 6
The entire audio data is transformed into a spectrogram of size 257×1,004. The training configurations mirror 
those of previous methods [21, 10], including a mini-batch size of 64, an SGD optimizer with momentum 0.9, a 
learning rate of 1e-3, and a weight decay of 1e-4. $\gamma$ is set as 4 for all datasets. $T$ is set 8,4,4,4,4 for 
CREMA-D, AVE, KS, MOSI, and UCF101 datasets, respectively. Page 6
## Differs from previous work
Existing balance-based methods [21, 18, 10, 34] try to modulate the learning of different modalities to balance 
their optimization. However, we found that imbalanced learning obeying the inverse of the modality variance 
ratio can contribute to better performance. Page 6
## Snapshot
ARL boosts multimodal AI performance by allocating more learning weight to the most reliable modality, 
improving overall understanding without extra components.
## Key findings
Enhancing the strongest modality (e.g., audio) raises the performance of the entire multimodal system, 
contrary to the prior belief that modalities should be balanced.
The approach yields consistent score improvements across a variety of tasks, ranging from modest to 
substantial gains.
ARL is effective for configurations with two, three, or more modalities and works with different model 
architectures.
## Objectives
The goal was to create a technique (ARL) that improves multimodal learning by preferentially strengthening the 
most reliable input streams.
## Study Subjects
The study involved computer models learning from multiple modalities such as sound, images, and text.
## Methods
ARL modifies the learning step sizes based on each modality’s reliability, giving larger updates to steadier (less 
noisy) inputs while requiring no new hardware or memory overhead.
## Results
Across multiple benchmark tests involving audio-visual games and speech tasks, models using ARL achieved 
higher accuracy scores than baseline methods, with improvements varying from a few percent to large margins.
## Conclusions
Prioritizing learning capacity for the most reliable modality leads to overall better multimodal performance, 
and this can be achieved without additional model components or memory.
## Limitations
The provided text does not specify any experimental or methodological limitations.
## Future Work
No explicit future research directions are mentioned in the excerpt.
## Practical Applications
ARL can be applied to any multimodal AI system—such as games that combine sound, video, and speech—to 
improve performance without extra hardware, making it suitable for real-world deployments where 
computational resources are limited.
## Study subjects
6698 samples
They are further divided into 6698 samples as the training set and 744 samples as the testing set
## Figure 1
<img width="1920" height="1080" alt="page-017" src="https://github.com/user-attachments/assets/1a744c8c-085c-4589-baea-e985f06948ca" />

The visualization on the audio-visual 
dataset CREMA-D. (a) presents the 
performance of the unimodal branch in 
the vanilla multimodal model. (b) 
presents the performance of the 
multimodal model with audio branch 
modulation. ‘ $a*5$ ’ represents 
increasing the gradient for the audio 
branch by fivefolds to accelerate its 
optimization. (c) presents the gap 
between the modality dependence and 
modality variance. 
$\frac{d_{a}}{d_{v}}$ denotes the 
model optimization dependence ratio on 
the audio and visual modalities (see 
Equation 4 ). $\frac{q_{a}}{q_{v}}$ 
denotes the inverse of the variance ratio 
of audio and visual modalities (see 
Equation 17 )
## Figure 2
<img width="1920" height="1080" alt="page-018" src="https://github.com/user-attachments/assets/f85520e0-1e26-4b49-b716-7d801b42951f" />

The pipeline of the multimodal model 
with ARL strategy. It consists of three 
components: the modality analysis to 
measure the modality variance; the 
asymmetric learning to align the 
optimization dependency on each 
modality with the inverse of their 
variance ratio; and the unimodal bias 
regularization to reduce multimodal bias. 
$g_{s}$ is the gradient passed back from 
the fusion module
## Figure 3
<img width="1920" height="1080" alt="page-019" src="https://github.com/user-attachments/assets/97cc258a-d692-4c02-a903-5827381ea061" />

Algorithm 1 Multimodal learning with 
ARL strategy
