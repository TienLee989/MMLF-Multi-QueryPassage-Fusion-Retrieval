# MMLF: Multi-query Multi-passage Late Fusion Retrieval

**Conference**: NAACL 2025  
**Authors**: Yuan-Ching Kuo, Yi Yu, Chih-Ming Chen, Chuan-Ju Wang  
**Affiliations**: Academia Sinica, The Ohio State University  
**Paper**: [NAACL 2025, pages 6602–6613]

---

## 📌 Overview

**MMLF** là một pipeline đơn giản nhưng hiệu quả trong truy hồi thông tin, sử dụng mô hình ngôn ngữ lớn (LLM) để cải thiện kết quả bằng cách:

1. Tạo nhiều truy vấn phụ (multi-query).
2. Mở rộng từng truy vấn thành đoạn văn ngữ cảnh (multi-passage).
3. Truy xuất độc lập và hợp nhất kết quả bằng **Reciprocal Rank Fusion (RRF)**.

> 📈 MMLF đạt **+4% Recall@1k trung bình**, và **+8% tối đa** so với các phương pháp SOTA trên 5 tập dữ liệu BEIR.

---

## 🔧 Key Components

### 1. Multi-query Generation
- Từ một truy vấn gốc, mô hình sinh ra **3 truy vấn phụ** phản ánh các khía cạnh khác nhau của mục đích tìm kiếm.

### 2. Query-to-passage Expansion
- Mỗi truy vấn phụ được mở rộng thành một đoạn văn giả định (pseudo-document) giàu thông tin.

### 3. Late Fusion with RRF
- Mỗi đoạn văn + truy vấn gốc được dùng để truy xuất độc lập.
- Các kết quả được kết hợp bằng thuật toán **Reciprocal Rank Fusion**.

---

## 📊 Benchmark Results

### ✅ Datasets (BEIR benchmark)
- DBPEDIA, FIQA-2018, NFCORPUS, TREC-COVID, TOUCHE-2020

### 📈 Performance Summary
| Method         | Avg Recall@1k | Avg nDCG@10 |
|----------------|----------------|-------------|
| Raw Query      | 66.37          | 33.84       |
| Query2Doc      | 70.44          | 39.56       |
| MILL           | 70.98          | 41.72       |
| **MMLF (ours)**| **73.50**      | **44.16**   |

---

## 🔍 Ablation Highlights

- **RRF** vượt trội hơn so với các kỹ thuật hợp nhất như CombSUM hay concat.
- Việc giữ lại **truy vấn gốc** trong quá trình hợp nhất kết quả giúp cải thiện hiệu quả truy hồi.
- Pipeline hai bước **MQ2MP** (tách riêng việc tạo sub-query và mở rộng passage) mang lại hiệu quả cao hơn so với các pipeline một bước.

---

## ⚠️ Limitations

- **Chi phí tính toán cao**: Sinh nhiều truy vấn phụ và mở rộng passage qua LLM rất tốn thời gian và tài nguyên.
- **Tải truy hồi cao**: Mỗi passage được truy xuất riêng biệt, làm tăng khối lượng công việc.
- Chưa đánh giá tác động của số lượng truy vấn phụ (fix = 3).

---

## 📂 Resources

- 💻 Code here!
- 📄 Full paper: NAACL 2025 Proceedings [https://aclanthology.org/2025.findings-naacl.367.pdf](https://aclanthology.org/2025.findings-naacl.367.pdf)

---

## 📚 Citation

```bibtex
@inproceedings{kuo2025mmlf,
  title={MMLF: Multi-query Multi-passage Late Fusion Retrieval},
  author={Kuo, Yuan-Ching and Yu, Yi and Chen, Chih-Ming and Wang, Chuan-Ju},
  booktitle={Proceedings of the 2025 Conference of the North American Chapter of the Association for Computational Linguistics (NAACL)},
  year={2025},
  pages={6602--6613}
}
