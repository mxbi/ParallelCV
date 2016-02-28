## ParallelCV - Multi-threaded cross-validation for KNIME

ParallelCV is a meta-node for KNIME, similar in functionality to the X-Partitioner/X-Agreggator, except that it performs each fold on a seperate thread in parallel.

On single-threaded workloads (such as the MultiLayerPerceptron Learner), and a CPU with >4 threads, this has a **5x speed increase** versus traditional CV. However, on workloads which are multi-threaded already (eg. Random Forests), this has no performance impact.

#### Features

- 5x faster than built-in tools
- Equal folds regardless of dataset size
- Results are in the same order as input
- Robust against uneven fold sizes (remainder gets placed into 5th fold)

#### Shortcomings

- 5-fold cross-validation only
- No performance benefit with multi-threaded loads
