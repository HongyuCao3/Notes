# 📘 Installing Conda on a Linux Server (No sudo Required)

## 1. Overview

Conda (Miniconda/Miniforge) can be installed in a user directory without root privileges. This is standard practice on shared servers, HPC clusters, and research environments.

---

## 2. Installation Steps

### Step 1: Download Installer

```bash
cd ~
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

Or:

```bash
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

---

### Step 2: Run Installer

```bash
bash Miniconda3-latest-Linux-x86_64.sh
```

During installation:

* Press `Enter` to read the license
* Type `yes` to accept
* Install to default path: `~/miniconda3`
* Choose `yes` to initialize Conda

---

### Step 3: Activate Conda

```bash
source ~/.bashrc
conda --version
```

---

### Step 4: Test Environment

```bash
conda create -n test python=3.10
conda activate test
python -V
```

---

## 3. Common Issues

### Issue: `conda: command not found`

Fix:

```bash
echo 'export PATH=$HOME/miniconda3/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

---

### Issue: Auto-activating base environment

Disable:

```bash
conda config --set auto_activate_base false
```

---

## 4. CondaToSNonInteractiveError Explained

### Error Message

```
CondaToSNonInteractiveError: Terms of Service have not been accepted...
```

### Meaning

Conda is trying to access **Anaconda official repositories**:

* `https://repo.anaconda.com/pkgs/main`
* `https://repo.anaconda.com/pkgs/r`

But you have **not accepted their Terms of Service (ToS)**.

This is related to **licensing restrictions**, not a technical failure.

---

## 5. Solutions

### Option 1: Accept Terms of Service

```bash
conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/main
conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/r
```

---

### Option 2 (Recommended): Use conda-forge Only

Remove default channels:

```bash
conda config --remove channels defaults
```

Add conda-forge:

```bash
conda config --add channels conda-forge
conda config --set channel_priority strict
```

---

### Check Current Channels

```bash
conda config --show channels
```

---

## 6. Recommended Setup for Servers (Best Practice)

Most HPC / research environments use:

* **Miniforge instead of Miniconda**
* **conda-forge as the only channel**
* **mamba for faster installs**

### Install Miniforge

```bash
wget https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh
bash Miniforge3-Linux-x86_64.sh
```

---

### Install Mamba

```bash
conda install mamba -n base -c conda-forge
```

Use it like:

```bash
mamba install numpy pandas pytorch
```

---

## 7. Offline Server Installation

If the server has no internet:

1. Download installer locally
2. Upload via `scp`:

```bash
scp Miniconda3-latest-Linux-x86_64.sh user@server:~
```

3. Install normally

---

## 8. Key Takeaways

* Conda does **not require sudo**
* Install into `~/miniconda3` or similar
* ToS error = licensing requirement, not a bug
* Prefer **conda-forge + Miniforge + mamba** on servers
* This setup is faster, cleaner, and avoids licensing issues

