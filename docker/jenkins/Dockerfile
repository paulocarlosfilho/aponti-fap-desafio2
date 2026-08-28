FROM jenkins/jenkins:lts

USER root

# Instala pré-requisitos essenciais de sistema[cite: 3, 5]
RUN apt-get update && apt-get install -y lsb-release curl libatomic1

# Adiciona a chave GPG oficial do Docker[cite: 3]
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc https://download.docker.com/linux/debian/gpg

# Configura o repositório estável do Docker[cite: 3]
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.asc] https://download.docker.com/linux/debian $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list

# Instala exclusivamente a CLI do Docker[cite: 3, 5]
RUN apt-get update && apt-get install -y docker-ce-cli

# Retorna para o usuário não-privilegiado padrão por segurança[cite: 3, 5]
USER jenkins