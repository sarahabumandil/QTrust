# [2103.05677] SMIL: Multimodal Learning with Severely Missing Modality
A meta-learning framework (SMSM) that combines K-means-guided missing modality 
reconstruction, uncertainty-guided feature regularization, and Bayesian inference 
achieves superior classification performance under severely missing modalities 
compared to generative baselines.
Mengmeng Ma1, Jian Ren2, Long 
Zhao3
2026
## Key concepts
• meta learning
• multimodal learning
• Variational Autoencoder
• Generative Adversarial Network
• MOSI
## Abstract
A common assumption in multimodal learning is the completeness of training data, i.e., full modalities are 
available in all training examples. Although there exists research endeavor in developing novel methods to 
tackle the incompleteness of testing data, e.g., modalities are partially missing in testing examples, few of them 
can handle incomplete training modalities. The problem becomes even more challenging if considering the case 
of severely missing, e.g., 90% training examples may have incomplete modalities. For the first time in the 
literature, this paper formally studies multimodal learning with missing modality in terms of flexibility (missing 
modalities in training, testing, or both) and efficiency (most training data have incomplete modality). 
Technically, we propose a new method named SMIL that leverages Bayesian meta-learning in uniformly 
achieving both objectives. To validate our idea, we conduct a series of experiments on three popular 
benchmarks: MM-IMDb, CMU-MOSI, and avMNIST. The results prove the state-of-the-art performance of 
SMIL over existing methods and generative baselines including autoencoders and generative adversarial 
networks. Our code is available at https://github.com/mengmenm/SMIL.
## Builds on previous research
One important direction in this area is multimodal fusion, which focuses on effective fusion of multimodal data. 
Early fusion is a common method which fuses different modalities by feature concatenation, and it has been 
widely adopted in previous studies (Wang et al 2017; Poria et al 2016). Page 2
However, under severely missing modality, it is non-trivial to train a reconstruction network from limited 
modality-complete samples. Inspired by (Kuo et al 2019), we approximate the missing modality using a 
weighted sum of modality priors learned from the modality-complete dataset. 
Page 3
The dataset includes $25,956$ movies and $23$ classes. We follow the training and validation splits provided in 
the previous work (Vielzeuf et al 2018). Page 4
We train the models for $10,000$ iteration with a learning rate of $10^{-4}$ for inner-loop and $10^{-3}$ fro 
outer-loop. Besides, we follow previous work (Vielzeuf et al 2018) to add a weight of $2.0$ on the positive label 
to balance the precision and recall since the labels are unbalanced. Page 6
## Differs from previous work
Lee et al(Lee et al 2020b) proposed a more general algorithm for latent feature regularization. Other than 
perturbing features, we propose to learn the regularization function following (Lee et al 2020b) but regularize 
the feature to reduce discrepancy between the reconstructed and true modality. 
Page 2
## Snapshot
A meta-learning framework (SMSM) that combines K-means-guided missing modality reconstruction, 
uncertainty-guided feature regularization, and Bayesian inference achieves superior classification performance 
under severely missing modalities compared to generative baselines.
## Key findings
We highlight that our method is better than typical generative designs, such as Autoencoder (AE)(Tran et al 
2017), Variational Autoencoder (VAE)(Kingma and Welling 2013), or Generative Adversarial Network 
(GAN)(Goodfellow et al 2014), since they often require a significant amount of full-modality data to learn from, 
which is usually not available in severely missing modality learning
To the best of our knowledge, we are the first work to systematically study the problem of multimodal learning 
with severely missing modality
We are interested in multimodal learning with severely missing modality, e.g., 90% of the training samples 
contain incomplete modalities
Our approach significantly outperforms all baselines among all ratios of modality missing, which showcases the 
efficiency of our approach in the missing modality problem
We analyze the results of the proposed algorithm for multimodal learning with severely missing modality on 
three datasets from two perspectives: efficiency under severely missing modality (Section 4.2) and flexibility to 
various modality missing pattern (Section 4.3)
## Objectives
The work aims to (1) develop a learning strategy that can reconstruct missing modalities without bias, (2) 
regularize multimodal features to reduce cross-modal discrepancy, and (3) employ a Bayesian meta-learning 
framework to infer posterior distributions for robust performance under various missing patterns.
## Methods
The approach integrates three components within a modified Model-Agnostic Meta-Learning (MAML) loop: (i) 
a main prediction network $f_{\theta}$; (ii) a feature-reconstruction network $f_{\phi_{c}}$ that generates 
approximations of missing-modality features from available modalities; and (iii) a feature-regularization 
network $f_{\phi_{r}}$ that uses Bayesian neural-network-based uncertainty to perturb latent features and 
reduce bias. Reconstruction is trained by predicting weighted combinations of modality priors learned from the 
limited complete data, while regularization leverages uncertainty estimates to guide learning.
Model modality weights $\bm{\omega}$ as $\mathcal{N}(\mathbf{I},\bm{\sigma})$, where 
$\bm{\sigma}=f_{\phi_c}(\mathbf{x}^1)$ is predicted by a feature-reconstruction network.
Reconstruct missing modality $\hat{\mathbf{x}}^{2}$ via the weighted sum 
$\langle\bm{\omega},\mathcal{M}\rangle$.
Introduce a feature-regularization network that outputs a Gaussian $\mathcal{N}(\bm{\mu},\bm{\sigma})$; 
the sampled regularization $\mathbf{r}$ modulates latent features through a Softplus-scaled operation.
Employ a bilevel meta-learning scheme: inner loop updates main network parameters $\theta$ using loss on 
partially-observed data $D^{m}$; outer loop updates all parameters $\{\theta,\phi_c,\phi_r\}$ based on loss 
on full data $D^{f}$. = \theta - \alpha \nabla_{\theta}\mathcal{L}(D^{m};\psi)$.”}
Optimize a variational lower bound: $\mathcal{L}_{\theta,\psi}= \mathbb{E}_{q(z|X)}[\log p(Y|X,z;\theta)] 
- \mathrm{KL}[q(z|X;\psi)\|p(z|X)]$, approximated via Monte-Carlo sampling.
Training details: Adam optimizer, batch sizes (32 for CMU-MOSI, 128 for MM-IMDb), learning rates $10^{-4}$ 
(inner) and $10^{-4}$–$10^{-3}$ (outer), 5k–10k iterations.
Two modality-specific feature extractors (standard LeNet-5 for images and a modified version for audio) 
extract features that are concatenated and fed into fully-connected layers for classification; training uses Adam 
(batch size 64, 15 000 iterations, learning rate 10⁻³) for both inner and outer loops of meta-learning. Missing 
modalities are reconstructed via a network that generates feature weights guided by K-means clustering; 
uncertainty-guided feature regularization reduces representation discrepancy; a Bayesian approach with 
variational inference models the posterior over reconstruction and regularization parameters.
## Results
Across all three benchmarks, SMIL consistently outperforms prior multimodal methods and strong generative 
baselines such as autoencoders, VAEs, and GANs, demonstrating superior accuracy even when 90 % of training 
samples are missing a modality.
Across all missing-data ratios, the proposed method outperforms all baselines (Lower-Bound, AE, GAN, MVAE) 
on both CMU-MOSI and MM-IMDb.
When only 20 % of text data is available (η=20 %), accuracy gains over AE and GAN are ~5.0 %; when η=10 %, 
gains increase to 7.6 % and 7.4 % respectively.
## Conclusions
The study establishes that multimodal learning can be both flexible and efficient under severe modality loss by 
using Bayesian meta-learning and feature-level reconstruction, marking the first systematic treatment of this 
problem and setting a new performance baseline.
The proposed SMIL framework effectively handles severely missing modalities by leveraging meta-learned 
reconstruction, regularization, and Bayesian inference, achieving consistent improvements over generative 
baselines across multiple datasets and missing patterns.
## Missing Pattern 1 (test Image Only)
With 20 % audio during training, SMIL outperforms the best generative baseline by 6.7 % and the lower bound 
by 3.3 %; with only 5 % audio, it is 1.10 % higher than the lower bound.
## Missing Pattern 2 (test Image + Audio)
SMIL exceeds the lower bound by 4.3 % and generative methods by 2.1 %; its performance drop when moving 
from two modalities to one is only 1.0 % versus 5.6 % for AE/GAN.
## Ablation On MM-IMDb
Removing K-means (SMIL w/o K-means) degrades performance, confirming its necessity; omitting feature 
regularization (SMIL w/o Regularization) also reduces accuracy, highlighting the benefit of regularization; 
deterministic or fixed-Gaussian variants of the Bayesian component underperform the full Bayesian approach, 
demonstrating the advantage of Bayesian inference.
## Study subjects
3 datasets
In this section, we analyze the results of the proposed algorithm for multimodal learning with severely missing 
modality on three datasets from two perspectives: efficiency under severely missing modality (Section 4.2) and 
flexibility to various modality missing pattern (Section 4.3).Experiment SettingDatasets
## Study analysis
K-means
We achieve this by learning a set of modality priors $\mathcal{M}$ which can be clustered among all modality-complete samples using K-means 
(MacQueen 1967) or PCA (Pearson 1901)
Gaussian distribution
Instead of generating a deterministic regularization $\mathbf{r}=f_{\phi_{r}}(\mathbf{h}^{l-1})$, we assume that $\mathbf{r}$ follows a 
multivariate Gaussian distribution $\mathcal{N}(\bm{\mu},\bm{\sigma})$, where the means and variances are calculated using 
$(\bm{\mu},\bm{\sigma})$ = $f_{\phi_{r}}(\mathbf{h}^{l-1})$
## Study limitations
SMIL’s reconstruction relies on a small set of modality-complete examples to learn priors, which may limit its 
effectiveness when complete data are extremely scarce or when more than two modalities are involved; the 
paper also does not explore scalability to large-scale real-world deployments.
The study evaluates only on datasets where the missing modality is audio (avMNIST) or limited to the MM-IMDb 
setting, and the reconstruction component relies on K-means clustering, which may limit scalability to 
higher-dimensional or more complex modalities.
## Future work
Planned extensions include handling a larger number of modalities, improving prior-learning and 
reconstruction quality under even harsher missing-data regimes, and applying the framework to real-world 
domains such as autonomous driving and privacy-sensitive social-network analysis.
Future research could extend the framework to other modality combinations, explore alternative clustering or 
generative mechanisms for reconstruction, and assess scalability to larger, real-world multimodal datasets 
with diverse missing patterns. {Inferred from the discussion of flexibility and the desire to apply the method to 
real-world scenarios where “partial modalities are missing or hard to collect.”}
## Practical applications
The ability to train robust multimodal models despite missing data enables applications in intelligent tutoring 
systems, robotics, healthcare diagnostics, autonomous vehicles, and privacy-constrained social-network 
analytics, where acquiring all modalities for every sample is often infeasible.
The approach is suited for real-world multimodal systems (e.g., audio-visual recognition, multimedia retrieval) 
where some sensors or data streams may be unavailable or costly to acquire, enabling robust classification 
without requiring full modality capture.
## Figure 1
<img width="1920" height="1080" alt="page-020" src="https://github.com/user-attachments/assets/8453c70e-2737-4539-89b6-684e2c117586" />

Multimodal learning configurations. (a) 
Train and test with full and paired 
modality (Ngiam et al. 2011 ) ; (b) Testing 
with missing modality (Tsai et al. 2019 ) ; 
(c) Training with unpaired modality (Shi 
et al. 2020 ) ; (d) We study the most 
challenging configurations of severely 
missing modality in training, testing, or 
both
## Figure 2
<img width="1920" height="1080" alt="page-021" src="https://github.com/user-attachments/assets/b8a66e8d-2145-4052-839f-331fb89fbb73" />

SMIL can uniformly learn from severely 
missing modality and test with either 
single or full modality. The 
reconstruction network $\phi_{c}$ 
outputs a posterior distribution, from 
which we sample weight $\omega$ to 
reconstruct the missing modality using 
modality priors. The regularization 
network $\phi_{r}$ also outputs a 
posterior distribution, from which we 
sample regularizer $r$ to perturb latent 
features for smooth embedding. The 
collaboration ( $\phi_{c}$ and 
$\phi_{r}$ ) guarantees flexible and 
efficient learning
## Figure 3
<img width="1920" height="1080" alt="page-022" src="https://github.com/user-attachments/assets/3c60a85e-55a4-436a-bae6-7587372e8900" />

Algorithm 1 Bayesian Meta-Learning 
Framework.
## Figure 4
<img width="1920" height="1080" alt="page-023" src="https://github.com/user-attachments/assets/d628ab97-b44d-4af4-9f12-2dca2423ce5b" />

F1 Samples score of each movie genre on 
the MM-IMDb dataset for the lower￾bound baseline ( blue ) and SMIL ( red ). 
The number of image samples for each 
movie genre is indicated by the green line
## Figure 5
<img width="1920" height="1080" alt="page-024" src="https://github.com/user-attachments/assets/8c4aa8da-64f5-40a9-a92f-e60bcb2f18f9" />

Classification accuracy (%) on avMNIST 
with two missing patterns. Left : training 
with 100% Image + $\eta$ % Audio and 
testing with Image Only. Right : training 
with 100% Image + $\eta$ % Audio and 
testing with Image + Audio
