# Canu

Canu is a fork of the [Celera Assembler](http://wgs-assembler.sourceforge.net/wiki/index.php?title=Main_Page), designed for high-noise single-molecule sequencing (such as the [PacBio](http://www.pacb.com) [RS II](http://www.pacb.com/products-and-services/pacbio-systems/rsii/)/[Sequel](http://www.pacb.com/products-and-services/pacbio-systems/sequel/) or [Oxford Nanopore](https://www.nanoporetech.com/) [MinION](https://nanoporetech.com/products)).

Canu is a hierarchical assembly pipeline which runs in four steps:

* Detect overlaps in high-noise sequences using [MHAP](https://github.com/marbl/MHAP)
* Generate corrected sequence consensus
* Trim corrected sequences
* Assemble trimmed corrected sequences

## Install:

The easiest way to get started is to download a [release](http://github.com/marbl/canu/releases). 

Alternatively, you can also build the latest unreleased from github:

    git clone https://github.com/marbl/canu.git
    cd canu/src
    make -j <number of threads>

The unreleased tip has not undergone the same testing as a release and so may have unknown bugs or issues generating sub-optimal assemblies. We recommend the release version for most users.

## Learn:

The [quick start](http://canu.readthedocs.io/en/latest/quick-start.html) will get you assembling quickly, while the [tutorial](http://canu.readthedocs.io/en/latest/tutorial.html) explains things in more detail.

## Run:

Brief command line help:

    ../<architecture>/bin/canu

Full list of parameters:

    ../<architecture>/bin/canu -options

## Citation:
 - Koren S, Walenz BP, Berlin K, Miller JR, Phillippy AM. [Canu: scalable and accurate long-read assembly via adaptive k-mer weighting and repeat separation](https://doi.org/10.1101/gr.215087.116). Genome Research. (2017).
 
 
 
 
 
 
 
 
#############################################################

for compiling on raijin: module load gcc/4.9.0 


set -euo pipefail # safe mode

set -x # logging

GRID_OPTIONS="-P {project} -q normal -l jobfs=400GB -l software=canu -l wd -N CANU_GRID -m abe -M {My.Email@home.com}"

module load gnuplot

/location/of/canu/Linux-amd64/bin/canu \
-p assembly_name \
-d /short/${PROJECT}/${USER}/canu_assembly \
-nanopore-raw /location/of/reads.fastq \
genomeSize=XXXm \
maxThreads=512 \
maxMemory=63 \
gridOptions="$GRID_OPTIONS" \
useGrid=remote \
gridEngineThreadsOption="-l ncpus=THREADS" \
executiveMemory=2 \
executiveThreads=1 \
java=/apps/java/jdk-10.0.1/bin/java \
gnuplot=/apps/gnuplot/5.2.4/bin/gnuplot

