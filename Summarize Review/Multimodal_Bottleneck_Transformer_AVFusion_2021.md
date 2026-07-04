# [2107.00135] Attention Bottlenecks for Multimodal Fusion
A novel transformer architecture (MBT) that uses a small set of cross-modal bottleneck 
tokens to fuse audio and visual information, achieving state-of-the-art performance 
on multiple video classification benchmarks while reducing computational cost.
Arsha Nagrani Shan Yang Anurag 
Arnab Aren Jansen Cordelia Schmid 
Chen Sun {anagrani, shanyang, 
aarnab
2026
## Key concepts
• Vision Transformer
• audio visual
• multimodal fusion
• mean average precision
• action recognition
## Abstract
Humans perceive the world by concurrently processing and fusing high-dimensional inputs from multiple 
modalities such as vision and audio. Machine perception models, in stark contrast, are typically modality￾specific and optimised for unimodal benchmarks, and hence late-stage fusion of final representations or 
predictions from each modality (‘late-fusion’) is still a dominant paradigm for multimodal video classification. 
Instead, we introduce a novel transformer based architecture that uses ‘fusion bottlenecks’ for modality fusion 
at multiple layers. Compared to traditional pairwise self-attention, our model forces information between 
different modalities to pass through a small number of bottleneck latents, requiring the model to collate and 
condense relevant information in each modality and share what is necessary. We find that such a strategy 
improves fusion performance, at the same time reducing computational cost. We conduct thorough ablation 
studies, and achieve state-of-the-art results on multiple audio-visual classification benchmarks including 
Audioset, Epic-Kitchens and VGGSound. All code and models will be released.
## Counterpoint to earlier claims
We note that first, the model focuses on semantically salient regions in the video for audio classification, 
particularly regions where there is motion that creates or modifies sound, i.e. the mouth of humans making 
sounds, fingertips on a piano, hands and instruments. This is unlike state of the art sound source localisation
techniques trained with images [11], which tend to highlight the entire object. 
Page 10
## Builds on previous research
For many works, the inputs to transformers are the output representations of single modality CNNs [39, 23] –
unlike these works we use transformer blocks throughout, using only a single convolutional layer to rasterise 2D 
patches. The tokens from different modalities are usually combined directly as inputs to the transformers [42], 
for example, the recently released Perceiver model [32] introduces an iterative attention mechanism which 
takes concatenated raw multimodal signals as inputs, which corresponds to our ‘early fusion’ baseline. 
Page 3
The dataset consists of 90,000 variable length clips spanning 100 hours. We report results for action 
recognition following standard protocol [14] - each action label is a combination of a verb and noun, and we 
predict both using a single network with two ‘heads’, both trained with a cross-entropy loss. 
Page 6
In this section we report results on 2 additional datasets, Moments in Time [47] and Kinetics [35]. In this section 
we report results on 2 additional datasets, Moments in Time [47] and Kinetics [35]. 
Page 16
## Differs from previous work
Audiovisual learning: Audiovisual multimodal learning has a rich history, both before and during the deep 
learning era [53]. In contrast, we carefully examine the impact of different modality fusion strategies, including 
limiting cross-modal attention flow to later layers of our model, and ‘channeling’ cross-modal connections 
through bottlenecks in our proposed Multimodal Bottleneck Transformer (MBT). . 
Page 3
Multimodal transformers have been applied to various tasks including audio enhancement [19, 60], speech 
recognition [27], image segmentation [66, 60], cross-modal sequence generation [43, 41, 56], image and video 
retrieval [28, 23, 8], visual navigation [51] and image/video captioning/classification [46, 59, 58, 40, 31]. For 
many works, the inputs to transformers are the output representations of single modality CNNs [39, 23] –
unlike these works we use transformer blocks throughout, using only a single convolutional layer to rasterise 2D 
patches. Page 3
## Snapshot
A novel transformer architecture (MBT) that uses a small set of cross-modal bottleneck tokens to fuse audio and 
visual information, achieving state-of-the-art performance on multiple video classification benchmarks while 
reducing computational cost.
## Key findings
1. Restricting cross-modal attention to a limited set of bottleneck latents forces each modality to summarise 
salient information, leading to better fusion quality.
2. The bottleneck approach mitigates the quadratic scaling of full pairwise attention, making the model more 
scalable to longer video sequences.
3. Mid-layer fusion (introducing cross-modal attention after unimodal feature extraction) is more effective 
than pure early or pure late fusion baselines.
Mid-fusion (L. f ≈ 8–10) outperforms both early (L. f = 0) and late (L. f = 12) fusion, with optimal performance at 
L. f = 10 for vanilla cross-attention and L. f = 8 for bottleneck fusion. Bottleneck fusion consistently matches or 
exceeds vanilla cross-attention while incurring negligible extra GFLOPs, especially for early fusion where it 
gains &gt;2 mAP with &lt;½ the computation. Varying the number of bottleneck tokens (B = 4–1024) has 
minimal impact on accuracy (≤0.5 mAP), justifying the use of B = 4.
We propose a new transformer architecture (MBT) for audiovisual fusion, and explore a number of different 
fusion strategies using cross-attention between latent tokens
## Objectives
The goal is to design a generic multimodal transformer architecture that efficiently fuses heterogeneous 
modalities, investigates where (early, mid, late) and how (vanilla cross-attention vs. bottleneck) to fuse them, 
and evaluates the impact of these design choices on video classification accuracy and computational 
complexity.
## Methods
The MBT builds on Vision Transformer (ViT) and Audio Spectrogram Transformer (AST) tokenisation, 
converting image patches and spectrogram patches into 1-D tokens with learned positional embeddings.
Three fusion strategies are explored: (1) early fusion (cross-modal attention at every layer), (2) mid fusion 
(cross-modal attention introduced only at a designated “fusion layer”), and (3) bottlenecked fusion, where a 
small set of latent “fusion units” act as attention bottlenecks forcing each modality to condense information 
before sharing.
Cross-modal interactions are implemented via Multi-Headed Cross-Attention (MCA) between modality tokens 
and the bottleneck latents, while intra-modal tokens attend freely within their own stream.
The core component is a Cross-Transformer layer that performs generalized cross-attention between 
modality-specific token sets, with separate parameters θ_rgb and θ_spec. To curb quadratic attention cost, a 
small set of B fusion-bottleneck tokens (B ≪ N. v, N. a) is inserted; all cross-modal attention must pass through 
these tokens. Three fusion strategies are explored: (i) unrestricted self-attention, (ii) vanilla cross-attention 
with separate modality weights, and (iii) bottleneck fusion. Fusion can occur at any layer L. f, enabling early, 
mid, or late fusion. The backbone is ViT-Base (L = 12, N_H = 12, d = 3072) initialized from ImageNet-21K; B is 
set to 4 for all experiments. Training uses binary cross-entropy for multi-label AudioSet and cross-entropy for 
single-label datasets, with a base learning rate 0.5, 50 epochs, Mixup (α = 0.3), stochastic depth (p = 0.3), batch 
size 64, and cosine LR schedule on TPUs. Input tokens are generated from 16×16 RGB patches (8 frames for 
AudioSet/VGGSound, 32 frames for Epic-Kitchens) and 16×16 spectrogram patches (400 patches for 8 s audio).
MBT employs cross-attention between modality-specific tokens and a set of B = 4 bottleneck tokens at each 
fusion layer; sampling windows of length t seconds (2, 4, 6, 8) are tested, with synchronized versus 
asynchronous modality sampling; a “modality MixUp” regulariser samples independent mix-up weights per 
modality; ablations include symmetric/asymmetric bottleneck updates, shared vs separate ViT encoders, and 
three ViT backbones (Small, Base, Large).
The authors train MBT models on large video corpora, using a ViT-B backbone for audiovisual fusion. They 
compare MBT to visual-only and late-fusion baselines (Table 8), and conduct ablations with checkpoints 
pre-trained on VGGSound, Kinetics-400, and AudioSet-500K before fine-tuning on Audioset-mini and 
VGGSound (Table 10).
## Results
MBT attains new state-of-the-art performance on all three benchmarks, most notably improving AudioSet 
mean average precision (mAP) by 5.9 points (a 12.7 % relative gain).
Ablation studies show that bottlenecked fusion matches or exceeds unrestricted full-attention models while 
using fewer FLOPs, confirming the computational advantage of the bottleneck design.
On the mini-AudioSet evaluation split, the best MBT configuration (bottleneck fusion, L. f = 8, B = 4) achieves 
higher mean average precision than comparable vanilla cross-attention models while keeping GFLOPs 
essentially constant across fusion layers. Across all three datasets, MBT matches or surpasses state-of-the-art 
multimodal video classifiers, with comparable or lower computational overhead.
Fusion with bottlenecks (t = 8 s, B = 4, Fₗ = 8) consistently beats visual-only and audio-only baselines across all 
datasets.
Modality MixUp raises AudioSet mAP from 42.6 to 43.9.
Performance improves monotonically with training set size, especially for audio-only models.
MBT surpasses prior fusion methods (e.g., Perceiver, Attn Audio-Visual) despite training on only 500 K samples.
Per-class analysis shows fusion improves 57/60 top AudioSet classes; gains exceed 60 % absolute AP for classes 
like “bicycle”.
Attention Rollout visualisations reveal the model focuses on semantically relevant, sound-producing regions 
(e.g., mouths, hands).
On the full Kinetics test set, MBT improves top-1 accuracy by ~1% over the visual baseline.
On the Kinetics-Sound subset, the improvement exceeds 4%.
On Epic-Kitchens, MBT gains almost 6% top-1 action accuracy versus late-fusion.
Pre-training on VGGSound yields a 3% mAP boost on Audioset-mini, while Kinetics-400 adds only 0.7%.
On VGGSound, AS-500K pre-training gives a 1.2% top-1 accuracy increase, whereas Kinetics-400 offers no 
benefit.
## Conclusions
A transformer-based multimodal architecture that channels cross-modal communication through compact 
bottlenecks can simultaneously boost classification accuracy and reduce computational demands, establishing 
a new benchmark for audio-visual video understanding.
A bottleneck-based cross-attention mechanism enables efficient multimodal fusion in transformers, allowing 
later-stage cross-modal interactions that preserve unimodal feature learning while reducing quadratic 
attention costs. Mid-layer fusion with a few bottleneck tokens provides the best trade-off between accuracy 
and computation for video classification.
Restricting cross-modal attention to a few bottleneck tokens yields superior audiovisual fusion with lower 
compute, establishing a new state-of-the-art across diverse video benchmarks and demonstrating that 
multimodal information is complementary even when one modality is weak.
## Study subjects
3 video classification datasets
We then ablate the key design choices in our model (Sec. 4.3), before finally comparing our model to the state of 
the art (Sec. 4.4).4.1 Datasets and evaluation protocolWe experiment with three video classification datasets –
AudioSet [24], Epic-Kitchens-100 [14] and VGGSound [12], described in more detail below
## Study analysis
For images we apply the standard data augmentations used in [6] (random crop, flip, colour jitter), and for spectrograms we use SpecAugment [50] 
with a max time mask length of 192 frames and max frequency mask length of 48 bins following AST [26]. We set the base learning rate to $0.5$ and 
train for $50$ epochs, using Mixup [67] with $\alpha=0.3$ and stochastic depth regularisation [30] with probability $p=0.3$. All models (across 
datasets) are trained with a batch size of $64$, synchronous SGD with momentum of $0.9$, and a cosine learning rate schedule with warmup of 
$2.5$ epochs on TPU accelerators using the Scenic library [15]
## Study limitations
The study focuses exclusively on audio-visual data; extending the bottleneck design to additional modalities 
(e.g., text, depth) remains untested.
Full scalability to very long videos is still constrained by the need to sample a fixed number of frames and 
spectrogram patches, which may omit fine-grained temporal dynamics.
The study evaluates MBT on three video datasets (AudioSet, Epic-Kitchens-100, VGGSound) and reports 
additional results only in the appendix; broader generalization to other modalities or larger-scale settings is not 
demonstrated. The impact of extremely large bottleneck token counts (&gt;1024) and of alternative backbone 
architectures is not explored.
The optimal fusion layer depth is a hyper-parameter that may need dataset-specific tuning; the current work 
only explores fully supervised training, and the transformer backbone remains computationally intensive, 
raising environmental and bias-related concerns.
## Future work
The authors plan to release code and models, and suggest exploring the bottleneck paradigm for other 
multimodal combinations and for unsupervised pre-training tasks such as cross-modal synchronization.
Investigating adaptive bottleneck sizes and dynamic fusion-layer selection could further improve efficiency and 
adaptability to diverse datasets.
While not explicitly detailed in the text, the authors note that the formulation is generic to any number of 
modalities, suggesting future extensions could involve additional sensory streams, larger bottleneck capacities, 
or alternative transformer backbones to further test scalability and generality.
Planned extensions include applying MBT to additional modalities such as text and optical flow, and 
investigating self-supervised learning frameworks to reduce reliance on large labelled datasets.
## Practical applications
The MBT can be deployed for real-time multimodal video analysis tasks such as action recognition, event 
detection, and content moderation where both sound and sight provide complementary cues.
Its reduced computational footprint makes it suitable for edge devices or large-scale video indexing services 
that must process massive video libraries efficiently.
MBT can be deployed for efficient multimodal video understanding tasks such as action recognition, 
sound-event detection, and any scenario requiring joint processing of visual and audio streams, benefiting 
real-time systems where computational resources are limited.
The bottleneck-based multimodal transformer can be deployed for robust video classification, sound-source 
localisation, and any real-world system that benefits from combining audio and visual cues, while its reduced 
computational footprint makes it more feasible for large-scale or edge deployments.
## Figure 1
<img width="1920" height="1080" alt="page-018" src="https://github.com/user-attachments/assets/9ae656cc-9458-424b-bc21-1e7f54e96a4d" />

Cross-modal Fusion . Unlike late fusion 
(left), where no cross-modal information 
is exchanged in the model until after the 
classifier, we investigate two pathways 
for the exchange of cross-modal 
information. The first is via standard 
pairwise self attention across all hidden 
units in a layer, but applied only to later 
layers in the model – mid fusion (middle, 
left)
## Figure 2
<img width="1920" height="1080" alt="page-019" src="https://github.com/user-attachments/assets/b55d0f09-d18b-4c5d-be0f-de6c33e9809b" />

A Multimodal Fusion Transformer applied 
to audiovisual inputs. The input sequence 
consists of image and spectrogram 
patches. These are then projected into 
tokens and appended to special CLS 
(classification) and FSN (fusion 
bottleneck) tokens. Our transformer 
encoder then uses self attention to model 
unimodal information, and restricts 
cross-modal information flow via cross 
attention with the bottleneck tokens at 
multiple layers of the network
## Figure 3
<img width="1920" height="1080" alt="page-020" src="https://github.com/user-attachments/assets/a183e4ff-591e-4b63-b354-bd5ada4f3c01" />

The impact of using attention 
bottlenecks for fusion on performance 
(left) and compute (right) at different 
fusion layers $L_{f}$ on AudioSet, using 
clip span $t=4$ and $B=4$ bottleneck 
tokens. Attention bottlenecks improve 
performance at lower computational cost
## Figure 4
<img width="1920" height="1080" alt="page-021" src="https://github.com/user-attachments/assets/5558039c-547d-4da1-911b-6238c1bbd8d4" />

The effect of varying input clip span $t$ 
on the AudioSet test set
## Figure 5
<img width="1920" height="1080" alt="page-022" src="https://github.com/user-attachments/assets/b0c3dd6f-0b47-4b3b-b44f-bf24a1d45faf" />

The effect of training data size on the 
AudioSet test set
## Figure 6
<img width="1920" height="1080" alt="page-023" src="https://github.com/user-attachments/assets/30b68c85-e9c8-404b-9fdd-a86232479330" />

Attention Maps. We compute maps of the 
attention from the output CLS tokens to 
the RGB image input space for a vanilla 
self-attention model and MBT on the 
Audioset test set. For each video clip, we 
show the original middle frame on the 
left with the ground truth labels 
overlayed at the bottom. The attention is 
particularly focused on sound source 
regions in the video that contain motion, 
eg. the fingertips on the piano, the hands 
on the string instrument, faces of 
humans. The bottlenecks in MBT further 
force the attention to be localised to 
smaller regions of the images (i.e the 
mouth of the baby on the top left and the 
mouth of the woman singing on the 
bottom right)
## Figure 7
<img width="1920" height="1080" alt="page-024" src="https://github.com/user-attachments/assets/932c10fd-c419-4ebc-8183-69686ab2d4bb" />

The effect of sharing weights for vanilla 
fusion
## Figure 8
<img width="1920" height="1080" alt="page-025" src="https://github.com/user-attachments/assets/2041a95c-1990-4dc9-a316-e8527f8cc0b3" />

Asynchronous vs synchronous sampling 
of RGB and spectrogram inputs
## Figure 9
<img width="1920" height="1080" alt="page-026" src="https://github.com/user-attachments/assets/fca6f509-eaef-4fe4-a672-90ff595fef1c" />

Per-class average precision for the top 60 
classes in Audioset ranked by mAP. Best 
viewed in colour and zoomed in. Note 
how audio-visual fusion helps improve 
performance over audio only for almost 
all classes. The visual only model 
performs well for classes that have a 
stronger visual signature than audio, 
eg ‘bicycle’, ‘mechanical fan’, ‘boat’ and 
‘arrow’
