# _S.Pombe_ NGS mutation analysis pipeline
# Purpose of this Python task
we analysed next-generation sequencing (NGS) reads, in this Python bioinformatics pipeline, against a reference genome in order to display mismatches in nucleotides and explore how exposure to genotoxic agents changes mutation rates, positions and spectra in _Schizosaccharomyces pombe_
# How to run the program
use the repository to open the google colab notebook directly, ensuring that 'reference.txt' and 'reads.csv' are uploaded to your working directory. Next, select 'Run all' to execute the setup, validation and analysis pipeline one after another 
# Inputs and Outputs
Inputs - 200 nt reference sequence ('reference.txt') and a CSV file ('reads.csv') including 6000 aligned sequencing reads across 6 samples (3 control and 3 treated)

Outputs - normalised and validated read records; 1-based mismatch coordinates; sample-level group summary tables; exploratory Welch's t-test comparisons 
# Code design
program depends on a five-function, modular, structure to make sure there is clean seperation of concerns and data safety:

Efficient validation - 'validate_read' uses '.upper()' normalisation and set inclusion '(set(seq).issubset({"A", "C", "G", "T"}))' in order to evaluate seq structure, correctly isolating edge cases such as 'empty-string' to length errors 

Robust coordinates - 'find_mutations' pairs reference and read bases using 'enumerate(..., start=1)' and 'zip' to eliminate index risks (off-by-one) when assigning 1-based positions

Immutability - 'analyse_reads' creates new dictionaries for each respective record instead of modifying input data in-place, to help keep original structures in tact for later comparisons. Helper functions condense multi-criteria sorting to handle positional ties effectively and clearly 
# Testing
code was tested across 3 categories:

Normal inputs - standard sequences with already known single or more substitutions against expected outputs 

Edge cases - Tests exact matches, terminal mutations at boundaries of index, uppercase/lowercase normalisation, empty lists, and tie-breaking 

Invalid inputs - Test for sequence length invalid reads, unexpected characters, verifiying of correct error-code ordering and handling of failures without crashing of the system 
