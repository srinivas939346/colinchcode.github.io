---
layout: post
title: "[python] Nucleotide and amino acid composition analysis using Python"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In bioinformatics, analyzing the composition of nucleotides and amino acids is a common task. Python provides a versatile and powerful set of tools that can be used for this purpose. In this blog post, we will explore how to perform nucleotide and amino acid composition analysis using Python.

## Table of Contents
1. [Introduction](#introduction)
2. [Nucleotide Composition Analysis](#nucleotide-composition-analysis)
3. [Amino Acid Composition Analysis](#amino-acid-composition-analysis)
4. [Conclusion](#conclusion)

---

## Introduction

Analyzing the composition of nucleotides and amino acids is important in many biological studies. It helps us understand the underlying structure and function of DNA, RNA, and proteins. Python provides several libraries and packages that simplify this analysis.

## Nucleotide Composition Analysis

To analyze the nucleotide composition of a DNA or RNA sequence, we can use the `Bio.Seq` module from the `biopython` library. First, we need to install `biopython` by running `pip install biopython` in your command line.

Here is an example code snippet that calculates the nucleotide composition of a given sequence:

```python
from Bio.Seq import Seq

sequence = "ATCGATCGATCG"
seq_obj = Seq(sequence)

composition = {
    "A": seq_obj.count("A"),
    "T": seq_obj.count("T"),
    "C": seq_obj.count("C"),
    "G": seq_obj.count("G")
}

total_count = sum(composition.values())

for base, count in composition.items():
    frequency = count / total_count * 100
    print(f"{base}: {frequency}%")
```

In the above code, we create a `Seq` object from the input sequence and then count the occurrences of each nucleotide in the sequence. The composition is stored in a dictionary, and we calculate the frequencies as percentages and print them.

## Amino Acid Composition Analysis

To analyze the amino acid composition of a protein sequence, we can use the `Bio.SeqUtils` module from the `biopython` library. This module provides various functions for protein sequence analysis.

Here is an example code snippet that calculates the amino acid composition of a protein sequence:

```python
from Bio.SeqUtils.ProtParam import ProteinAnalysis

sequence = "MSRSLLLRFLLFLLLLPPLP"
analysed_seq = ProteinAnalysis(sequence)

composition = analysed_seq.get_amino_acids_percent()

for amino_acid, frequency in composition.items():
    print(f"{amino_acid}: {frequency}%")
```

In the above code, we create a `ProteinAnalysis` object from the input sequence and then use the `get_amino_acids_percent` method to obtain the amino acid composition as a dictionary. We then iterate over the keys and values of the dictionary to print the frequencies.

## Conclusion

Python provides powerful libraries and tools for analyzing the composition of nucleotides and amino acids in biological sequences. With the `biopython` library, we can easily calculate the composition and frequency of nucleotides and amino acids in DNA, RNA, and protein sequences. This makes Python a valuable language for bioinformatics and computational biology studies.

---

References:
- `biopython` library: [https://biopython.org/](https://biopython.org/)
- `biopython` documentation: [https://biopython.readthedocs.io/](https://biopython.readthedocs.io/)