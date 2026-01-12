# Prediction-of-TATA-DNA-Sequence
DNA Sequence Classification: TATA Box Detection Using LSTM
Overview
This project uses Deep Learning (LSTM neural networks) to classify DNA sequences based on the presence or absence of TATA box motifs. The TATA box is a crucial promoter element found in the DNA of eukaryotes, playing a vital role in gene transcription regulation.

Table of Contents

Project Description
Dataset
Installation
Usage
Model Architecture
Results
Project Structure
Future Work
References

Project Description
Problem Statement
Identifying regulatory elements like TATA boxes in DNA sequences is essential for understanding gene expression mechanisms. This project creates labeled training data by detecting TATA box motifs using pattern matching, then trains a deep learning model to learn and predict these patterns automatically.
Approach

Label Creation: Pattern matching using IUPAC nucleotide codes to identify TATA boxes in unlabeled sequences
Sequence Tokenization: Converting DNA sequences (A, T, G, C) into numerical representations
Deep Learning: Bidirectional LSTM networks for binary classification
Evaluation: Comprehensive performance metrics including accuracy, AUC, and confusion matrices

Key Innovation
Unlike traditional supervised learning where labels are pre-existing, this project generates its own labels by detecting specific TATA box motif patterns in the DNA sequences, then trains a neural network to learn these patterns and generalize to new sequences.
Dataset
Input Data

NucleotideSequence: Raw DNA sequences containing nucleotides (A, T, G, C)
NCBIGeneID: Gene identifiers from NCBI database

Label Generation
The target variable MotifPresent is created programmatically by scanning each sequence for TATA box patterns:
Motif Patterns Detected

TATAAA: Exact canonical TATA box sequence
TATAWAWR: Variant pattern where:

W = A or T
R = A or G
Regex: TATA[AT]A[AG][AG]


Data Preprocessing

Label generation from unlabeled DNA sequences
Dataset balancing using undersampling to handle class imbalance
Sequence tokenization at character level
Padding sequences to uniform length (200 nucleotides)

Installation
Requirements


### Key Features
- **Character-level Embedding**: Each nucleotide (A, T, G, C) is embedded in 32-dimensional space
- **Bidirectional LSTM**: Captures sequential patterns from both forward and backward directions
- **Dropout Regularization**: Prevents overfitting (0.2 recurrent, 0.3 final layer)
- **Binary Classification**: Sigmoid activation outputs probability of TATA box presence

### Why LSTM?
DNA sequences have sequential dependencies - nucleotides at different positions interact to form functional motifs. LSTM networks excel at learning such long-range dependencies in sequences.


Model Enhancements

Experiment with CNN-LSTM hybrid architectures
Implement attention mechanisms for interpretability
Try Transformer-based models (BERT for genomics)


Data Augmentation

Reverse complement sequences
Sliding window approaches
Synthetic sequence generation using GANs


Extended Analysis

Compare rule-based vs. learned patterns
Feature importance analysis
Cross-species validation
Handle variable-length sequences


Real-world Applications

Predict promoter strength
Identify mutations affecting TATA boxes
Integrate with gene expression data


Limitations

Label Quality: Labels are generated from pattern matching, which may miss subtle variations
Fixed Length: Sequences are padded/truncated to 200 nucleotides
Binary Classification: Doesn't capture TATA box strength or exact position
Limited Patterns: Only detects two specific TATA box motifs

