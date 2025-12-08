# Embedding-Based Multimodal Semantic Search for E-Commerce

This repository contains the code and experiments for the project:

**“Embedding-Based Multimodal Semantic Search for E-Commerce”**

The goal of this project is to build a multimodal semantic search engine for fashion e-commerce that can:
- Retrieve products using **natural-language text queries** (text → image),
- Find visually similar products given a **query image** (image → image),

by leveraging **vision–language embeddings (CLIP)** instead of traditional keyword-based search.

---

##  Project Overview

Modern e-commerce platforms host millions of products, often with incomplete or noisy textual metadata. Traditional search (TF–IDF, keyword search) struggles with:
- Vague or style-based queries (e.g., “oversized pastel hoodie with minimal print”),
- Visual similarity (e.g., “show me similar shoes to this photo”).

In this project we:

1. Build an **embedding-based retrieval system** using CLIP to map images and text into a shared semantic space.
2. Implement a **keyword-based TF–IDF baseline** for comparison.
3. Evaluate both systems with ranking metrics such as **Recall@K, median rank, mean rank, and mAP**.

---

## 🧱 Architecture

High-level pipeline:

1. **Data Layer**
   - Load product images and metadata (titles, descriptions, categories, etc.).
   - Clean and normalize text; organize image paths and IDs.

2. **Embedding Layer**
   - Use a pretrained **CLIP model** (from  Transformers) to encode:
     - Product images → image embeddings  
     - Text queries / product titles → text embeddings

3. **Vector Index / Retrieval Layer**
   - Store embeddings in a **vector index** (e.g., FAISS / in-memory index).
   - Perform nearest neighbor search to retrieve top-K similar items for:
     - Text → Image retrieval
     - Image → Image retrieval

4. **Baseline Search Layer**
   - Build a **TF–IDF / keyword-based** search pipeline over product titles/descriptions.
   - Compare performance with the embedding-based system.

5. **Evaluation Layer**
   - Compute ranking metrics:
     - Recall@K
     - Median Rank / Mean Rank
     - Mean Average Precision (mAP)
   - Analyze qualitative results (good matches, failure cases).

---

##  Dataset

We use a fashion e-commerce dataset with product images and metadata:

- **R. Luhaniwal, “E-commerce Product Images (Fashion Images)”, Kaggle Dataset, 2021.**

You can download it directly from Kaggle and place it under a local folder, e.g.:

```text
data/
  images/
    <all product images>
  metadata.csv   # product_id, image_path, title, description, category, etc.
