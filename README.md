# Continual Meta Learning Experiments

_This repo is built on top of Meta-Experience Replay (MER): https://github.com/mattriemer/MER (which itself is a fork of GEM https://github.com/facebookresearch/GradientEpisodicMemory)_

----


## Available Datasets

The code in this repository should work on the variants of MNIST used in the experiments. This includes Rotations, Permutations, and Many Permutations. It would need to be slightly extended to be applied to other interesting continual learning benchmarks like CIFAR-100 or Omniglot.

The original MNIST database is available at http://yann.lecun.com/exdb/mnist/ and interface for generating your own MNIST variants is provided as part of the GEM project https://github.com/facebookresearch/GradientEpisodicMemory/tree/master/data.

### Basic Setup

Create a virtual environment (either with Python 3 virtualenv or anaconda)

Install dependencies for Cython (only for GEM code which uses quadprog)
```sudo apt install gcc build-essential```

then simply install all other dependencies
```pip install --user -r requirements.txt```

### Getting the datasets

The first step is to download and uncompress all three datasets (30 GB of storage needed) execute the following command:

```python get_data.py all```

For just MNIST Rotations (4.1 GB) execute:

```python get_data.py rotations```

For just MNIST Permutations (4.1 GB) execute:

```python get_data.py permutations```

For just MNIST Many Permutations (21 GB) execute:

```python get_data.py manypermutations```

## Getting Started

In mer_examples.sh see examples of how to run variants of MER from the paper and baseline models from the experiments. We make sure first that this script is excutable:

```chmod +x mer_examples.sh```

Now, executing the following command leads to running a full suite of experiments with a random seed of 0:

```
./mer_examples.sh "0"
```

Within the file you can see examples of how to run models from our experiments on each datasets and memory size setting. For instance, we can execute MER from Algorithm 1 in the paper (meralg1) on MNIST Rotations with 5120 memories using the following commands:
```
export ROT="--n_layers 2 --n_hiddens 100 --data_path data/ --save_path results/ --batch_size 1 --log_every 100 --samples_per_task 1000 --data_file mnist_rotations.pt --cuda no --seed 0"
python3 main.py $ROT --model meralg1 --lr 0.03 --beta 0.03 --gamma 1.0 --memories 5120 --replay_batch_size 100 --batches_per_example 10
```

## Available Models

- Online Learning (online)

- Task Specific Input Layer (taskinput)

- Independent Models per Task (independent)

- Elastic Weight Consolidation (ewc)

- Gradient Episodic Memory (gem)

- Experience Replay Algorithm 4 (eralg4)

- Experience Replay Algorithm 5 (eralg5)

- Meta-Experience Replay Algorithm 1 (meralg1)

- Meta-Experience Replay Algorithm 6 (meralg6)

- Meta-Experience Replay Algorithm 7 (meralg7)

