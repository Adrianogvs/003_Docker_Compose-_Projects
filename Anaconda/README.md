# Dockerized Anaconda Environment

Este projeto oferece um ambiente Dockerizado com o Anaconda, permitindo a criação de um contêiner pronto para uso com o Jupyter Notebook.

## Pré-requisitos

- Docker instalado na máquina local. [Download aqui](https://www.docker.com/products/docker-desktop)

## Instruções de Uso

1. **Clone este repositório:**

    ```bash
    git clone https://github.com/seu-usuario/seu-repositorio.git
    ```

2. **Navegue até o diretório do projeto:**

    ```bash
    cd seu-repositorio/Anaconda
    ```

3. **Construa a imagem Docker:**

    ```bash
    docker build -t anaconda-docker .
    ```

4. **Execute o contêiner com o Jupyter Notebook:**

    ```bash
    docker run -it --rm -p 8888:8888 -v ${PWD}:/app anaconda-docker jupyter notebook --ip=0.0.0.0 --no-browser --allow-root
    ```

5. **Abra o navegador e acesse a seguinte URL:**

    ```
    http://localhost:8888/?token=SEU_TOKEN
    ```

    Certifique-se de substituir `SEU_TOKEN` pelo token fornecido no terminal.

6. **Explore e utilize o Jupyter Notebook conforme necessário.**

## Observações

- Os notebooks e arquivos fora do contêiner estão no diretório `./Anaconda` para persistência após a execução do contêiner.

- Ao encerrar o contêiner (`Ctrl+C` no terminal), o contêiner será removido, mas os arquivos fora do contêiner permanecerão.

