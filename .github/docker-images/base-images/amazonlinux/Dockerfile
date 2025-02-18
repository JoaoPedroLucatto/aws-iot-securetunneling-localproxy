FROM amazonlinux:latest as base
ARG OPENSSL_CONFIG

# Install Prerequisites

RUN yum check-update; yum upgrade -y && \
	yum install -y git boost-devel autoconf automake \
	wget libtool curl make gcc-c++ unzip cmake3 python-devel openssl11-devel which

# Install Dependencies

RUN ln -s /usr/bin/cmake3 /usr/bin/cmake
RUN mkdir /home/dependencies

WORKDIR /home/dependencies
RUN wget https://www.zlib.net/zlib-1.2.13.tar.gz -O /tmp/zlib-1.2.13.tar.gz && \
	tar xzvf /tmp/zlib-1.2.13.tar.gz && \
	cd zlib-1.2.13 && \
	./configure && \
	make && \
	make install

WORKDIR /home/dependencies
RUN wget https://boostorg.jfrog.io/artifactory/main/release/1.81.0/source/boost_1_81_0.tar.gz -O /tmp/boost.tar.gz && \
	tar xzvf /tmp/boost.tar.gz && \
	cd boost_1_81_0 && \
	./bootstrap.sh && \
	./b2 install link=static

WORKDIR /home/dependencies
RUN wget https://github.com/protocolbuffers/protobuf/releases/download/v3.17.3/protobuf-all-3.17.3.tar.gz -O /tmp/protobuf-all-3.17.3.tar.gz && \
	tar xzvf /tmp/protobuf-all-3.17.3.tar.gz && \
	cd protobuf-3.17.3 && \
	mkdir build && \
	cd build && \
	cmake ../cmake && \
	make && \
	make install

WORKDIR /home/dependencies
RUN git clone https://github.com/openssl/openssl.git && \
	cd openssl && \
	git checkout OpenSSL_1_1_1-stable && \
	./config && \
	make depend && \
	make all

WORKDIR /home/dependencies
RUN git clone --branch v2.13.6 https://github.com/catchorg/Catch2.git && \
	cd Catch2 && \
	mkdir build && \
	cd build && \
	cmake ../ && \
	make && \
	make install
