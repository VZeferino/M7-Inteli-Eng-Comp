# Instruções para Montar o Projeto

## 1. Configurando o Ambiente
- **Criação do Arquivo Principal**:
  - Crie um arquivo chamado `main.py`. Este arquivo deve conter a estrutura da rota que direciona para o `index.html`, onde está o currículo.

- **Iniciando o Servidor**:
  \`\`\`bash
  python -m uvicorn main:app --reload
  \`\`\`

## 2. Configuração do Container Docker

- **Criação do Dockerfile**:
  - No diretório raiz do projeto, crie um arquivo chamado `Dockerfile`. Este arquivo deve ter as seguintes instruções:
    \`\`\`Dockerfile
    # imagem base
    FROM python:3.11

    # diretório da imagem que vamos trabalhar
    WORKDIR /code

    # definição dos requirements 
    COPY ./requirements.txt /code/requirements.txt
    RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt

    # copiando conteúdo para o diretório /code da imagem
    COPY . /code

    # definição de acesso ao server
    CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]
    \`\`\`
  - Note: Foi necessário acrescentar mais dependências no `requirements.txt`.

- **Construção (Build) do Docker Image**:
  \`\`\`bash
  docker build -t nota11:latest .
  \`\`\`

## 3. Docker Hub

- **Criação de Repositório**:
  - No Docker Hub, crie um repositório público para armazenar o container.

- **Tag e Push**:
  - Adicione uma tag ao seu container com o nome do seu repositório no Docker Hub:
    \`\`\`bash
    docker tag nota11:latest vzeferino/teste-aula-zefe:latest
    \`\`\`
  - Faça o push do seu container para o Docker Hub:
    \`\`\`bash
    docker push vzeferino/teste-aula-zefe:latest
    \`\`\`

## 4. Utilizando o Container

- **Execução**:
  - Agora, você pode executar o container em qualquer máquina que possua o Docker instalado:
    \`\`\`bash
    docker run -p 4000:80 vzeferino/teste-aula-zefe:latest
    \`\`\`
