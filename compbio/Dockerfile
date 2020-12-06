FROM continuumio/miniconda3:4.9.2
LABEL maintainer="Haizi Zheng <haizi.zh@gmail.com>"

ARG DEBIAN_FRONTEND=noninteractive

# ENV LANGUAGE=C
# ENV LANG=C
# ENV LC_ALL=C
ENV LANG C.UTF-8

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y --no-install-recommends \
    build-essential \
    apt-utils \
    git \
    curl \
    vim \
    wget \
    ca-certificates

RUN conda install -y mamba -c conda-forge
RUN conda config --add channels conda-forge && conda config --add channels bioconda

RUN mamba install -y r-base
RUN mamba install -y r-essentials r-tidyverse r-here r-optparse r-logging
RUN mamba install -y bioconductor-rsamtools

RUN mamba install -y -c bioconda bwa ucsc-bedclip ucsc-bedsort trimmomatic bedtools \
    fastqc htslib samtools bedops ucsc-bigwigtobedgraph ucsc-wigtobigwig \
    ucsc-bedgraphtobigwig bcftools gatk

RUN apt-get install -y --no-install-recommends htop 
RUN mamba install -y r-doparallel
RUN mamba install r-vcfr r-philentropy bioconductor-hicrep
RUN mamba install -y bioawk multiqc samblaster 

RUN apt-get install -y --no-install-recommends wget bzip2 ca-certificates gnupg2 squashfs-tools git
RUN /bin/bash -c "wget -O- http://neuro.debian.net/lists/buster.us-ca.full | tee /etc/apt/sources.list.d/neurodebian.sources.list && \
    apt-key adv --recv-keys --keyserver hkp://pool.sks-keyservers.net:80 0xA5D32F012649A5A9 && \
    apt-get -y update && apt-get install -y --no-install-recommends singularity-container"

RUN conda clean --all -y 