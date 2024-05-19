# Use the Jenkins image with JDK 11
FROM jenkins/jenkins:2.414.2-jdk11

# Switch to root user to install necessary packages
USER root

# Update package list and install required packages including sudo
RUN apt-get update && apt-get install -y \
    lsb-release \
    python3-pip \
    sudo

# Add Docker’s official GPG key
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc https://download.docker.com/linux/debian/gpg

# Set up Docker stable repository
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.asc] https://download.docker.com/linux/debian $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list

# Update package list again and install Docker CLI
RUN apt-get update && apt-get install -y docker-ce-cli

# Grant Jenkins user passwordless sudo
RUN echo "jenkins ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Switch back to Jenkins user
USER jenkins

# Install Jenkins plugins
RUN jenkins-plugin-cli --plugins "blueocean:1.25.3 docker-workflow:1.28"
