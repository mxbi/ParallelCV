## ParallelCV - Multi-threaded cross-validation for KNIME

ParallelCV is a meta-node for KNIME, similar in functionality to the [X-Partitioner](https://www.knime.org/files/nodedetails/_mining_meta_mining_crossvalidation_X_Partitioner.html)/[X-Agreggator](https://www.knime.org/files/nodedetails/_mining_meta_mining_crossvalidation_X_Aggregator.html), except that it performs each fold on a seperate thread in parallel.

On single-threaded workloads (such as training a [Multi-Layer Perceptron](https://www.knime.org/files/nodedetails/_mining_nn_mlp_RProp_MLP_Learner.html)), and a CPU with >4 threads, this has a **5x speed increase** versus traditional CV. However, on workloads which are multi-threaded already (eg. Random Forests), this has no performance impact.

#### Features

- 5x faster than built-in tools
- Equal folds regardless of dataset size
- Results are in the same order as input
- Robust against uneven fold sizes (remainder gets placed into 5th fold)
- Drop in replacement for X-Paritioner/Aggregator

#### Shortcomings

- 5-fold cross-validation only
- No performance benefit with multi-threaded loads
- Learner/Predictor must be duplicated for each fold in workflow due to KNIME limitations

#### Bugs

- No bugs, just features

## Install

Head over to the [releases](https://github.com/mxbi/ParallelCV/releases) page to download the latest zip file. In KNIME, choose File -> Import Workflow and select the Workflow zip file. This contains a workflow with the ParallelCV Partitioner and Agreggator setup in an example, ready to copy to another Workflow.

Alternatively, you can `git clone` and place the 'Workflow' folder in your KNIME Workspace directory.

## Usage

1. Copy the Paritioner and Aggregator nodes to your workflow
2. Connect the input table to the input port of the ParallelCV-Partitioner
3. Duplicate your Predictor/Learner pair for each fold and connect each one to a pair of train/test ports on the node as per the below layout
4. Take the labeled output table from your learner and connect them to the Aggregator.
5. Connect the output of the Aggregator and use it in your workflow

![Image of the node port layout](https://raw.githubusercontent.com/mxbi/ParallelCV/master/node-ports.png)

Unfortunately due to limitations in the way KNIME works, this requires a seperate learner/predictor copy for each fold. If you want to control the parameters for all folds at once, use a [**Table Creator**](https://www.knime.org/files/nodedetails/_io_io_other_Table_Creator.html) with a **Table Row to Variable** node to pass parameters as flow variables to your learner.

## Under the hood

The **partitioner** is essentially a bunch of Math Formula nodes which calculate the start and endpoints of each fold. These are then converted into flow variables, merged, and passed to a Row Filter which creates the train/test sets for each fold. The **aggregator** takes the output tables from the predictor and concanetates them back into one table.

![Image of the internal node layout](https://raw.githubusercontent.com/mxbi/ParallelCV/master/node-internals.png)
