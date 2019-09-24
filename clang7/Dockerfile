FROM conanio/clang7
LABEL name="clang7"
LABEL version="master"
LABEL maintainer="dschwab@andrew.cmu.edu"

RUN sudo apt-get update && \
	sudo apt-get install -y llvm-7 && \
        sudo apt-get clean
RUN CPPFLAGS=-fPIC CFLAGS=-fPIC pyenv install -vvv 3.7.4
RUN pyenv global 3.7.4 && pyenv rehash
RUN pip install -U pip conan
