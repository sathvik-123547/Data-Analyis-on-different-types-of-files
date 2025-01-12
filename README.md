# README for Assignment Solution

## Overview
This repository contains solutions for the evaluation and analysis of retrieval models, including QL, BM25, and DPR, applied to a set of queries. The primary focus is to:

1. Compute and compare Average Precision (AP) values for the models.
2. Interpret the results and speculate on the reasons for observed differences.
3. Handle edge cases such as queries with no retrieved documents.
4. Generate a precision/recall graph for a specific query (141630) across the three models.

---

## Code Structure

### 1. `comparison_table`
This function creates a table that compares the AP values of QL, BM25, and DPR models for all queries. It also calculates the percentage improvement of QL and DPR over BM25.

**Output Format:**
| Query ID | BM25 AP | QL AP | BM25 → QL (%) | DPR AP | BM25 → DPR (%) |
|----------|---------|-------|-------------------|--------|-------------------|

**Key Features:**
- Reads evaluation files for each model.
- Uses the `eval` function to compute AP values.
- Calculates percentage improvements for clear comparison.
- Prints results directly to the console.

### 2. `eval`
This function computes evaluation measures for queries based on their trecrun and qrels files. It outputs detailed metrics such as AP, P@13, R@13, and nDCG@23.

**Main Metrics Computed:**
- Average Precision (AP)
- Precision at 13 (P@13)
- Recall at 13 (R@13)
- F1 Score at 13 (F1@13)
- nDCG at 23 (nDCG@23)

### 3. Precision/Recall Graph for Query 141630
This part generates a precision/recall graph for query 141630, comparing QL, BM25, and DPR.

**Steps:**
1. Extract precision and recall data for each model during evaluation.
2. Use matplotlib to plot precision vs. recall curves for all models on the same graph.

---

## How to Run
1. Clone the repository and navigate to the folder:
   ```bash
   git clone <repo-url>
   cd <repo-folder>
   ```
2. Place the required evaluation files (`*.trecrun` and `qrels`) in the designated directory.
3. Run the `comparison_table` function to generate and display the AP comparison table.
   ```python
   from solution import comparison_table
   comparison_table()
   ```
4. To generate the precision/recall graph for query 141630, use:
   ```python
   from solution import plot_precision_recall
   plot_precision_recall()
   ```

---

## Results Interpretation
### 4.1 Comparison Table
- QL generally improves upon BM25 due to its probabilistic nature, offering better term weighting.
- DPR shows significant improvement over BM25 and QL due to its neural-based dense passage retrieval capabilities.

### 4.2 AP with No Retrieved Documents
- AP is 0.0 when no documents are retrieved, as no precision can be accumulated. This is consistent with evaluation standards to penalize empty retrievals.

### 4.3 Precision/Recall Graph
- The graph highlights the trade-offs between precision and recall for QL, BM25, and DPR.
- DPR typically outperforms the other models due to its ability to retrieve dense representations of relevant documents.

---

## Dependencies
- Python 3.x
- `matplotlib` for graphing
- Evaluation scripts compatible with TREC format

---

## File Structure
```
.
├── solution.py         # Main solution script with all functions
├── README.md           # This file
├── evaluation_data/    # Directory containing input trecrun and qrels files
└── output/             # Directory for storing temporary evaluation outputs
```

---

## License
This project is licensed under the MIT License. See the LICENSE file for details.

