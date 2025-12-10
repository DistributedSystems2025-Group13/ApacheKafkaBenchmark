FROM --platform=linux/amd64 ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

# Install basic dependencies
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    unzip \
    git \
    software-properties-common \
    python3 \
    python3-pip \
    vim \
    jq \
    && rm -rf /var/lib/apt/lists/*

# Install JDKs
RUN apt-get update && apt-get install -y \
    # openjdk-8-jdk \
    # openjdk-21-jdk \
    openjdk-25-jdk

# Install Maven
RUN apt-get update && apt-get install -y maven 

# Install AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && unzip awscliv2.zip \
    && ./aws/install \
    && rm -rf awscliv2.zip aws

# Install Terraform
RUN apt-get update && apt-get install -y gnupg
RUN wget -O- https://apt.releases.hashicorp.com/gpg | \
    gpg --dearmor | \
    tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
RUN echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
    https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
    tee /etc/apt/sources.list.d/hashicorp.list
RUN apt-get update && apt-get install -y terraform

# Install Ansible
RUN apt-add-repository --yes --update ppa:ansible/ansible
RUN apt-get update && apt-get install -y ansible

# Setup JAVA_HOME
ENV JAVA_HOME=/usr/lib/jvm/java-25-openjdk-amd64
ENV PATH="$JAVA_HOME/bin:$PATH"

# # Helper scripts for switching Java
# RUN echo "alias setjava8='export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 && export PATH=\$JAVA_HOME/bin:\$PATH && java -version'" >> /root/.bashrc
# RUN echo "alias setjava21='export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64 && export PATH=\$JAVA_HOME/bin:\$PATH && java -version'" >> /root/.bashrc
# RUN echo "alias setjava25='export JAVA_HOME=/usr/lib/jvm/java-25-openjdk-amd64 && export PATH=\$JAVA_HOME/bin:\$PATH && java -version'" >> /root/.bashrc

# Setup AWS CLI
RUN aws configure set region eu-central-1

RUN ssh-keygen -t rsa -f ~/.ssh/kafka_aws -N ""

WORKDIR /work

CMD ["/bin/bash"]
