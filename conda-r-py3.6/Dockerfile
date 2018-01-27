FROM centos:latest

ENV ANACONDA_URI=https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
ENV PATH="/opt/anaconda3/bin:$PATH"

USER root

RUN yum update -y && yum install bzip2 -y && yum clean all

RUN curl -o installAnacoda.sh $ANACONDA_URI && \
    chmod a+x installAnacoda.sh && \
    ./installAnacoda.sh -b -p /opt/anaconda3


RUN conda update jupyter ipython conda -y && \
    conda install r-irkernel -y

ADD s2i /usr/libexec/s2i

ENV JUPYTER_CONFIG_DIR="/jupyter"

# this needs to be more elegant
RUN mkdir $JUPYTER_CONFIG_DIR && chmod -R a+wrx $JUPYTER_CONFIG_DIR

EXPOSE 8888

USER 1001

WORKDIR $JUPYTER_CONFIG_DIR

ENV HOME=$JUPYTER_CONFIG_DIR

CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0"]

