FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive
# update apt and collect a few essential tools
# then add the gcc repository before updating apt again.
# now we can install gcc 10 compiler.
# we also download miniconda.
RUN apt-get update \
	&& apt-get install -y wget curl unzip tar git binutils software-properties-common \
	&& wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh \
	&& add-apt-repository -y ppa:ubuntu-toolchain-r/test \
	&& apt-get update
g
# install miniconda
ENV PATH="/root/miniconda3/bin:$PATH"
ENV DEBIAN_FRONTEND noninteractive
RUN mkdir /root/.conda && bash Miniconda3-latest-Linux-x86_64.sh -b

# install the gcc 10.1 compilers, and documentation libraries
# and set gcc-10.1 to default.
RUN apt-get install -y gcc-10 g++-10 doxygen  \
    && update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-10  100 \
    && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-10  100

# install cmake
ENV PATH="$PATH:/cmake-3.18.1-Linux-x86_64/bin"
RUN wget https://github.com/Kitware/CMake/releases/download/v3.18.1/cmake-3.18.1-Linux-x86_64.tar.gz \
    && tar -xvf cmake-3.18.1-Linux-x86_64.tar.gz

# create conda environment, install some python deps and pyomexmeta
RUN conda init bash \
    && . ~/.bashrc \
    && conda create --name rr python=3.7 \
    && conda activate rr
