# Use a imagem oficial do Ubuntu como base
FROM ubuntu:latest

# Instale as dependências necessárias para o Anaconda
RUN apt-get update && \
    apt-get install -y wget bzip2

# Baixe e instale o Anaconda
RUN wget https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh -O /tmp/anaconda.sh && \
    bash /tmp/anaconda.sh -b -p /opt/conda && \
    rm /tmp/anaconda.sh

# Adicione o Anaconda ao PATH
ENV PATH="/opt/conda/bin:${PATH}"

# Defina o diretório de trabalho padrão
WORKDIR /app

# Exponha a porta, se necessário
# EXPOSE 8888

# Comando padrão a ser executado quando o contêiner for iniciado
CMD ["/bin/bash"]
