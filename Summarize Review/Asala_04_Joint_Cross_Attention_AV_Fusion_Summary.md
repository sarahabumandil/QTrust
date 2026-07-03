# Asala Abo Grara - A Joint Cross-Attention Model for Audio-Visual Fusion in Dimensional Emotion Recognition

## Paper Information

| Item | Details |
|---|---|
| Paper | A Joint Cross-Attention Model for Audio-Visual Fusion in Dimensional Emotion Recognition |
| Main Topic | Audio-Visual Fusion |
| Main Modalities | Audio and Visual / Facial Expressions |
| Task | Dimensional Emotion Recognition |
| Output | Valence and Arousal values |
| Relevance to Our Project | This is the closest paper to our prototype because it combines audio and facial features. |

---

## 1. Paper Overview

This paper proposes a **Joint Cross-Attention model** for audio-visual emotion recognition. The goal is to predict continuous emotion dimensions, specifically **valence** and **arousal**, by combining facial and vocal modalities.

The paper argues that simple feature concatenation and traditional recurrent fusion do not fully capture the complementary relationships between audio and visual signals. Therefore, it proposes a fusion mechanism that uses joint audio-visual representations inside a cross-attention module.

---

## 2. Problem Addressed by the Paper

In audio-visual emotion recognition, audio and visual modalities provide complementary information. Sometimes the face may be unclear due to pose, blur, or low illumination. In other cases, the audio may be noisy or silent. A strong fusion model must learn when and how each modality contributes to emotion prediction.

Existing methods often use:

- Feature concatenation.
- LSTM-based fusion.
- Conventional attention.
- Vanilla cross-attention.

However, these methods may not fully model both intra-modal and inter-modal relationships.

---

## 3. Proposed Solution

The proposed method builds a joint audio-visual representation and uses it to attend to individual audio and visual features.

The main idea is:

1. Extract visual features from face video clips.
2. Extract audio features from spectrograms.
3. Concatenate audio and visual features to create a joint representation.
4. Compute correlation between the joint representation and each individual modality.
5. Generate attention maps.
6. Produce attended audio and visual features.
7. Concatenate the attended features and predict valence and arousal.

---

## 4. Important Figures and Tables

### Figure 1: Valence-Arousal Space

![Joint Figure 1](Pic/Asala_JointCrossAttention_Figure1_Valence_Arousal_Space.png)

This figure explains the dimensional emotion space. Valence measures emotional positivity or negativity, while arousal measures emotional intensity.

### Figure 2: Joint Cross-Attention Architecture

![Joint Figure 2](Pic/Asala_JointCrossAttention_Figure2_Architecture.png)

This is the main architecture. It shows the visual stream, audio stream, feature extraction, joint cross-attention, fusion, and valence/arousal prediction.

### Table 1: Ablation Study

![Joint Table 1](Pic/Asala_JointCrossAttention_Table1_Ablation_Study.png)

This table compares different backbones and fusion strategies. Joint Cross-Attention achieves strong results, especially for valence.

### Table 2: Validation Set Comparison

![Joint Table 2](Pic/Asala_JointCrossAttention_Table2_Validation_Comparison.png)

This table compares the proposed method with previous audio-visual fusion methods on the AffWild2 validation set.

### Table 3: Test Set Comparison

![Joint Table 3](Pic/Asala_JointCrossAttention_Table3_Test_Comparison.png)

This table compares the method with other submissions on the AffWild2 test set.

---

## 5. Key Findings

- Joint Cross-Attention improves audio-visual fusion compared to simple concatenation.
- Joint representation helps capture both intra-modal and inter-modal relationships.
- Audio and visual information can complement each other for emotion recognition.
- The method improves the baseline significantly on valence and arousal prediction.

---

## 6. Research Gap

Although the paper provides an effective audio-visual fusion model, it assumes that both audio and visual modalities are available and reasonably reliable. It does not directly address missing modalities, dynamic noise, modality imbalance, or real-time reliability changes.

**Gap Statement:**

> Joint Cross-Attention effectively models audio-visual interactions, but it does not handle missing or unreliable modalities. In real-world prototypes, audio may be noisy and facial expressions may be unclear, so fusion should be combined with modality reliability estimation and imbalance-aware decision making.

---

## 7. Contribution to Our Final Project

This paper is the main technical reference for our prototype because our prototype will combine audio and facial expressions.

| Paper Idea | Use in Our Project |
|---|---|
| Audio stream | Use microphone input and extract speech/acoustic features. |
| Visual stream | Use camera input and extract facial-expression features. |
| Joint Cross-Attention | Use as the main fusion strategy. |
| Valence-arousal prediction | Use as a possible emotion-state output. |
| Attention-based fusion | Replace simple concatenation with smarter fusion. |

---

## 8. Proposed Project Solution Inspired by This Paper

The prototype can be designed as follows:

1. Capture audio using a microphone.
2. Capture facial expressions using a camera.
3. Extract audio features such as MFCC or spectrogram-based features.
4. Extract facial features using a visual backbone.
5. Apply a cross-attention or joint fusion module.
6. Predict emotional state or valence-arousal values.

To improve the paper's limitation, we can add a modality quality check before fusion.

---

## 9. Final Takeaway

This paper gives the strongest direct architecture for our prototype. It supports the idea that audio and facial expressions should not be fused by simple concatenation only; instead, attention-based fusion can better capture their complementary relationship.