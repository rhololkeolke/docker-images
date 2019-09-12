FROM rhololkeolke/clang8
LABEL name="dart-model-explorer"
LABEL version="master"
LABEL maintainer="dschwab@andrew.cmu.edu"

COPY conan_config conan_config
COPY conanfile.txt conanfile.txt

# conan system requirements uses sudo
RUN sudo apt-get update && \
	sudo apt-get install -y toilet libsdl2-dev libglfw3-dev libopenal-dev ninja-build cowsay && \
	sudo apt-get clean
RUN git clone https://github.com/possatti/pokemonsay && \
	cd pokemonsay && \
	./install.sh && \
	cd .. && \
        rm -rf pokemonsay
RUN conan config install conan_config
RUN conan install --build=outdated conanfile.txt

