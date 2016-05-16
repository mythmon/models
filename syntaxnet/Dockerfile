FROM ubuntu:xenial-20160503
WORKDIR /app
ENV DEBIAN_FRONTEND=noninteractive
ENV PATH=/root/bin:$PATH

# Install dependencies
RUN apt-get update
RUN apt-get install -y --no-install-recommends \
        openjdk-8-jdk pkg-config zip g++ zlib1g-dev unzip swig wget \
        python python-pip python-wheel python-dev
RUN wget https://github.com/bazelbuild/bazel/releases/download/0.2.2/bazel-0.2.2-installer-linux-x86_64.sh && \
    chmod +x bazel-0.2.2-installer-linux-x86_64.sh && \
    ./bazel-0.2.2-installer-linux-x86_64.sh --user
RUN pip install setuptools
RUN pip install 'protobuf==3.0.0b2' asciitree numpy

# Install Syntaxnet
COPY . /app
RUN cd /app/tensorflow && ./configure
RUN bazel test syntaxnet/... util/utf8/...
