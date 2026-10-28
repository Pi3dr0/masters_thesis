
### ==🔵Key Concepts
- **[[k-mer]]**: is a substring of length k taken from DNA or biological sequence.
- Total = k-mers count every overlapping substring
- Distinct = k-mers count each uniq sequence type that appears at least one
- Canonical k-mers: lexicographically smaller sequence between a k-mer and its reverse complement, which help handle double-stranded DNA
- Common Sizes:
	- k=2, k=3 -> dimers or trimers
	- k=31 -> commonly used in genome analysis to balance uniquness and computation limits

### ==🟢Main Application in Bioinformatics
- Genome Assembly
- Alignment-Free Comparsion
- Metagenomics & Classification
- Quality Control
- Popular Counting Tools


```scala
import scala.collection.mutable

// Input: A string Text and an integer k
// Output: All most frequent k-mers in Text

def freqWordsProb(seq: String, k: Int): Map[String,Int] =
	val counts = mutable.Map[String, Int]()
	
	for i <- 0 to seq.length - k do
		val kmer = seq.substring(i, i+k)
		counts(kmer) = counts.getOrElse(kmer, 0) + 1
	
	counts.toMap
```

