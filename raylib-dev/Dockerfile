# Use a base Ubuntu image
FROM ubuntu:22.04

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    git \
    vim \
    tmux \
    gcc \
    gdb \
    valgrind \
    libglfw3-dev \
    libopenal-dev \
    libasound2-dev \
    libx11-dev \
    libxi-dev \
    libsndfile1-dev \
    libfreetype6-dev \
    libcurl4-openssl-dev \
    libpthread-stubs0-dev \
    libxrandr-dev \
    libxinerama-dev \
    libxxf86vm-dev \
    libgl1-mesa-dev \
    libglu1-mesa-dev \
    xorg-dev \
    && rm -rf /var/lib/apt/lists/*

# Clone Raylib and build it
RUN git clone https://github.com/raysan5/raylib.git /raylib
WORKDIR /raylib
RUN cmake . && make install

RUN git config --global user.name "<your-name>" && \
    git config --global user.email "<your-email>"

COPY .bash_aliases /root/.bash_aliases
COPY .vimrc /root/.vimrc
COPY .bashrc /root/.bashrc
# Set up the working directory for your projects
WORKDIR /projects

# Run bash by default
CMD ["/bin/bash"]

#docker build -t raylib-dev-environment .
#docker run -it --name raylib-dev-container c-dev-environment

