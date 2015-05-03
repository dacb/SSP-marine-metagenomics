FROM bwawrik/qiime

MAINTAINER Dave Beck <dacb@uw.edu>

# download fastqc to /usr/local, unpack it and add the path to the global environment
RUN mkdir -p /usr/local \
	&& cd /usr/local \
	&& wget http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.3.zip \
	&& unzip fastqc_v0.11.3.zip \
	&& chmod +x /usr/local/FastQC/fastqc

ENV PATH /usr/local/FastQC:$PATH

# install R and required packages
RUN apt-get install R
RUN R -e 'install.packages("vegan", repos="http://cran.us.r-project.org")'
