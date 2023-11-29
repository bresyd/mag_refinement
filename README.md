# mag_refinement

The script mag_refinement.sh is for extending contigs obtained from a metagenome assembly. Its primary purpose lies in improving size and contiguity of contigs representing a metagenome assembled genome (MAG). Once a MAG is obtained (either by manual binning of contigs or by using any available binning software), this script can be used to elongate, and potentially connect, the contigs of the MAG. This is done by mapping of all reads used in the initial metagenome assembly to the contigs of the MAG, and then reassembling the mapped reads. This process is then repeated several times, always using the contigs from the previous iteration (only using those >2kb) as input for the mapping in the current iteration. 

mag_refinement.sh currently also uses two helper scripts, fasta_to_gc_cov_length_tab.pl and tab_to_fasta.pl, to filter the assembled contigs by length. I recommend adding the path to those two helper scripts to your .bashrc file  

The current version of the script was developed to include short-read (Illumina paired end) as well as long-read (Pacbio HIFI reads) metagenome data. The mapped long reads are included in the assembly as single end reads. However, the script could easily be modified to run on short-read data only by removing the lines related to the mapping of the pacbio reads and removing the argument for the single end reads in the assembly.

## Dependencies
mag_refinement.sh uses the following publically available software (with the respective version I am currently using the script with in brackets):
[minimap2](https://github.com/lh3/minimap2) (v2.22-r1101),
[samtools](https://github.com/samtools/samtools) (v1.14),
[coverM](https://github.com/wwood/CoverM) (v0.6.1),
[SeqKit](https://github.com/shenwei356/seqkit) (v2.3.0),
[SPAdes](https://github.com/ablab/spades) (v3.15.3).

For mag_refinement.sh to successfully find all the dependencies, [minimap2](https://github.com/lh3/minimap2),
[samtools](https://github.com/samtools/samtools),
[coverM](https://github.com/wwood/CoverM) and
[SeqKit](https://github.com/shenwei356/seqkit) need to be installed in a conda environment called "read_mapping", while [SPAdes](https://github.com/ablab/spades) needs to be installed in a conda environment called "assembly".




