# Docker no Ubuntu
### Instalação:

1. Configure o repositório Apt do Docker
~~~shell
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
~~~

2. Instale os pacotes Docker.
~~~shell
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
~~~
3. Verifique se a instalação do Docker Engine foi bem-sucedida executando a imagem hello-world.
~~~shel
sudo docker run hello-world
~~~

Recebendo erros ao tentar executar sem root?

O grupo de usuários `docker` existe, mas não contém usuários, por isso é necessário usar o `sudo` para executar comandos do Docker.

Para criar o grupo `docker` e adicionar seu usuário:

1. Crie o grupo `docker`.
~~~shel
sudo groupadd docker
~~~
2. Adicione seu usuário ao grupo docker.
~~~shel
sudo usermod -aG docker $USER
~~~
3. Saia e faça login novamente para que sua participação no grupo seja reavaliada. Você também pode executar o seguinte comando para ativar as alterações nos grupos:
~~~shel
newgrp docker
~~~
4. Verifique se você pode executar comandos do docker sem o sudo.
~~~shel
docker run hello-world
~~~

### Criando uma imagem Docker
1. Crie um arquivo vazio chamado Dockerfile.
~~~shel
touch Dockerfile
~~~
2. Usando um editor de texto ou editor de código, adicione o seguinte conteúdo ao Dockerfile:
~~~shel
# syntax=docker/dockerfile:1

FROM node:18-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000
~~~
3. Construa a imagem usando os seguintes comandos:
~~~shel
docker build -t getting-started .
~~~

### Iniciar um container de aplicativo
~~~shel
docker run -dp 127.0.0.1:3000:3000 getting-started
~~~

### Fontes:
* https://docs.docker.com/desktop/install/ubuntu/
* https://docs.docker.com/get-started/02_our_app/
* https://busy-sunspot-00c.notion.site/Settings-for-EC2-db344aed5235413d9e0f71e6d457ba90
