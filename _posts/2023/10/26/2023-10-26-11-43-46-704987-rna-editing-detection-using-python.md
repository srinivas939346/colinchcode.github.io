---
layout: post
title: "[python] RNA editing detection using Python"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

**Introduction**

RNA editing is a biological process that involves the alteration of RNA sequences after transcription. It plays an important role in expanding the functional diversity of RNA molecules. Detecting RNA editing events is crucial for understanding the regulation and function of genes.

In this blog post, we will explore how to detect RNA editing events using Python. We will utilize a Python library called `Pysam` for working with Sequence Alignment/Map (SAM) files, which are commonly used to store aligned sequencing reads.

## Prerequisites

To follow along with this tutorial, you will need:

- Python 3 installed on your machine
- Pysam library installed (can be installed using `pip install pysam` command)

## Loading SAM file

First, we need to load the SAM file containing aligned sequencing reads. SAM files are tab-delimited text files that store information about the alignment of each read against a reference genome.

We can use the `pysam.AlignmentFile` class to open the SAM file. Let's see how to do it:

```python
import pysam

# Open SAM file
samfile = pysam.AlignmentFile("path/to/samfile.sam", "r")
```

Make sure to replace `"path/to/samfile.sam"` with the actual path to your SAM file.

## Filtering edits

Next, we need to filter the aligned reads to identify potential RNA editing events. One common approach is to look for discrepancies between the reference genome and the aligned reads at specific positions.

Let's assume we are interested in detecting RNA editing events where a C (cytosine) is converted to U (uracil) in the RNA molecule. We can use the following code to filter out reads with C-to-U edits:

```python
filtered_reads = []

for read in samfile.fetch():
    # Check each position in the read
    for i, base in enumerate(read.seq):
        # If the base is 'C' and the read alignment doesn't have 'U' at the same position
        if base == 'C' and read.query_sequence[i] != 'U':
            filtered_reads.append(read)
            break
```

This code iterates over each aligned read and checks each base in the read sequence. If a C base is found and the corresponding position in the aligned read does not have a U base, we consider it a potential RNA editing event and add that read to the `filtered_reads` list.

## Analyzing edits

Finally, we can analyze the filtered reads to obtain information about the location and frequency of RNA editing events. We can count the number of times a C-to-U edit occurs at each position in the reads.

Here's an example code snippet that performs this analysis and prints the positions and edit frequencies:

```python
edit_counts = {}

for read in filtered_reads:
    for i, base in enumerate(read.seq):
        if base == 'C' and read.query_sequence[i] != 'U':
            position = read.pos + i + 1
            if position in edit_counts:
                edit_counts[position] += 1
            else:
                edit_counts[position] = 1

# Print edit positions and frequencies
for position, count in edit_counts.items():
    print(f"Edit at position {position}: {count} occurrences")
```

In this code, we iterate over the filtered reads and count the occurrences of C-to-U edits at each position. The position is calculated using the `read.pos` attribute and the current index `i`. The edit counts are stored in a dictionary where the position is the key and the edit frequency is the value. Finally, we print the edit positions and frequencies.

## Conclusion

In this blog post, we have learned how to detect RNA editing events using Python. We used the `Pysam` library to load and analyze SAM files containing aligned sequencing reads. We filtered reads with C-to-U edits and counted the occurrences of these edits at each position.

Detecting RNA editing events is a complex task, and this tutorial provides just a basic example. Further analysis and validation may be required depending on the specific research or application. If you're interested in this topic, make sure to explore additional resources and reference materials.

**References:**
- Pysam documentation: [https://pysam.readthedocs.io](https://pysam.readthedocs.io)
- Li, W., & Godzik, A. (2006). Cd-hit: A fast program for clustering and comparing large sets of protein or nucleotide sequences. Bioinformatics, 22(13), 1658-1659.

Thank you for reading! Hope you found this tutorial useful.