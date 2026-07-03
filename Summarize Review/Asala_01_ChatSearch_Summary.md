# Asala Abo Grara - ChatSearch: A Dataset and a Generative Retrieval Model for General Conversational Image Retrieval

## Paper Information

| Item | Details |
|---|---|
| Paper | ChatSearch: A Dataset and a Generative Retrieval Model for General Conversational Image Retrieval |
| Main Topic | Conversational Image Retrieval (CIR) |
| Main Modalities | Text and Image |
| Main Output | Retrieved images and textual responses |
| Relevance to Our Project | Provides a strong reference for multimodal conversational retrieval and user-intent reasoning. |

---

## 1. Paper Overview

This paper introduces **ChatSearch**, a dataset for general conversational image retrieval, and **ChatSearcher**, a generative retrieval model. The goal is to retrieve images based on an interactive multi-turn conversation between the user and the system. Unlike traditional image retrieval, the user intent is not always expressed in one direct query; it may be hidden across multiple dialogue turns and may involve both text and images.

The model is designed to understand interleaved image-text inputs, infer implicit user intentions, and either generate textual responses or retrieve relevant image candidates.

---

## 2. Problem Addressed by the Paper

Traditional image retrieval systems usually depend on:

- A direct text query.
- A reference image.
- A simple image description.
- A single round of user interaction.

These systems become weak when the query is conversational, multi-turn, and multimodal. In real usage, users often refine their search progressively, mention implicit details, or provide both text and visual examples. Therefore, the retrieval model must understand the full dialogue context instead of only matching isolated text or image features.

---

## 3. Proposed Solution

The paper proposes two main contributions:

### 3.1 ChatSearch Dataset

A dataset for conversational image retrieval that includes three subtasks:

| Subtask | Context Modality | Input Type | Output |
|---|---|---|---|
| tChatSearch | Text | Multi-round textual dialogue | Image candidates |
| iChatSearch | Image + Text | Single image and text instruction | Image candidates |
| mChatSearch | Image + Text | Multi-round multimodal dialogue | Image candidates |

### 3.2 ChatSearcher Model

ChatSearcher is a generative retrieval model that can process interleaved image-text inputs and produce interleaved outputs. It uses:

- A large language model for dialogue understanding.
- A visual encoder for image representation.
- A Q-Former to compress image features.
- A special `[IMG]` token to indicate image retrieval.
- A feature queue to support image matching and retrieval.

---

## 4. Important Figures and Tables

### Figure 1: General Conversational Image Retrieval

![ChatSearch Figure 1](Pic/Asala_ChatSearch_Figure1_General_Conversational_Image_Retrieval.jpg)

This figure shows that ChatSearcher can accept multimodal dialogue inputs and generate either textual responses or retrieved images.

### Figure 2: Data Construction Pipeline

![ChatSearch Figure 2](Pic/Asala_ChatSearch_Figure2_Data_Construction_Pipeline.jpg)

This figure illustrates how the ChatSearch dataset is constructed using GPT, an image gallery retriever, an image captioner, context merging, and manual review.

### Figure 3: Multimodal Dialogue Construction

![ChatSearch Figure 3](Pic/Asala_ChatSearch_Figure3_Multimodal_Dialogue_Construction.jpg)

This figure explains how multimodal dialogues are generated using reference images and reference text.

### Figure 4: ChatSearcher Architecture

![ChatSearch Figure 4](Pic/Asala_ChatSearch_Figure4_ChatSearcher_Architecture.jpg)

This is the main architecture of ChatSearcher. It combines visual encoding, Q-Former, a multimodal LLM, and a feature queue for image retrieval.

### Table 1: Dataset Statistics

![ChatSearch Table 1](Pic/Asala_ChatSearch_Table1_Dataset_Statistics.jpg)

This table summarizes the three ChatSearch subtasks and their sample numbers.

### Table 2: Main Retrieval Results

![ChatSearch Table 2](Pic/Asala_ChatSearch_Table2_Main_Results.jpg)

This table shows that ChatSearcher outperforms CLIP and FROMAGe on conversational image retrieval.

---

## 5. Key Findings

- Multi-turn conversation improves image retrieval because it provides richer context.
- Interleaved image-text understanding is stronger than using only text or only image features.
- ChatSearcher performs best on multimodal conversational retrieval because it can reason over dialogue history.
- Traditional retrieval models such as CLIP are limited when user intention is implicit and distributed across dialogue turns.

---

## 6. Research Gap

Although ChatSearch is strong in text-image conversational retrieval, it does not cover other important modalities such as audio, facial expressions, motion, touch, physiological signals, or environmental sensors. It also focuses mainly on image retrieval, not on real-world multimodal sensing systems that combine multiple heterogeneous signals.

**Gap Statement:**

> ChatSearch demonstrates the value of multimodal conversational context for image retrieval, but it remains limited to text and image modalities. A practical multimodal CIR system still needs to support additional modalities such as audio, facial expressions, motion, physiological indicators, and environmental sensors.

---

## 7. Contribution to Our Final Project

This paper supports our project by providing the **conversational retrieval foundation**. It shows how a system can use dialogue context to understand implicit user intent.

For our final prototype, the idea can be extended as follows:

| From ChatSearch | How We Use It in Our Project |
|---|---|
| Multi-turn context | Keep user interaction history to refine system decisions. |
| Image-text reasoning | Extend reasoning to audio and facial expressions. |
| Retrieval based on implicit intent | Use multimodal signals to infer emotional or behavioral state. |
| Interleaved multimodal input | Design a pipeline that can combine audio and visual features. |

---

## 8. Proposed Project Solution Inspired by This Paper

For the final project, ChatSearch inspires a practical direction:

1. Accept multimodal input from microphone and camera.
2. Extract audio and facial-expression features.
3. Keep interaction context if the system is conversational.
4. Use fusion or attention to combine modalities.
5. Produce a final state prediction or retrieval result.

In the prototype, this paper supports the idea of moving from a simple one-shot prediction system to a more interactive multimodal system.

---

## 9. Final Takeaway

ChatSearch is important because it proves that multimodal dialogue context can improve retrieval. However, our project should go beyond text-image retrieval by applying similar reasoning principles to audio-visual emotion or state understanding.