# Medical QA RAG with Faithfulness Evaluation
## RAI-8001 Applied NLP 

### Project Overview
A Retrieval-Augmented Generation (RAG) pipeline for biomedical question answering
using PubMedQA, with evaluation across three dimensions: retrieval quality,
QA accuracy, and faithfulness to retrieved evidence.

### How to Run

**Environment:** Google Colab with GPU runtime (T4 recommended)

**Steps:**
1. Open `notebooks/pubmedqa_rag.ipynb` in Google Colab
2. Set runtime to GPU: Runtime → Change runtime type → T4 GPU
3. Add your Anthropic API key to Colab Secrets (key icon in left sidebar):
   - Name: `ANTHROPIC_API_KEY`
   - Value: your key from console.anthropic.com
4. Run all cells sequentially

**Note:** The notebook uses Google Drive for persistent storage of intermediate
results (embeddings, FAISS index, generation outputs). On first run, the MedCPT
encoding step takes ~30 minutes. Subsequent runs load cached results automatically.

### Dependencies
See `requirements.txt`. All packages are installed in the first notebook cell.

### Project Structure
```
pubmedqa-rag/
├── notebooks/
│   └── pubmedqa_rag.ipynb            # Main notebook
├── report/
│   └── report.pdf                    # Final report (6 pages)
├── outputs/                          # Figures and evaluation results
├── requirements.txt
├── .gitignore
└── README.md
```

### Architecture
```
Question → Retriever (BM25 / MedCPT / Hybrid) → Top-k Passages → LLM Generator → Answer
                                                                                     ↓
                                                                             Faithfulness Check
                                                                             (Biomedical NLI)
```

### Key Results (Test Set, n=500)

| Metric             | BM25  | MedCPT | Hybrid |
|--------------------|-------|--------|--------|
| Recall@5           | 0.846 | 0.884  | 0.924  |
| Macro F1           | 0.589 | 0.558  | 0.577  |
| Accuracy           | 0.672 | 0.652  | 0.684  |
| Faithfulness       | 56.6% | 60.8%  | 63.2%  |
| Correct & Faithful | 39.8% | 40.4%  | 45.6%  |

### References
- Jin, Q. et al. (2019). PubMedQA. *EMNLP-IJCNLP*.
- Xiong, G. et al. (2024). Benchmarking RAG for Medicine. *ACL Findings*.
- Jin, Q. et al. (2023). MedCPT. *Bioinformatics*.

### Repository
https://github.com/federica896/pubmedqa-rag
