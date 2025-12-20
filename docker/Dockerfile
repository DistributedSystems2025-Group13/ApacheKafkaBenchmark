FROM --platform=linux/amd64 ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

# Install basic dependencies
RUN apt-get update && apt-get install -y \
    curl wget unzip git vim jq \
    build-essential libz-dev zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

# Install OpenJDK 21
RUN apt-get update && apt-get install -y openjdk-21-jdk

# Install Oracle GraalVM 21
RUN mkdir -p /opt/graalvm && \
    curl -L https://download.oracle.com/graalvm/21/latest/graalvm-jdk-21_linux-x64_bin.tar.gz | \
    tar -xzC /opt/graalvm --strip-components=1

# Install Maven
RUN apt-get update && apt-get install -y maven

# Setup default Java version
ENV JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64
ENV PATH="$JAVA_HOME/bin:/opt/graalvm/bin:$PATH"

WORKDIR /work

CMD ["/bin/bash"]
