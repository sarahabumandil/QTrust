# Asala Abo Grara - PDMP Proposal-Focused Summary

## Paper Information

| Item | Details |
|---|---|
| Paper | PDMP: Rethinking Balanced Multimodal Learning via Performance-Dominant Modality Prioritization |
| Main Topic | Performance-dominant modality prioritization |
| Main Problem | Balanced learning is not always optimal when one modality is naturally more informative. |
| Main Use for Our Proposal | Supports dynamic modality prioritization. |

---

## 1. Why This Paper Matters for the Proposal

This paper is very useful because it challenges the idea that all modalities should always be balanced equally. It argues that the modality with stronger performance should sometimes guide multimodal learning.

For our proposal, this supports the idea that audio and facial expressions should not always have fixed equal weights. The system should prioritize the modality that is more reliable or more informative in the current situation.

---

## 2. Main Idea

PDMP proposes **Performance-Dominant Modality Prioritization**.

The method works in two main stages:

1. **Modality Analysis:** Train unimodal models and identify which modality performs better.
2. **Gradient Modulation:** Adjust training so the performance-dominant modality can guide multimodal optimization.

---

## 3. Important Points for the Proposal

- Balanced multimodal learning is not always the best strategy.
- A stronger modality should sometimes receive more attention.
- The goal should be performance improvement, not only equal contribution.
- This idea can be extended into a real-time dynamic prioritization module.

---

## 4. Selected Important Figures and Table

### Figure 1: Balanced vs Imbalanced Learning

![PDMP Figure 1](Pic/Asala_PDMP_Figure1_Balanced_vs_Imbalanced_Learning.jpg)

**Why it is important:** This figure shows that balanced learning does not always lead to the best multimodal performance.

### Figure 2: Performance-Dominant Modality Prioritization

![PDMP Figure 2](Pic/Asala_PDMP_Figure2_Performance_Dominant_Modality_Prioritization.jpg)

**Why it is important:** This is the core PDMP framework and directly supports the idea of modality prioritization.

### Figure 3: Modality Analysis and PDMP Strategy

![PDMP Figure 3](Pic/Asala_PDMP_Figure3_Algorithm1_Modality_Analysis_and_PDMP_Strategy.jpg)

**Why it is important:** This figure explains how modality dominance can be detected and used.

### Table 1: Main Comparison

![PDMP Table 1](Pic/Asala_PDMP_Table1_Main_Comparison.jpg)

**Why it is important:** This table supports the claim that prioritizing the dominant modality can improve performance.

---

## 5. Research Gap

PDMP focuses mainly on training-time modality prioritization. However, in real-world systems, the dominant modality can change from one situation to another.

For example:

- Audio may be dominant when speech is clear.
- Visual modality may be dominant when the face is clear and audio is noisy.
- Both modalities may be weak when the environment is noisy and the camera is poor.

**Gap we can use:**

> Current performance-dominant modality methods need to be extended from static training-time prioritization to dynamic real-time modality prioritization.

---

## 6. How This Paper Helps Our Final Proposal

PDMP supports our proposed idea of **dynamic modality prioritization**.

In our project, we can adapt the idea as follows:

- Estimate audio reliability.
- Estimate face/visual reliability.
- Decide which modality should have higher weight.
- Fuse modalities using reliability-aware cross-attention.

---

## 7. Final Takeaway

PDMP helps us argue that the project should not force equal audio-face fusion. Instead, the system should dynamically prioritize the modality that is more useful and reliable.
