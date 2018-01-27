FROM centos:latest

ENV ANACONDA_URI=https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
ENV PATH="/opt/anaconda3/bin:$PATH"
ENV JUPYTER_CONFIG_DIR="/jupyter"

USER root

RUN yum update -y && yum install bzip2 -y && yum clean all

RUN curl -o installAnacoda.sh $ANACONDA_URI && \
    chmod a+x installAnacoda.sh && \
    ./installAnacoda.sh -b -p /opt/anaconda3


RUN conda update jupyter ipython conda -y && \
    conda install r-irkernel -y

ADD s2i /usr/libexec/s2i

EXPOSE 8888

USER 1001

RUN mkdir $JUPYTER_CONFIG_DIR
WORKDIR $JUPYTER_CONFIG_DIR

CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0"]

