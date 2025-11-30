TensorFlow GPU Setup on Windows Native (RTX 3090)
TensorFlow 2.10 — Last Version Supporting GPU on Windows Native

⚠️ Important:
TensorFlow 2.10 is the last version that supports GPU on native Windows.
Anything above 2.10 will NOT detect the GPU unless using WSL2 or DirectML.

📌 Overview

This guide explains how to install TensorFlow 2.10 GPU on Windows Native, using:

NVIDIA RTX 3090 (Compute Capability 8.6)

Windows 10/11 (64-bit)

System CUDA 12.4 + Latest NVIDIA Drivers (does NOT affect conda setup)

Conda environment with CUDA 11.2 + cuDNN 8.1

TensorFlow requires exact versions to work on Windows GPU.

Component	Required Version
CUDA Toolkit	11.2
cuDNN	8.1.0
Python	3.9
TensorFlow	2.10
🚀 Installation Guide (Step-by-Step)
1️⃣ Install Microsoft Visual C++ Redistributable

TensorFlow on Windows requires the MSVC runtime.

Download & install:
Microsoft Visual C++ Redistributable (2015–2022)

2️⃣ Install Miniconda

Download Miniconda for Windows:
https://docs.conda.io/en/latest/miniconda.html

Install using default settings.

3️⃣ Create a Dedicated TensorFlow Environment
conda create --name tf python=3.9
conda activate tf

4️⃣ Install CUDA 11.2 & cuDNN 8.1 Inside Conda

These versions are required specifically for TensorFlow 2.10 GPU:

conda install -c conda-forge cudatoolkit=11.2 cudnn=8.1.0


✔ No conflict with your system CUDA (12.4).
✔ Everything remains isolated inside the environment.

5️⃣ Install TensorFlow 2.10 (GPU — Last Supported Version)

Update pip first:

pip install --upgrade pip


Install TensorFlow:

pip install "tensorflow<2.11"


This ensures TensorFlow 2.10 GPU is installed.

6️⃣ Fix the ptxas.exe Missing Error

If you see:

ptxas.exe not found

Could not find ptxas

GPU fails to compile kernels

Install NVCC inside the environment:

conda install -c nvidia cuda-nvcc


This installs the required ptxas.exe.

7️⃣ Verify Installation
✔️ CPU Test
python -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"


A tensor output means TensorFlow works.

✔️ GPU Detection Test
python -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"


Expected:

[PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]


If empty → GPU was not detected.

🖥️ System Requirements
✔️ Supported GPUs

TensorFlow GPU on Windows supports compute capability ≥ 3.5.
RTX 3090 = Compute Capability 8.6 → Fully supported.

✔️ Supported OS

Windows 10 64-bit

Windows 11 64-bit

⚠ Notes & Limitations
❗ System CUDA (12.x) does NOT matter

TensorFlow uses the conda CUDA:

CUDA 11.2

cuDNN 8.1

System CUDA is ignored.

❗ Do NOT install TensorFlow from Conda

Always install via pip:

Conda builds may be old

GPU support may be missing

❗ GPU Support Removed After TF 2.10

To use TensorFlow ≥ 2.11 with GPU, you must switch to:

Linux

WSL2

TensorFlow-DirectML (not recommended for training)

💡 Final Environment Summary
Component	Version
Python	3.9
TensorFlow	2.10
CUDA Toolkit	11.2
cuDNN	8.1
NVCC / ptxas	Installed via cuda-nvcc
GPU	NVIDIA RTX 3090
