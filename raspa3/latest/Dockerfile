
FROM ubuntu:26.04

ENV DEBIAN_FRONTEND=noninteractive
ENV RASPA_DIR=/usr/local/share/raspa3

# Base tools and Kitware CMake repository
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates wget gpg git && \
    wget -qO- https://apt.kitware.com/keys/kitware-archive-latest.asc \
        | gpg --dearmor -o /usr/share/keyrings/kitware-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/kitware-archive-keyring.gpg] https://apt.kitware.com/ubuntu/ resolute main" \
        > /etc/apt/sources.list.d/kitware.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        cmake ninja-build \
        llvm lld clang clang-tidy \
        libc++-dev libc++abi-dev \
        libc++-21-dev libc++abi-21-dev \
        libunwind-22-dev \
        libomp-dev libclang-rt-dev \
        python3 python3-dev pybind11-dev \
        liblapack64-dev libblas64-dev \
        libfftw3-dev \
        ocl-icd-opencl-dev opencl-headers \
        zlib1g-dev && \
    rm -rf /var/lib/apt/lists/*

# Fetch RASPA3 source
WORKDIR /opt

RUN git clone https://github.com/iRASPA/RASPA3.git raspa3

WORKDIR /opt/raspa3

# Configure using the Ubuntu 26 AVX2 preset
RUN cmake -B build \
        --preset=linux-x86_64-core-avx2-ubuntu-26 \
        -DCMAKE_CXX_STDLIB_MODULES_JSON=/usr/lib/llvm-21/lib/libc++.modules.json \
        -DBUILD_APP=ON \
        -DBUILD_PYTHON=OFF \
        -DBUILD_TESTING=OFF \
        -DBUILD_BENCHMARKS=OFF && \
    cmake --build build --parallel 4 && \
    cmake --install build

WORKDIR /workspace

ENTRYPOINT ["raspa3"]
