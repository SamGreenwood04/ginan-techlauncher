FROM ubuntu:24.04

ARG DEBIAN_FRONTEND=noninteractive

# Install minimal dependencies for development
RUN apt-get update -y \
    && apt-get upgrade -y --no-install-recommends \
    && apt-get install -y --no-install-recommends \
    ca-certificates \
    git \
    gcc \
    g++ \
    ccache \
    curl \
    wget \
    cmake \
    make \
    gzip \
    vim \
    nano \
    zip \
    unzip \
    tar \
    pkg-config \
    ninja-build \
    sudo \
    gfortran \
    gnupg \
    openssh-client \
    mingw-w64 \
    g++-mingw-w64 \
    gcc-mingw-w64 \
    binutils-mingw-w64 \
    python3 \
    python3-venv \
    autoconf \
    automake \
    libtool \
    nasm \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

# Give ubuntu user sudo access
RUN echo "ubuntu ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/ubuntu \
    && chmod 0440 /etc/sudoers.d/ubuntu

# Set up vcpkg directory with proper permissions
RUN mkdir -p /opt/vcpkg \
    && chown -R ubuntu:ubuntu /opt/vcpkg

USER ubuntu
WORKDIR /workspace

# Install vcpkg
RUN git clone https://github.com/microsoft/vcpkg.git /opt/vcpkg \
    && /opt/vcpkg/bootstrap-vcpkg.sh -disableMetrics

# Set environment variables for vcpkg
ENV VCPKG_ROOT=/opt/vcpkg
ENV PATH="${VCPKG_ROOT}:${PATH}"

# Set default shell to bash
SHELL ["/bin/bash", "-c"]

CMD ["/bin/bash"]
