# ML‑Agents Advanced Installation Guide  

This single Markdown document contains everything you need to get Unity’s **ML‑Agents 4.x** running in a reproducible Conda environment with the latest stable GitHub release and a fix for the `pkg_resources` error that appears on modern Python versions.

---

## Overview

- Create an isolated Conda environment (`mlagents`) with Python 3.10.11  
- Install the correct PyTorch wheel (CUDA 12.1)  
- Clone the `release_23` branch of the official ML‑Agents repository  
- Install the two pip packages in the proper order  
- Pin `setuptools==81.0.0` to avoid a `ModuleNotFoundError: No module named 'pkg_resources'` on Python ≥ 3.12  
- Verify with `mlagents-learn --help`

---

## Prerequisites

| Item | Minimum version |
|------|-----------------|
| **Python** | 3.10.11 (or newer) |
| **Conda** | Miniconda / Anaconda |
| **CUDA Toolkit** | CUDA 12.1 (for the GPU‑enabled PyTorch wheel) |
| **Git** | Any recent version |

> ⚙️ If you already have a suitable Python environment, skip to **Step 2: Clone and install ML‑Agents**.

---

## Step 0 – Read the Official Documentation

The Unity docs provide essential background:
<https://docs.unity3d.com/Packages/com.unity.ml-agents@4.0/manual/Installation.html>

> Use the following commands as a reproducible rewrite of those instructions.

---

## 1️⃣ Create and Activate the Conda Environment

```bash
# following instructions in: https://docs.unity3d.com/Packages/com.unity.ml-agents@4.0/manual/Installation.html
conda create -n mlagents python=3.10.11
conda activate mlagents
pip3 install torch~=2.2.1 --index-url https://download.pytorch.org/whl/cu121

# advanced installation relies on latest stable release from git. Simple one install packages directly I think
git clone --branch release_23 https://github.com/Unity-Technologies/ml-agents.git

# install packages inside cloned project in the correct order!
cd /path/to/ml-agents
python -m pip install ./ml-agents-envs
python -m pip install ./ml-agents

# when calling mlagents-learn --help I get the error ModuleNotFoundError: No module named 'pkg_resources'
# apparently pkg_resources has been removed from "modern" python versions so we need to install an older version
# see the end of https://github.com/ManimCommunity/manim/issues/3585
pip install setuptools==81.0.0

# this should work now with a warning about pkg_resources only
mlagents-learn --help 
```

---

## 🎉 You’re Ready!

- **ML‑Agents** is now installed and ready for training environments, simulations, or contribution to the repo.
- If anything breaks, double‑check each step above and consult the Unity ML‑Agents docs or ask me.  
