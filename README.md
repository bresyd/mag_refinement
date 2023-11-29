# mag_refinement

The script mag_refinement.sh is for extending contigs obtained from a metagenome assembly. Its primary purpose lies in improving size and contiguity of contigs representing a metagenome assembled genome (MAG). Once a MAG is obtained (either by manual binning of contigs or by using any available binning software), this script can be used to elongate, and potentially connect, the contigs of the MAG. This is done by mapping of all reads used in the initial metagenome assembly to the contigs of the MAG, and then reassembling the mapped reads. This process is then repeated several times, always using the contigs from the previous iteration (only using those >2kb) as input for the mapping in the current iteration. 

mag_refinement.sh currently also uses two helper scripts, fasta_to_gc_cov_length_tab.pl and tab_to_fasta.pl, to filter the assembled contigs by length. I recommend adding the path to those two helper scripts to your .bashrc file (alternatively you could add the absolute path to the two scripts into mag_refinement.sh).  

The current version of the script was developed to include short-read (Illumina paired end) as well as long-read (Pacbio HIFI reads) metagenome data. The mapped long reads are included in the assembly as single end reads. However, the script could easily be modified to run on short-read data only by removing the lines related to the mapping of the pacbio reads and removing the argument for the single end reads in the assembly.

## Dependencies and requirements
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

mag_refinement.sh has been developed on Linux 4.9.0-17-amd64 x86_64 using Debian 9

## Installation
Just download mag_refinment.sh plus the two helper scritps (fasta_to_gc_cov_length_tab.pl and tab_to_fasta.pl) into your desired directory.

## Usage
**./mag_refinment.sh seed_contigs_path pacbio_path fw_reads_path rv_reads_path project_name no_of_iterations threads**  
with  
**seed_contigs_path**  path to fasta file with seed contigs  
**pacbio_path**  path to pacbio reads  
**fw_reads_path**  path to forward reads  
**rv_reads_path**  path to reverse reads  
**project_name**  prefix for output files  
**no_of_iterations**  number of iterations to run  
**threads**  number of threads to use where appropriate  

## Test dataset
