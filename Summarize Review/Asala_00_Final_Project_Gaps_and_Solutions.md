# Asala Abo Grara - Final Project Gaps and Practical Solutions from the Reviewed Papers

## Project Context

Our project focuses on **Multimodal CIR Research** and aims to study how different modalities can be integrated, including language, audio, visual signals, touch, motion, physiological indicators, and environmental sensors. The initial prototype will focus on **audio and facial expressions**.

---

## 1. Combined Research Gap

The reviewed papers show that multimodal learning has strong theoretical progress, but there is still a practical gap in building a real prototype that can handle noisy, missing, imbalanced, and changing modalities.

**Main Project Gap:**

> Existing multimodal methods provide strong solutions for text-image retrieval, audio-visual fusion, and modality imbalance. However, most of them assume stable, available, and reliable modalities. A practical prototype must dynamically assess modality quality, handle imbalance, and fuse audio and facial-expression features under real-world conditions.

---

## 2. Gap and Solution from Each Paper

| Paper | Main Gap | Project Solution Inspired by the Paper |
|---|---|---|
| ChatSearch | Limited to text-image retrieval and does not include audio, facial expressions, or sensor signals. | Extend conversational multimodal reasoning from text-image to audio-face inputs. |
| Diagnosing & Re-learning | Training-focused and classification-based; does not handle dynamic real-time reliability. | Add a modality quality diagnosis module before fusion. |
| BalanceBenchmark | No existing method achieves the best balance between performance, imbalance, and complexity. | Evaluate prototype using accuracy, modality balance, and computational cost. |
| Joint Cross-Attention AV Fusion | Strong audio-visual fusion but assumes both modalities are available and reliable. | Use cross-attention as the main fusion strategy and add reliability-aware weighting. |
| PDMP | Prioritizes dominant modality during training but not dynamically during inference. | Add dynamic modality prioritization based on current audio/face reliability. |

---

## 3. Proposed Final Prototype Direction

The final prototype can be designed as follows:

```text
Microphone Input  →  Audio Feature Extraction
Camera Input      →  Facial Expression Feature Extraction
                         ↓
              Modality Quality Assessment
                         ↓
              Dynamic / Reliability-Aware Fusion
                         ↓
              Emotion or State Prediction
```

---

## 4. Proposed Modules

| Module | Purpose | Supported by Paper |
|---|---|---|
| Audio Feature Extractor | Extract speech or acoustic features. | Joint Cross-Attention |
| Facial Feature Extractor | Extract facial-expression representations. | Joint Cross-Attention |
| Quality Assessment | Detect noisy or unreliable modalities. | Diagnosing & Re-learning |
| Dynamic Fusion | Combine audio and visual features adaptively. | Joint Cross-Attention + PDMP |
| Relative Balance Strategy | Avoid forcing equal modality contribution. | BalanceBenchmark + PDMP |
| Conversational Context Extension | Support future interactive CIR behavior. | ChatSearch |

---

## 5. Final Suggested Research Direction

A strong research direction for our project is:

> Reliability-aware audio-visual fusion for multimodal conversational interaction, using cross-attention and dynamic modality prioritization to handle modality imbalance and real-world signal quality changes.

---

## 6. Final Project Contribution

The project can contribute by proposing a theoretical framework that combines:

- Audio-visual cross-attention.
- Modality quality assessment.
- Relative balance instead of absolute balance.
- Dynamic modality prioritization.
- A practical prototype using microphone and camera inputs.

This makes the project more practical than papers that focus only on theoretical fusion or static training-time optimization.