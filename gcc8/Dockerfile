FROM conanio/gcc8
LABEL name="gcc8"
LABEL version="master"
LABEL maintainer="dschwab@andrew.cmu.edu"

RUN CPPFLAGS=-fPIC CFLAGS=-fPIC pyenv install -vvv 3.7.4
RUN pyenv global 3.7.4 && pyenv rehash
RUN pip install -U pip conan
