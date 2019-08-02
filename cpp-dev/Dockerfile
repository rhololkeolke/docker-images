FROM ubuntu:18.04
LABEL name="cpp-dev"
LABEL version="master"
LABEL maintainer="digidevin@gmail.com"

ARG NPROC=$(nproc)

RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get install -qy build-essential \
	ca-certificates \
	curl \
	figlet \
	git \
	libbz2-dev \
	libncurses5-dev \
	libncursesw5-dev \
	libreadline-dev \
	libsqlite3-dev \
	libssl-dev \
	make \
	mercurial \
	python3-software-properties \
	software-properties-common \
	swig \
	tk-dev \
	wget \
	xz-utils \
	zip \
	zlib1g-dev && \
	apt-get clean

RUN add-apt-repository -y ppa:ubuntu-toolchain-r/test && \
	apt-get update && \
	apt-get install -y gcc-8 g++-8 && \
	apt-get clean

# setup clang key
RUN wget -O clang.gpg http://apt.llvm.org/llvm-snapshot.gpg.key && \
	apt-key add clang.gpg && \
	rm clang.gpg

COPY clang.list /etc/apt/sources.list.d/clang.list

RUN apt-get update && \
	apt-get install -y clang*-8* \
	llvm*-8* && \
	apt-get clean

ENV CC='/usr/bin/clang-8' CXX='/usr/bin/clang++-8'

# install cmake
RUN wget https://cmake.org/files/v3.15/cmake-3.15.1.tar.gz -O cmake.tar.gz && \
	tar -xzvf cmake.tar.gz && \
	rm cmake.tar.gz && \
	mv cmake-3.15.1 cmake && \
	cd cmake && \
	./bootstrap && \
	make -j${NPROC} && \
	make install && \
	cd .. && \
	rm -rf cmake

# install ninja
RUN git clone git://github.com/ninja-build/ninja.git && \
	cd ninja && \
	git checkout v1.9.0 && \
	./configure.py --bootstrap && \
	mkdir -p /usr/local/bin/ && \
	mv ninja /usr/local/bin/ninja && \
	cd .. && \
	rm -rf ninja

# install pyenv
RUN curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash

# setup bashrc
RUN echo 'PATH=~/.pyenv/bin:$PATH' >> ~/.bashrc && \
	echo 'eval "$(pyenv init -)"' >> ~/.bashrc && \
	echo eval $(pyenv virtualenv-init -) >> ~/.bashrc

ENV PYENV_ROOT /root/.pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH

RUN pyenv install 3.7.4
RUN pyenv rehash
ENV PYENV_VERSION=3.7.4
RUN pip install -U pip conan pre-commit

CMD ["/bin/bash"]
