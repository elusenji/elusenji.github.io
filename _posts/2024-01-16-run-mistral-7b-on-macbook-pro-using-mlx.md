---
title: Run Mistral 7B on a MacBook Pro using MLX
date: 2023-01-16 21:30:00 +0300
categories: [Machine Learning]
tags: [apple, mlx]     # TAG names should always be lowercase
---

Last month, [Apple released the MLX framework](https://ml-explore.github.io/mlx/build/html/index.html), an open source machine learning framework for deploying and running machine learning models on Apple Silicon. MLX's Python API closely mirrors the NumPy syntax, making it familiar and easier to learn and use.

Here's a quick, beginner friendly guide to running Mistral 7B (a large language model from Mistral AI) on a Macbook Pro using MLX.

First, we'll start by installing MLX:

> Requirements: M-series chip, Python >= 3.8, MacOS >= 13.3

Create a directory 'mlx'

```bash
mkdir mlx && cd mlx
```

Create and activate a Python virtual enviroment

```bash
python3 -m venv env
source ./env/bin/activate
```

Install MLX framework from PyPI

```bash
pip install mlx
```

The next step is to install the Mistral 7B LLM

First, clone the MLX examples repo from Github:

```bash
git clone https://github.com/ml-explore/mlx-examples.git
```
Navigate to the Mistral directory:

```bash
cd mlx-examples && cd llms && cd mistral
```
Install the dependencies:
```python
pip install -r requirements.txt
```

Next, download the model and tokenizer:
> This takes a while to download about ~13.4 GB model files. Feel free to make a cup of coffee...


```bash
curl -O https://files.mistral-7b-v0-1.mistral.ai/mistral-7B-v0.1.tar
tar -xf mistral-7B-v0.1.tar
```

Convert the weights. This step converts the weights from Pytorch compatible to MLX compatible (that can be directly loaded to MLX) and writes them in an NPZ file.

```python
python convert.py
```

Generate sample text with the Mistral 7B model:

```python
python mistral.py --prompt "Out in the savannah, where lions roam free"
```

I ran this on an M2 with 16GB RAM, and it was quite slow- generating a mere 6 words in a period of 7 minutes. Some redditors have had significantly better results with 24GB RAM and more.

However, despite the memory constraints, this was a good chance to play around with MLX and test out its capabilities.