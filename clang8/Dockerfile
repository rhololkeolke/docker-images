FROM conanio/clang8
LABEL name="clang8"
LABEL version="master"
LABEL maintainer="dschwab@andrew.cmu.edu"

RUN CPPFLAGS=-fPIC CFLAGS=-fPIC pyenv install -vvv 3.7.4
RUN pyenv global 3.7.4
