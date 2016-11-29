FROM nvidia/cuda:7.5-cudnn4-devel-ubuntu14.04
MAINTAINER caffe-maint@googlegroups.com

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        git \
        wget \
        libatlas-base-dev \
        libboost-all-dev \
        libgflags-dev \
        libgoogle-glog-dev \
        libhdf5-serial-dev \
        libleveldb-dev \
        liblmdb-dev \
        libopencv-dev \
        libprotobuf-dev \
        libsnappy-dev \
        protobuf-compiler \
        python-dev \
        python-numpy \
        python-pip \
        python-scipy && \
    rm -rf /var/lib/apt/lists/*
    
WORKDIR /opt

# MATIO
RUN wget http://jaist.dl.sourceforge.net/project/matio/matio/1.5.2/matio-1.5.2.tar.gz && \
    tar -xvzf matio-1.5.2.tar.gz && \
    rm matio-1.5.2.tar.gz
    
WORKDIR /opt/matio-1.5.2

RUN ./configure && make -j8 && make install -j8

ENV CAFFE_ROOT=/opt/caffe
WORKDIR $CAFFE_ROOT

ENV INCLUDE_DIRS=/opt/matio-1.5.2/src/:$INCLUDE_DIRS
ENV LIBRARY_DIRS=/opt/matio-1.5.2/src/:$LIBRARY_DIRS

# FIXME: clone a specific git tag and use ARG instead of ENV once DockerHub supports this.
ENV CLONE_TAG=master

RUN git clone -b ${CLONE_TAG} --depth 1 https://bitbucket.org/aquariusjay/deeplab-public-ver2.git . && \
    for req in $(cat python/requirements.txt) pydot; do pip install $req; done && \
    cp Makefile.config.example Makefile.config && \
    make all -j8 && \
    make pycaffe -j8

ENV PYCAFFE_ROOT $CAFFE_ROOT/python
ENV PYTHONPATH $PYCAFFE_ROOT:$PYTHONPATH
ENV PATH $CAFFE_ROOT/build/tools:$PYCAFFE_ROOT:$PATH
RUN echo "$CAFFE_ROOT/build/lib" >> /etc/ld.so.conf.d/caffe.conf && ldconfig

WORKDIR /workspace
