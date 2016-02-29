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

#### Bugs

- No bugs, just features

## Install/Usage

**Install:** Head over to the [releases](https://github.com/mxbi/ParallelCV/releases) page to download the latest zip file. In KNIME, choose File -> Import Workflow and select the Workflow zip file. This contains a workflow with the ParallelCV Partitioner and Agreggator setup in an example, ready to copy to another Workflow.

Alternatively, you can `git clone` and place the folder in your KNIME Workspace directory.
