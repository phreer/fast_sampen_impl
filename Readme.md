# fast_sampen_impl: Implementation for Fast Sample Entropy Computation
This repository contains a program for **fast computation** of **Sample
Entropy**, based on kd tree, range-kd tree and randomly sample (Monte Carlo and
quasi-Monte Carlo) method.

## Requirements
Currently only Linux is supported.

## Description
Depending on the sample method employed, the randomly sample based methods can
be divided to Monte Carlo based (called **MCSampEn**) or quasi-Monte Carlo based
(**QMCSampEn**). As far as MCSampEn is concerned, according to whether the
sample process is with replacement or not, we have two variants denominated as
**MCSampEnWR** and **MCSampEnWOR** respectively. These methods estimate the
sample entropy of a time series from the subset of templates of the original
set. Two parameters involve in the usage of randomly sample based methods: N0
and N1. For each trial, a down-sampled subset with size N0 of the templates will
be drawn from the original set of templates, on which we will perform range
counting. For each estimation of sample entropy, N1 trials will be performed and
the outcomes of these trials will be averaged to approximate the groundtruth
number of matched pairs and used to produced an estimated sample entropy.

For convenience, direct methods are also provided, including simple direct
method, which performs range counting by definition of sample entropy and fast
direct method available on https://physionet.org/content/sampen/1.0.0/ [2].

Besides, the program also contains two kd tree based algorithms, of which the
first one is the simple kd tree method without any optimization and the second
one is called sliding kd tree as described in [1].

Lastly, a new method called range-kd tree is also introduced, whose main
structure is a kd tree. The main tree of a range-kd tree is a m-dimensional kd
tree. The range-kd tree method allows us to compute sample entropy by building
only one kd tree by attaching each node in the tree a additional tree (not be
confused with the children) built as a binary search tree from the
set of (m+1)-component of the templates the node represents. This method
achieves considerable speedup compared with sliding kd tree.

## Usage
First, clone this repository or just download the `.AppImage` file in `Linux`
folder. Then run it with option `-h` for help. The following table lists the
shipped algorithms and the corresponding options. For all the methods, arguments
`--input`, `-n`, `-r`, `-m` should be passed to the program for the input file
name, data length, threshold for similarity and template length. For sample
based algorithms, parameters N0 and N1 should be specified by `--sample-size`
and `--sample-num` respectively. It is as well reccomended to use
`--output-level 0` to suppress unnecessary outputs.

| method  | option |
|---|---|
| direct | `-d` \| `--direct` |
| fast direct | `-fd` \| `--fast-direct` |
| simple kd tree | `--simple-kdtree` |
| sliding kd tree | `-skd` \| `--sliding-kdtree` |
| range-kd tree | `-rkd` \| `--range-kdtree` |
| MCSampEnWR | `-u` \| `--uniform` |
| MCSampEnWOR | `--swr` |
| QMCSampEn | `-q` |

Note that the `--input-format` argument is important for reading inputs. Two
formats is supported of which the first one looks like
```
5
3
4
55
...
```
which we called `simple` format, and the second looks like
```
1 34 23
2 43 41
3 42 1
...
```
which we called `multirecord` format. When reading `multirecord` files, 
only the second column will be read and returned while others will be omitted.


## Reference
[1] Y.-H. Pan, Y.-H. Wang, S.-F.
Liang, and K.-T. Lee, “Fast computation of sample entropy and approximate
entropy in biomedicine,” Computer Methods and Programs in Biomedicine, vol. 104,
no. 3, pp. 382–396, Dec. 2011, doi: 10.1016/j.cmpb.2010.12.003.

[2] Goldberger, A., Amaral, L., Glass, L., Hausdorff, J., Ivanov, P. C., Mark,
R., ... & Stanley, H. E. (2000). PhysioBank, PhysioToolkit, and PhysioNet:
Components of a new research resource for complex physiologic signals.
Circulation [Online]. 101 (23), pp. e215–e220.