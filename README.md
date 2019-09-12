### Sequence Sampler

This python program takes a reference FASTA file (with one or multiple features) as an input, and probabilistically samples sequences from the features within this input file, writing them to an output FASTA. A window for the lengths and GC content of these sequences can be provided by the user, in addition to the minimum and maximum number of sequences to be sampled per feature (plus the probability that sequences won't be sampled from a feature).

In addition to the output FASTA file, the sampler also generates a 'counts' file which provides a count of the total sampled sequences per feature in the input FASTA; as well as an 'info' file with sequence lengths and GC contents of all sampled sequences.  

Prior to using the script, ensure that the input FASTA file has no newlines within the features. Use the following command in bash to generate a new input file if there are any :\
`awk '/^>/ {printf("\n%s\n",$0);next; } { printf("%s",$0);}  END {printf("\n");}' < file.fa > out.fa `

Usage example:\
`python sequenceSampler.py --inFile input.fasta --outFile output.fasta --outPath output_directory --minlen 30 --maxlen 50 --num 10000 --minseq 0 --maxseq 10 --minGC 25 --maxGC 45 --nonGC 20 --noSampling 30` 

The inputs are as follows:

```
Required inputs:
--inFile	input FASTA file
--outPath	output path
--minlen	minimum length of sampled sequence
--maxlen	maximum length of sampled sequence


Optional inputs:
--outFile	output FASTA file name
--num 		maximum number of total sampled sequences
--minseq	minimum number of sampled sequences per feature
--maxseq	maximum number of sampled sequences per feature
--minGC		minimum GC content of sampled sequence
--maxGC		maximum GC content of sampled sequence
--nonGC		percent probability to accept sequence if outside GC range
--noSampling	percent probability that a feature has no sampled sequences represented in output
```

### To Do:
* Sample sequences from within length and GC window so that these follow a gaussian distribution
* Debug and add 5' and 3' biasing as user-defined options


