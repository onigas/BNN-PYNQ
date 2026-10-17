# CIFAR-10 test batch

`test_batch.bin` is the unmodified binary test batch from CIFAR-10, containing 10,000 colour images (32 × 32 pixels) and labels. The training set is not included.

Original dataset and citation: https://www.cs.toronto.edu/~kriz/cifar.html

Dataset authors: Alex Krizhevsky, Vinod Nair, and Geoffrey Hinton. Please cite Alex Krizhevsky, *Learning Multiple Layers of Features from Tiny Images*, 2009, when using the dataset.

Obtained from the binary archive mirrored at https://data.brainchip.com/dataset-mirror/cifar10/cifar-10-binary.tar.gz and verified against the original archive MD5: `c32a1d4ab5d03f1284b67883e8d87530`.

- Size: 30,730,000 bytes
- SHA-256: `8e2eb146ae340b09e24670f29cabc6326dba54da8789dab6768acf480273f65b`

Notebook 03 downloads this file once into `bnn/cifar-10-batches-bin/` and reuses it on subsequent runs.
