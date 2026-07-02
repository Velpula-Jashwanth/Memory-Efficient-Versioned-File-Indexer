# CS253 Assignment 1

## Memory-Efficient Versioned File Indexer

**Name:** Jashwanth\
**Roll Number:** 241157

------------------------------------------------------------------------

# Overview

This project implements a **memory-efficient versioned file indexer in
C++**.\
The program processes large text files using a **fixed-size buffer** and
builds a **word-level index** that maps each unique word to its
frequency.

The system supports multiple file versions and allows analytical queries
such as:

-   Word frequency queries
-   Top-K frequent words
-   Difference in frequency between two versions

The implementation ensures that **memory usage remains independent of
file size** by reading the file incrementally using a fixed-size buffer.

------------------------------------------------------------------------

# Features

-   Incremental file processing using a fixed-size buffer
-   Case-insensitive word indexing
-   Support for multiple file versions
-   Efficient word frequency storage using hash maps
-   Command-line based query interface
-   Object-oriented C++ design

------------------------------------------------------------------------

# Program Structure

## 1. BufferedReader

Responsible for reading large files incrementally using a fixed-size
buffer.

Responsibilities: - Open input files - Read file chunks using a buffer -
Maintain constant memory usage

------------------------------------------------------------------------

## 2. Tokenizer

Extracts words from the text data read from the buffer.

Responsibilities: - Identify alphanumeric tokens - Convert tokens to
lowercase - Handle tokens split across buffer boundaries

------------------------------------------------------------------------

## 3. VersionedIndex

Stores word frequency maps for different versions of files.

Responsibilities: - Build word indexes - Maintain versioned data -
Provide frequency lookup for queries

------------------------------------------------------------------------

## 4. Query Classes

An abstract base class **Query** is used for query execution.

Derived classes:

-   **WordQuery** -- returns the frequency of a word
-   **TopQuery** -- returns top-K frequent words
-   **DiffQuery** -- computes frequency difference between two versions

This design demonstrates **inheritance and runtime polymorphism**.

------------------------------------------------------------------------

# C++ Concepts Used

The implementation demonstrates several important C++ features:

-   Object-Oriented Programming
-   Inheritance
-   Runtime Polymorphism
-   Templates
-   Exception Handling
-   Standard Template Library (STL)

------------------------------------------------------------------------

# Compilation

Compile using:

    g++ analyzer.cpp -O2 -o analyzer

On Windows:

    g++ analyzer.cpp -O2 -o analyzer.exe

------------------------------------------------------------------------

# Running the Program

## Word Count Query

    .\analyzer.exe --file dataset.txt --version v1 --buffer 512 --query word --word error

Returns the frequency of the word **error** in version **v1**.

------------------------------------------------------------------------

## Top-K Query

    .\analyzer.exe --file dataset.txt --version v1 --buffer 512 --query top --top 10

Displays the **10 most frequent words**.

------------------------------------------------------------------------

## Difference Query

    .\analyzer.exe --file1 dataset_v1.txt --version1 v1 \
    --file2 dataset_v2.txt --version2 v2 \
    --buffer 512 --query diff --word error

Returns the difference in frequency of the word **error** between two
versions.

------------------------------------------------------------------------

# Buffer Size Constraints

    256 KB ≤ buffer ≤ 1024 KB

Example:

    --buffer 512

------------------------------------------------------------------------

# Assumptions

-   Words are sequences of **alphanumeric characters**
-   Word matching is **case-insensitive**
-   Memory usage grows only with the **number of unique words**
-   Files may be arbitrarily large because they are processed
    incrementally

------------------------------------------------------------------------

# Example Output

    Word count = 42
    Buffer Size: 512 KB
    Execution Time: 0.004 seconds

------------------------------------------------------------------------

# Notes

-   Dataset files must exist in the same directory as the executable or
    be provided using an absolute path.
-   The program processes files incrementally and does not load the
    entire file into memory.
