FROM rhololkeolke/cpp-dev:latest
LABEL name="dart-model-explorer"
LABEL version="master"
LABEL maintainer="dschwab@andrew.cmu.edu"

COPY conan_config /conan_config
COPY conanfile.txt /conanfile.txt

# conan system requirements uses sudo
RUN apt-get update && \
	apt-get install -y sudo toilet libsdl2-dev libglfw3-dev libopenal-dev && \
        apt-get clean
RUN conan config install conan_config
RUN conan install --build=outdated --build=cascade /conanfile.txt

