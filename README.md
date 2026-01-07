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



Labeling Process
pythondef motif_present(sequence, motifs):
    """
    Scans DNA sequence for TATA box motifs.
    Returns 1 if any motif is found, 0 otherwise.
    """
    for motif_pattern in motifs.values():
        if re.search(motif_pattern, sequence):
            return 1
    return 0

# Create labels for entire dataset
train_data['MotifPresent'] = train_data['NucleotideSequence'].apply(
    lambda x: motif_present(x, motifs)
)
Data Preprocessing

Label generation from unlabeled DNA sequences
Dataset balancing using undersampling to handle class imbalance
Sequence tokenization at character level
Padding sequences to uniform length (200 nucleotides)

Installation
Requirements
bashpip install pandas numpy tensorflow scikit-learn matplotlib seaborn imbalanced-learn
Dependencies
python- Python 3.8+
- TensorFlow 2.x
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- imbalanced-learn

## Model Architecture

### Network Design
```
Input: DNA sequences (padded to length 200)
    ↓
Embedding Layer: 5 tokens → 32 dimensions
    ↓
Bidirectional LSTM: 64 units (dropout 0.2, recurrent_dropout 0.2)
    ↓
Bidirectional LSTM: 32 units (dropout 0.2, recurrent_dropout 0.2)
    ↓
Dropout Layer: 0.3
    ↓
Dense Output: 1 unit (sigmoid) → TATA probability
```

### Key Features
- **Character-level Embedding**: Each nucleotide (A, T, G, C) is embedded in 32-dimensional space
- **Bidirectional LSTM**: Captures sequential patterns from both forward and backward directions
- **Dropout Regularization**: Prevents overfitting (0.2 recurrent, 0.3 final layer)
- **Binary Classification**: Sigmoid activation outputs probability of TATA box presence

### Why LSTM?
DNA sequences have sequential dependencies - nucleotides at different positions interact to form functional motifs. LSTM networks excel at learning such long-range dependencies in sequences.

## Results

### Performance Metrics
*(Update with your actual results)*
- **Accuracy**:  0.7200
- **AUC**: 0.7932


### Interpretation
- **High Accuracy**: Model successfully learned TATA box patterns
- **Confusion Matrix**: Shows true positives, false positives, true negatives, false negatives
- **ROC-AUC**: Measures model's ability to distinguish between TATA and non-TATA sequences


## Workflow Summary
```
Raw DNA Sequences
       ↓
[Motif Detection - Regex Pattern Matching]
       ↓
Labeled Dataset (TATA=1, Non-TATA=0)
       ↓
[Data Balancing]
       ↓
[Tokenization & Padding]
       ↓
[LSTM Model Training]
       ↓
[Evaluation & Visualization]
       ↓
Trained Classifier
Future Work
Potential Improvements

Enhanced Labeling

Include more TATA box variants
Detect position-specific information
Multi-class classification (different motif types)


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

References
TATA Box Biology

Smale, S. T., & Kadonaga, J. T. (2003). The RNA polymerase II core promoter. Annual Review of Biochemistry.
Basehoar, A. D., et al. (2004). Identification and distinct regulation of yeast TATA box-containing genes. Cell.

Deep Learning for Genomics

Zou, J., et al. (2019). A primer on deep learning in genomics. Nature Genetics.
Eraslan, G., et al. (2019). Deep learning: new computational modelling techniques for genomics. Nature Reviews Genetics.

LSTM Networks

Hochreiter, S., & Schmidhuber, J. (1997). Long short-term memory. Neural Computation.

Bioinformatics Tools

IUPAC Nucleotide Codes: Cornish-Bowden, A. (1985). Nomenclature for incompletely specified bases in nucleic acid sequences.


Dataset : http://kaggle.com/datasets/harshvardhan21/dna-sequence-prediction
