FROM ubuntu:24.04

ARG repository="openfhe-development"
ARG branch=main
ARG tag=v1.3.0
ARG no_threads=1

ENV DEBIAN_FRONTEND=noninteractive

#install pre-requisites for OpenFHE
RUN apt update && apt install -y git \
                                 build-essential \
                                 gcc \
                                 g++ \
                                 cmake \
                                 libomp-dev

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

#git clone the openfhe-development repository and its submodules (this always clones the most latest commit)
RUN git clone https://github.com/openfheorg/$repository.git && cd $repository && git checkout $branch && git checkout $tag && git submodule sync --recursive && git submodule update --init  --recursive

#installing OpenFHE and running tests
RUN mkdir /$repository/build && cd /$repository/build && cmake .. && make -j $no_threads && make install && make testall
