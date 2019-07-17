# docker-bam_readcount_helper-cwl

# instructions
## https://pvactools.readthedocs.io/en/latest/pvacseq/input_file_prep/readcounts.html

Running bam-readcount

bam-readcount uses a bam file and site list regions file as input. The site lists are created from your decomposed VCF, one for snvs and one for indels. Snvs and indels are then run separately through bam-readcount using the same bam. Indel regions must be run in a special insertion-centric mode.

Example bam-readcount command

bam-readcount -f <reference_fasta> -l <site_list> <bam_file> [-i] [-b 20]

The -i option must be used when running the indels site list in order to process indels in insertion-centric mode.

A minimum base quality of 20 is recommended which can be enabled using the -b 20 option.

The mgibio/bam_readcount_helper-cwl Docker container contains a bam_readcount_helper.py script that will create the snv and indel site list files from a VCF and run bam-readcount. Information on that Docker container can be found here: dockerhub mgibio/bam_readcount_helper-cwl.

Example bam_readcount_helper.py command

/usr/bin/python /usr/bin/bam_readcount_helper.py <decomposed_vcf> <sample_name> <reference_fasta> <bam_file> <output_dir>

This will write two bam-readcount files to the <output_dir>: <sample_name>_bam_readcount_snv.tsv and <sample_name>_bam_readcount_indel.tsv, containing readcounts for the snv and indel positions, respectively.
