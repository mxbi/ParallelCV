## ParallelCV - Multi-threaded cross-validation for KNIME

ParallelCV is a meta-node for KNIME, similar in functionality to the X-Partitioner/X-Agreggator, except that it performs all folds in parallel. On single-threaded workloads (such as the MultiLayerPerceptron Learner), this produces an output **5x faster** than using traditional CV. This has no effect on performance when working with workloads that are already multithreaded (e.g. Random Forests)

#### Features

- 5x faster than built-in tools
- Equal folds regardless of dataset size
- Results are in the same order as input
- Robust against uneven fold sizes (remainder gets placed into 5th fold)

#### Shortcomings

- 5-fold cross-validation only
- No performance benefit with multi-threaded loads
