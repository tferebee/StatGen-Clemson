
## Class on Tuesday/ Thursday 10.02.18
Make a directory called statgen
Make a directory called maize_v40_reference
Download Maize reference sequence, Index it with bowtie2 (will take a while)
Make a raw data directory 
Copy 10 maize individuals (sequences) to the folder
Launch the process_array.script to run QC and trimming on the 10 samples


## make a directory called statgen
```
mkdir statgen
cd statgen
pwd
```	
## make a directory called maize_v40_reference

	mkdir maize_v40_reference
	cd maize_v40_reference
	
## Download and index the reference sequence

wget ftp://ftp.ensemblgenomes.org/pub/release-40/plants/fasta/zea_mays/dna/Zea_mays.AGPv4.dna.toplevel.fa.gz
wget ftp://ftp.ensemblgenomes.org/pub/release-40/plants/gtf/zea_mays/Zea_mays.AGPv4.40.gtf.gz

## unzip the files

gunzip *

## Index the reference assembly for alignment with Bowtie2

module add bowtie2/2.3.1
bowtie2-build Zea_mays.AGPv4.dna.toplevel.fa maize_ref

## you should see the below if it worked properly
[saski@node1873 maize_v40_reference]$ ls
maize_ref.1.bt2  maize_ref.3.bt2  maize_ref.rev.1.bt2  Zea_mays.AGPv4.40.gtf
maize_ref.2.bt2  maize_ref.4.bt2  maize_ref.rev.2.bt2  Zea_mays.AGPv4.dna.toplevel.fa

## make a raw data directory and copy 10 maize individuals (sequences) to the folder
## move up a level in your directory
cd ..  
pwd
## -- you should be in statgen: /home/saski/statgen

mkdir raw_data
cd raw_data

## copy files to your directory DO NOT CHANGE NAME
cp /scratch3/saski/statgen/raw_data/statgen_*.gz .

## list the files -- you should see the below
[saski@login001 raw_data]$ ls
statgen_10.fastq.gz  statgen_2.fastq.gz  statgen_4.fastq.gz  statgen_6.fastq.gz  statgen_8.fastq.gz
statgen_1.fastq.gz   statgen_3.fastq.gz  statgen_5.fastq.gz  statgen_7.fastq.gz  statgen_9.fastq.gz

## navigate up 1 level
cd ..
pwd
#  you should be in /home/saski/statgen

## make a directory for class scripts
mkdir scripts
cd scripts

## copy master pbs script and bash script for submitting
cp /scratch3/saski/statgen/scripts/process_array.script .
cp /scratch3/saski/statgen/scripts/create_submit.bash .

## open the create_submit.bash script and modify the 6th line
vi create_submit.bash
## from inputpwd=/home/saski/statgen/raw_data
i
## just change the username to your username
ESC :wq

## open the process_array.script script and modify the 24th line
vi process_array.script

#from export SOURCEPATH=/home/saski/statgen

#just change the username
ESC :wq

## Launch the process_array.script to run QC and trimming on   the 10 samples
	#open a new terminal window and login to the user node
	cd /home/saski/statgen/scripts  # use your user name here
	
	./create_submit.bash
	
	# there should be 10 .pbs scripts created and automatically submitted to the cluster
	
	#To see what is running in your queue
	qstat -u username



