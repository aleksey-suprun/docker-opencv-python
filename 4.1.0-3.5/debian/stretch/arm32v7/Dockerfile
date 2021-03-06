FROM balenalib/raspberrypi3-python:3.5-stretch-build

ENV NPROC 4
ENV OPENCV_VERSION 4.1.0
ENV OPENCV_SRC_DOWNLOAD_URL https://github.com/opencv/opencv/archive/${OPENCV_VERSION}.tar.gz

RUN [ "cross-build-start" ]

RUN pip3 install numpy

RUN apt-get update -y \
    && apt-get install --no-install-recommends -y \
        cmake \
        g++

RUN mkdir /opencv \
    && cd /opencv \
    && curl -sSL ${OPENCV_SRC_DOWNLOAD_URL} | tar --strip-components=1 -xzf - \
    && mkdir build && cd build \
    && cmake \
        -D CMAKE_BUILD_TYPE=Release \
        -D CMAKE_INSTALL_PREFIX=/usr/local \
        -D BUILD_SHARED_LIBS=OFF \
        -D BUILD_EXAMPLES=OFF \
        -D BUILD_TESTS=OFF \
        -D BUILD_PERF_TESTS=OFF \
        .. \
    && make -j${NPROC} \
    && make install \
    && cd / \
    && rm -rf /opencv

RUN [ "cross-build-end" ]
