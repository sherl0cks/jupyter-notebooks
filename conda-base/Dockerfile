# inspired by: 
# https://github.com/openshift-s2i/s2i-wildfly/blob/master/11.0/Dockerfile
# https://github.com/sclorg/s2i-base-container/blob/master/core/Dockerfile

FROM centos/s2i-base-centos7

EXPOSE 8888

ENV ANACONDA_URI=https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh \
    ANACONDA_HOME=/opt/anaconda3
    PATH="$ANACONDA_HOME/bin:$PATH"

USER root

RUN INSTALL_PKGS="bzip2" && \
    yum update -y && \
    yum install $INSTALL_PKGS -y && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y

RUN curl -o installAnacoda.sh $ANACONDA_URI && \
    chmod a+x installAnacoda.sh && \
    ./installAnacoda.sh -b -p $ANACONDA_HOME &&
    rm installAnacoda.sh 

COPY ./s2i/bin/ $STI_SCRIPTS_PATH

USER 1001

CMD $STI_SCRIPTS_PATH/usage