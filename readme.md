# HNSW study scratchpad

## HNSW parameters

### Search Parameters

- What is ef? - the size of the dynamic list for the nearest neighbors.
- What if ef is high? - more accurate but slower search
- Ef cannot be set lower than the number of k. Why?
  The remaining k results after executing the algorithm becomes the resulting output.

- Ef cannot be set higher than the size of the dataset.
  It can be anything between k and the size of the dataset.
- What happens if ef is too small? - If ef is set too low,
  the search may not be accurate enough.
  It might fail to find the k nearest neighbors.

- what is k? - number of nearest neighbors to be returned.

### Construction Parameters

- What is the purpose of the M parameter
  - The M parameter controls the number of bi-directional links
    created for each new element during the graph's construction.
    A higher m improves performance for high-dimensional datasets
    and high recall,
    while a lower M is suitable for low-dimensional datasets.
  - M = 6 is optimal for dim 4 vectors.
  - M = 12-48 is ok for the most of the use cases.
  - If M is changed, one has to update the other parameters.
  - You can assume `M * ef` or `M * ef_construction` is a constant.
- What is the purpose of ef_construction
  - What is the difference btw ef? - It controls the index quality during construction.
    Higher values of ef_construction
    results in longer construction times.
  - How to tell if ef_construction is well-chosen? - Perform search
    ef = ef_construction. If recall is below 0.9,
    there may be room for improvement.
- What is num_elements?
  - It is the maximum number of elements that can be
    stored in the index. If you need to extend, you use
    load_index function and specify a new maximum number of elements.

### Misc

- How is memory usage affected by the algorithm's parameters?
  - Memory consumption is manily affected by the M parameter.
    Each element inthe index consumes M \* (8 - 10) bytes.
- What tradeoffs in tuning parameters?
  - ef, ef_construction improves accuracy, but at the cost of slower search and index build times.
  - M improves performance on high-dimensional data but increases memory usage.
