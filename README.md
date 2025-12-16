# C# INT34057 Project — CAFA-6 Protein Function Prediction

Repo này là codebase cho cuộc thi Kaggle **CAFA-6 Protein Function Prediction**: dự đoán **GO terms** cho **protein** dựa trên **chuỗi acid amin**

- **Input:** CAFA6 dataset (FASTA + train_terms + go-basic.obo) + embeddings (protein_ids + protein_embeddings) + (optional) GOA annotations.
- **Output:** `submission.tsv` gồm 3 cột tab-separated: `protein_id`, `go_term`, `score`.

## What this project does (pipeline overview)

1. Download CAFA6 competition data + embeddings (+ optional GOA).
2. Build label space & training targets theo 3 aspects của GO: **C / F / P**.
3. Train 3 model MLP (mỗi aspect một model).
4. Predict trên test set và merge các dự đoán lại thành bảng `(protein_id, term, score)`.
5. **Ontology propagation:** lan truyền score từ child terms lên ancestor terms bằng max.
6. (Optional) **GOA postprocess:** loại các term “NOT” và/hoặc thêm GOA positives.
7. Export `submission.tsv`.

## TL;DR / Quickstart

> Các lệnh dưới đây chạy được trên local / Vast.ai / Colab / server bất kỳ, miễn là có Python và (khuyến nghị) GPU.

### 0) Clone repo
```bash
git clone <YOUR_REPO_URL>
cd <YOUR_REPO_FOLDER>



