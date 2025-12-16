# CAFA6 Protein Function Prediction

**Bài toán:** dự đoán các **GO terms** (multi-label) cho protein ở 3 nhánh GO (**C/F/P**) từ **precomputed ESM-650M embeddings**.  
**Input:** embeddings + train labels (`train_terms.tsv`) + GO ontology (`go-basic.obo`) + (tuỳ chọn) GOA (`goa_uniprot_all.csv`)  
**Output:** `submission.tsv` (3 cột tab-separated: `protein_id`, `go_term`, `score`).
## Pipeline (high level)

- Download competition data + embeddings
- Build label space & targets cho từng aspect: **C / F / P**
- Train **3 model** (mỗi aspect 1 MLP)
- Predict test cho từng aspect → merge thành bảng `(protein_id, go_term, score)`
- Ontology propagation: lan truyền điểm từ **child → parent** bằng **max**
- (Optional) GOA postprocess:
  - remove các GO term bị đánh dấu **NOT**
  - add GOA positives (ground truth) với score cấu hình
- Export `submission.tsv`
