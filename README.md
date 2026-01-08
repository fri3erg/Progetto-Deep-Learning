# Infix to Postfix Notation Translator

This project implements a Deep Learning solution to translate mathematical expressions from **Infix Notation** (e.g., `(a + b) * c`) to **Postfix Notation** (Reverse Polish Notation, e.g., `a b + c *`). 

The core of the solution is a sequence-to-sequence **Transformer** model, designed to be highly accurate while remaining computationally efficient (~550k parameters).

## Project Overview

The goal of this project is to parse parenthesized mathematical expressions with a maximum syntactic depth of 4 and correctly reorder them into postfix form. This task requires the model to understand hierarchical structures and operator precedence, which are inherently ambiguous in infix notation without parentheses.

### Key Features
*   **Architecture**: Transformer Encoder-Decoder.
*   **Efficiency**: Optimized to use only ~550k parameters (limit was 2M).
*   **Accuracy**: Achieves **100.0% accuracy** on the formal test set.
*   **Inference**: Autoregressive decoding for sequence generation.

## Repository Structure

*   **`Infix_to_postfix_notation_FINAL.ipynb`**: The main submission file. Contains the optimized model, training loop, and formal evaluation.
*   **`Infix_to_postifx_notation_specification.ipynb`**: Original project specifications and problem constraints.
*   **`Infix_to_postifx_notation_optimized.ipynb`**: Development version of the optimized model.
*   **`Infix_to_postifx_notation_tiny.ipynb`**: Experimental "Tiny" model (~43k parameters).
*   **`Infix_to_postifx_notation_attempt.ipynb`**: Initial attempts and baseline experiments.

## Model Architecture

The final model moves away from recurrent architectures (LSTMs/GRUs) in favor of a **Transformer**, which effectively captures the nested dependencies of mathematical syntax.

| Hyperparameter | Value | Description |
| :--- | :--- | :--- |
| **Model Type** | Transformer | Encoder-Decoder architecture |
| **Embedding Dimension** | 64 | `D_MODEL` |
| **Layers** | 3 | Encoder and Decoder layers |
| **Heads** | 4 | Multi-head attention |
| **Feed Forward Dim** | 512 | `FF_DIM` |
| **Total Parameters** | **~550,416** | Well below the 2M limit |

## Performance

The model was evaluated on a formal test set of 30 expressions, repeated over 10 rounds.

| Model Variant | Parameters | Accuracy (Mean ± Std) | Notes |
| :--- | :--- | :--- | :--- |
| **Baseline** | ~1.4M | 0.9988 ± 0.0036 | Initial large model (D_MODEL=128) |
| **Optimized (Final)** | **~550k** | **1.0000 ± 0.0000** | **Selected for submission** |
| **Tiny** | ~43k | 0.9960 ± 0.0060 | Extreme compression experiment |

## Usage

1.  Open `Infix_to_postfix_notation_FINAL.ipynb` in Jupyter Notebook or Google Colab.
2.  Run the cells sequentially to:
    *   Generate the dataset.
    *   Build and compile the Transformer model.
    *   Train the model (converges in ~5 epochs).
    *   Run the autoregressive inference and formal test loop.