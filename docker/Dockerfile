FROM bwawrik/qiime

MAINTAINER Dave Beck <dacb@uw.edu>

# download fastqc to /usr/local, unpack it and add the path to the global environment
RUN mkdir -p /usr/local \
	&& cd /usr/local \
	&& wget http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.3.zip \
	&& unzip fastqc_v0.11.3.zip \
	&& chmod +x /usr/local/FastQC/fastqc

ENV PATH /usr/local/FastQC:$PATH

# note that the qiime image we start from already has R installed
# install R packages
RUN R -e 'install.packages("vegan", repos="http://cran.us.r-project.org")'

# copy fastq-join to correct location
RUN cp /usr/local/qiime_software/ea-utils-1.1.2-537-release/fastq-join /usr/local/bin

# install MAFFT
# note that the touch is a work around for a problem with the ubuntu LTS 14.04 used
# for the qiime image and a depedent package libpam-systemd:amd64
RUN touch /etc/init.d/systemd-logind \
	&& apt-get -y install mafft

# create an example directory for storing examples
RUN mkdir /examples

# copy the R script to load the biom tab file into a more accessible location
RUN cp /usr/local/lib/python2.7/dist-packages/qiime/support_files/R/loaddata.r /examples

# copy a base set of QIIME parameters
COPY parameters.txt /examples
