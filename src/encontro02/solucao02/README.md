Para montar esse projeto foi necessário

Criar um arquivo `main.py` contendo a estrutura da rota a ser direcionada para o nosso index.html que contem o currículo.  

Acionar o server por meio do comando: 

    `python -m uvicorn main:app --reload`

Construir o Container

Crie um arquivo `Dockerfile` na raiz do seu projeto contendo as instruções para construir o seu container.

   ```Dockerfile
   # imagem base
        FROM python:3.11
    # diretório da imagem que vamos trabalhar
        WORKDIR /code

    # definição dos requirements 
        COPY ./requirements.txt /code/requirements.txt

        RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt
    #
        COPY . /code

    #Definição de acesso ao server
        CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]```

(Foi necessário acrescentar mais dependencias no requirements)

Então precisa fazer o build

    ```docker build -t nota11:latest```

Criar um Repositório no Docker Hub
No Docker Hub foi criado um repositório pulico onde posteriormente foi armazenado nosso container. 

Fazer o Push para o Docker Hub
O container foi setado com a tag com o nome do repositório no Docker Hub:

```
    docker tag vzeferino/teste-aula-zefe:latest
```

Em seguida foi feito o push do do container para o Docker Hub:

```
    docker push vzeferino/teste-aula-zefe:latest
```

Usar o Container do Docker Hub
Enfim é possível executar o container em qualquer máquina que tenha o Docker instalado:

```
docker run -p 4000:80 vzeferino/teste-aula-zefe:latest
```
