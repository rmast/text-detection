FROM centos:centos7

MAINTAINER "Robert Mast" rn.mast@zonnet.nl

WORKDIR /tmp/

#Install JAVA
RUN yum groupinstall -y 'Development Tools'

#Environment setup related to Python
ENV CONDA_HOME /root/miniconda3
ENV PATH $CONDA_HOME/bin:$PATH
ENV CONDA_ENVIRONMENT conda-environment


WORKDIR /root/

RUN git clone https://github.com/azmiozgen/text-detection.git
# Install python+conda and H2O
RUN echo "Installing Miniconda..." \
    && curl -L -O 'https://repo.anaconda.com/miniconda/Miniconda3-py37_23.1.0-1-Linux-x86_64.sh'  \
    && bash Miniconda3-py37_23.1.0-1-Linux-x86_64.sh -b \
    && echo "Done." \
    && echo "Creating environment..." \
    && cd text-detection \
    && mv requirements.txt text-detection.yml \
    && conda env create -f text-detection.yml \
    && echo "Done." \
    && source activate text-detection \
    && conda clean -y -a \
    && yum clean all
