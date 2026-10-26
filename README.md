# BNN-PYNQ PIP INSTALL Package

## Important: Install BNN-PYNQ on the board before running notebooks

**Cloning this repository is not enough.** The Jupyter notebooks use `import bnn`, so the `bnn` Python package must be installed **on the PYNQ-Z2 board**, not on the student's PC.

On the board, open a terminal (Jupyter Terminal or SSH). **Any working directory is fine.** Run:

```bash
sudo pip3 install git+https://github.com/onigas/BNN-PYNQ.git
```

After installation, restart the Jupyter kernel and open the notebooks under `/home/xilinx/jupyter_notebooks/bnn/`. Check with:

```python
import bnn
```

**Note:** The original installation instructions were tested through PYNQ 2.5. PYNQ 3.0.1 compatibility has not been confirmed. Reinstallation may replace the contents of the Jupyter `bnn/` notebook folder; back up edited notebooks first.

---

This repo contains the pip install package for Quantized Neural Network (QNN) on PYNQ. 
Two different network topologies are here included, namely CNV and LFC as described in the <a href="https://arxiv.org/abs/1612.07119" target="_blank"> FINN Paper </a>. 
Now, there are multiple implementations available supporting different precision for weights and activation:

- 1 bit weights and 1 bit activation (W1A1) for CNV and LFC
- 1 bit weights and 2 bit activation (W1A2) for CNV and LFC
- 2 bit weights and 2 bit activation (W2A2) for CNV

We support 3 boards for hardware acceleration which are Pynq-Z1, Pynq-Z2 and Ultra96 (with PYNQ image).

Note, this repository has now been archived and is no longer being actively maintained.
If you are relying on this repository, we strongly recommend you switch to the [FINN compiler](https://github.com/xilinx/finn).

## Notebook execution order

Run the notebooks in the following order. All eleven notebooks are in the same `notebooks/` directory.

| Order | Notebook |
| --- | --- |
| 1 | [01_CNV-BNN_Cifar10.ipynb](notebooks/01_CNV-BNN_Cifar10.ipynb) |
| 2 | [02_CNV-QNN_Cifar10.ipynb](notebooks/02_CNV-QNN_Cifar10.ipynb) |
| 3 | [03_CNV-QNN_Cifar10_Testset.ipynb](notebooks/03_CNV-QNN_Cifar10_Testset.ipynb) |
| 4 | [04_CNV-QNN_Cifar10_Webcam.ipynb](notebooks/04_CNV-QNN_Cifar10_Webcam.ipynb) |
| 5 | [05_LFC-QNN_MNIST.ipynb](notebooks/05_LFC-QNN_MNIST.ipynb) |
| 6 | [06_LFC-BNN_MNIST_Webcam.ipynb](notebooks/06_LFC-BNN_MNIST_Webcam.ipynb) |
| 7 | [07_LFC-BNN_Chars_Webcam.ipynb](notebooks/07_LFC-BNN_Chars_Webcam.ipynb) |
| 8 | [08_CNV-BNN_Road-Signs.ipynb](notebooks/08_CNV-BNN_Road-Signs.ipynb) |
| 9 | [09_CNV-BNN_SVHN.ipynb](notebooks/09_CNV-BNN_SVHN.ipynb) |
| 10 | [10_CIFAR10_Live_Webcam.ipynb](notebooks/10_CIFAR10_Live_Webcam.ipynb) |
| 11 | [11_GTSRB_Webcam.ipynb](notebooks/11_GTSRB_Webcam.ipynb) |

Notebook 10 extends the original Xilinx examples with continuous USB-camera capture using the pretrained CNV-W1A1 model on the FPGA. It displays accelerator timing, Python call timing, and application FPS.

For notebook 10, first run notebook 01 successfully. Download the notebook into the board's Jupyter folder and run its cells in order. The default session lasts 30 seconds; use **Kernel → Interrupt** to stop sooner. No package reinstallation is needed. Shut down other camera/BNN kernels first.

The live notebook includes a central crop, an enlarged 32 × 32 input view, camera cleanup, and student experiments. Code and camera cleanup paths have been checked with simulated devices; physical PYNQ/C270 validation is still required.

Notebook 11 uses the existing `road-signs` CNV-W1A1 FPGA model with 43 traffic-sign classes plus a “Not a roadsign” class. It starts with two file-based reference checks, then classifies the central region of a USB-camera image. Use printed signs or a phone display, leaving the PC screen for Jupyter. Run the cells in order; the camera starts only in section 6 and stops after 30 seconds or 300 frames. Use **Kernel → Interrupt** to stop early. Camera/FPGA validation is required on the board.

## FPGA-only network benchmark

[01.1 — CNV-W1A1 FPGA benchmark](notebooks/01.1_CNV-BNN_Cifar10_FPGA_Benchmark.ipynb)
uses the existing CIFAR-10 hardware runtime; all six convolutions, two pooling operations
and three fully connected layers run in the FPGA. Run it on PYNQ with BNN already installed,
after shutting down other FPGA notebook kernels. No reinstall or hardware rebuild is needed.

The notebook reports native `ExecAccel` timing, full API duration with prepared input,
and image-file-to-class duration separately, using warm-up and repeated measurements.
Native timing includes launch/polling and excludes host packing and buffer copies;
it is not a pure FPGA cycle count. Temporary CIFAR inputs use `/dev/shm` and are removed.
CNV scores are integer rankings, not probabilities. Historical ImageNet timings are context
only: CIFAR-10 CNV uses a different model, input size and class count.
Python control-flow checks use a mocked BNN interface; real hardware timing must be measured on PYNQ.

## Citation
If you find BNN-PYNQ useful, please cite the <a href="https://arxiv.org/abs/1612.07119" target="_blank">FINN paper</a>:

    @inproceedings{finn,
    author = {Umuroglu, Yaman and Fraser, Nicholas J. and Gambardella, Giulio and Blott, Michaela and Leong, Philip and Jahre, Magnus and Vissers, Kees},
    title = {FINN: A Framework for Fast, Scalable Binarized Neural Network Inference},
    booktitle = {Proceedings of the 2017 ACM/SIGDA International Symposium on Field-Programmable Gate Arrays},
    series = {FPGA '17},
    year = {2017},
    pages = {65--74},
    publisher = {ACM}
    }

## Quick Start

Please refer to PYNQ <a href="https://pynq.readthedocs.io/en/latest/getting_started.html" target="_blank"> Getting Started</a> guide to set-up your PYNQ Board.

In order to install it to your PYNQ, connect to the board, open a terminal and type:

```
sudo pip3 install git+https://github.com/Xilinx/BNN-PYNQ.git (on PYNQ v2.3 and later versions, tested up to v2.5)
sudo pip3.6 install git+https://github.com/Xilinx/BNN-PYNQ.git (on PYNQ v2.2 and earlier)
```

This will install the BNN package to your board, and create a **bnn** directory in the Jupyter home area. You will find the Jupyter notebooks to test the networks in this directory.

## Repo organization 

The repo is organized as follows:

-	bnn: contains the LfcClassifier and CnvClassifier python class description
	-	src: contains the sources of the different precision networks, the libraries to rebuild them, and scripts to train and pack the weights:
		- library: FINN library for HLS QNN descriptions, host code, script to rebuilt and drivers for the PYNQ and Ultra96 (please refer to README for more details)
		- network: HLS top functions for QNN topologies (CNV and LFC) with different implementations for weight and activation precision, host code and make script for HW and SW build (please refer to README for more details)
		- training: scripts to train on the Cifar10, GTSRB and MNIST datasets and scripts to pack the weights in a binary format which can be read by the overlay
	-	bitstreams: contains the bitstreams for the 5 overlays
		- pynqZ1-Z2: bitstreams for Pynq devices
		- ultra96: bitstreams for Ultra96 devices
	-	libraries: pre-compiled shared objects for low-level driver of the 5 overlays each for hardware and software runtime
		- pynqZ1-Z2: shared objects used by Pynq devices
		- ultra96: shared objects used by ultra96
	-	params: set of trained parameters for the 5 overlays:
		- <a href="http://yann.lecun.com/exdb/mnist/" target="_blank"> MNIST </a> and <a href="https://www.nist.gov/srd/nist-special-database-19" target="_blank"> NIST </a> dataset for LFC network. Note that NIST dataset is only applicable to LFC-W1A1 by default.
		- <a href="https://www.cs.toronto.edu/~kriz/cifar.html" target="_blank"> Cifar10 </a>, <a href="http://ufldl.stanford.edu/housenumbers/" target="_blank"> SVHN </a> and <a href="http://benchmark.ini.rub.de/?section=gtsdb&subsection=dataset" target="_blank"> German Road Signs </a> dataset for CNV network. Note that SVHN and German Road Signs databases are only applicable to CNV-W1A1 by default.
-	notebooks: lists a set of python notebooks examples, that during installation will be moved in `/home/xilinx/jupyter_notebooks/bnn/` folder
-	tests: contains test script and test images

## Hardware design rebuilt

In order to rebuild the hardware designs, the repo should be cloned in a machine with installation of the Vivado Design Suite (tested with 2018.2). 
Following the step-by-step instructions:

1.	Clone the repository on your linux machine: `git clone https://github.com/Xilinx/BNN-PYNQ.git --recursive`;
2.	Move to `<clone_path>/BNN_PYNQ/bnn/src/network/`
3.	Set the XILINX_BNN_ROOT environment variable to `<clone_path>/BNN_PYNQ/bnn/src/`
4.	Launch the shell script make-hw.sh with passing parameters for target network, target platform and mode, with the command `./make-hw.sh {network} {platform} {mode}` where:
	- network can be cnvW1A1, cnvW1A2, cnvW2A2 or lfcW1A1, lfcW1A2;
	- platform can be pynqZ1-Z2 or ultra96;
	- mode can be `h` to launch Vivado HLS synthesis, `b` to launch the Vivado project (needs HLS synthesis results), `a` to launch both;
5.	The results will be visible in `clone_path/BNN_PYNQ/bnn/src/network/output/` that is organized as follows:
	- bitstream: contains the generated bitstream(s);
	- hls-syn: contains the Vivado HLS generated RTL and IP (in the subfolder named as the target network and target platform);
	- report: contains the Vivado and Vivado HLS reports;
	- vivado: contains the Vivado project;
6.	Copy the generated bitstream, hwh and tcl script on the PYNQ board `pip_installation_path/bnn/bitstreams/`

