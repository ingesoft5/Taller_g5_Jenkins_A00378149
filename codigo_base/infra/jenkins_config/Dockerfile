FROM jenkins/jenkins:lts-jdk17

USER root

# 1. Instalar Maven y curl/ca-certificates
RUN apt-get update && apt-get install -y --no-install-recommends \
    maven \
    curl \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# 2. Descargar e instalar el binario estático oficial del CLI de Docker
RUN curl -fsSL https://download.docker.com/linux/static/stable/x86_64/docker-24.0.7.tgz | tar -xzf - -C /tmp \
    && mv /tmp/docker/docker /usr/local/bin/ \
    && rm -rf /tmp/docker

# 3. Configurar permisos del grupo docker para el usuario jenkins
RUN groupadd -f docker && usermod -aG docker jenkins

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
# RUN jenkins-plugin-cli --plugin-file /usr/share/jenkins/ref/plugins.txt

USER jenkins