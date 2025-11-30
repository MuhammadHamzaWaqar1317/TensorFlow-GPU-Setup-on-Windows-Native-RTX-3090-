<div align="center">

<img src="https://upload.wikimedia.org/wikipedia/commons/2/2d/Tensorflow_logo.svg" alt="TensorFlow Logo" width="120"/>

# TensorFlow-GPU-Setup-on-Windows-Native-RTX-3090
### TensorFlow 2.10 • Python 3.9 • CUDA 11.2 • cuDNN 8.1 • Windows Native  
(Your system already has CUDA 12.4 — this setup still works.)

[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.10-FF6F00?logo=tensorflow)](https://www.tensorflow.org/)
[![Python](https://img.shields.io/badge/Python-3.9-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![CUDA](https://img.shields.io/badge/CUDA-11.2-76B900?logo=nvidia)](https://developer.nvidia.com/cuda-toolkit)
[![cuDNN](https://img.shields.io/badge/cuDNN-8.1.0-76B900?logo=nvidia)](https://developer.nvidia.com/cudnn)
[![Platform](https://img.shields.io/badge/Windows-Native-0078D6?logo=windows&logoColor=white)](https://www.microsoft.com/windows)

</div>

---

## ⚠️ Important Notice
> **TensorFlow 2.10 is the LAST version that supports GPU on Windows Native.**  
> TensorFlow 2.11+ **WILL NOT** use your GPU unless you use WSL2.

---

## 📌 System Overview

| Component | Requirement |
|----------|-------------|
| **GPU** | NVIDIA RTX 3090 (Compute Capability 8.6) |
| **Python** | 3.9 |
| **CUDA Toolkit** | 11.2 (installed inside Conda) |
| **cuDNN** | 8.1.0 |
| **TensorFlow** | 2.10 |
| **Windows** | Windows 10/11 (64-bit) |

> 💡 **NOTE:** Your system CUDA **12.4** does *not* affect TensorFlow installed inside Conda.

---

## 🚀 Installation Steps

---

### 1️⃣ Install Microsoft Visual C++ Redistributable  
Required for TensorFlow runtime.

📥 Download →  
**https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist**

---

### 2️⃣ Install Miniconda (Recommended)
📥 Download Miniconda →  
**https://docs.conda.io/en/latest/miniconda.html**

Install with default settings.

---

### 3️⃣ Create Conda Environment for TensorFlow

```bash
conda create --name tf python=3.9
conda activate tf
```

### 4️⃣ Install CUDA 11.2 + cuDNN 8.1 (Inside Conda)

These are the versions TensorFlow 2.10 specifically requires.

```bash
conda install -c conda-forge cudatoolkit=11.2 cudnn=8.1.0
```

### 5️⃣ Upgrade Pip


```bash
pip install --upgrade pip
```

---

### 6️⃣ Install TensorFlow 2.10 (GPU)

Install using **pip** — NOT conda.

```bash
pip install "tensorflow<2.11"
```

### 7️⃣ Fix ptxas.exe / NVCC Not Found Error

If TensorFlow shows errors like:
ptxas.exe not found, NVCC missing, GPU kernels cannot compile

Install CUDA-NVCC inside Conda:

```bash
conda install -c nvidia cuda-nvcc
```
This provides ptxas.exe, required for GPU kernel compilation.

### ✅ Verification

✔ CPU Test

```bash
python -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```
You should see a numeric tensor value.

✔ GPU Detection Test

```bash
python -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"
```
Expected output:
```bash
[PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]
```
If this list is empty, TensorFlow could not detect your GPU.

---

## 🖥 Environment Summary

| Component | Version |
|----------|-------------|
| **Python** | 3.9 |
| **TensorFlow** | 2.10 |
| **CUDA Toolkit** | 11.2 (installed inside Conda) |
| **cuDNN** | 8.1.0 |
| **NVCC / ptxas** | Installed using cuda-nvcc |
| **GPU** | RTX 3090 |


---

## ⚠ Notes & Limitations

- System CUDA (12.x) **does NOT affect** TensorFlow inside Conda.
- TensorFlow versions **> 2.10 do NOT support GPU** on Windows Native.
- For TF 2.11+ GPU support, you must use **WSL2 or Linux**.
- Do **NOT** install TensorFlow using Conda — always use **pip**.
