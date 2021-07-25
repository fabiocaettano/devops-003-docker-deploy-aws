# REALIZANDO UM DEPLOY NO SERVIÇO AWS 

### Objetivo do laboratório:
- Configurar um arquivo Dockerfile com MultiStage Build;
- Armazenar a imagem no repositório da AWS, utilizando o serviço ECR;
- Autenticar-se no serviço da AWS através de comando de linha;
- Realizar um deploy no serviço de cloud da AWS, utilizando a instância EC2;
- Utiizr a ferramenta docker-machine que possibilita interagir com o servidor cloud através de comando de linha.
- Export as porta do container;
- Acessar aplicação através do browser.


### Pré-requisitos:
- Ter uma conta na AWS Service;
- Através do IAM (serviço da AWS) cadastrar 1 usuário e vincular as seguintes politicas:  ;
- Instalações necessárias: aws-cli, docker e docker-machine.



### Analisando o arquivo Dockerfile:

O Dockerfile abaixo gerou uma imagem com o tamanho de 266 MB:
```
FROM node
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 8080
CMD [ "node", "index.js" ]
```

Com o recurso de Multistage Build é possivel otimizar este processo de construção de imagem.
O arquivo Dockerfile foi reestruturado.
No primeiro FROM é realizado o build da aplicação.
Já no segundo FROM a imagem é apenas de execução permitindo a redução para 26 MB.
```
FROM node:lts-alpine as build
WORKDIR /app
RUN npm install -g http-server
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build


FROM nginx:alpine
WORKDIR /app
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```


### Credenciais AWS

Acesse o terminal e verique a versão do aws-cli:
```
$ aws --version
```

Digite comando para configurar o usuário:
```
$ aws configure
```

Informe as credenciais (IAM):
```
$ AWS Access Key ID:
$ AWS Secret Access Key:
$ Default region name:
$ Default output format:

```


### Subindo a imagem para o ECR

No site da AWS,procure o serviço Elastic Container Register (ECR).
![](https://github.com/fabiocaettano/docker-deploy-aws/blob/main/images/ecr_search.png)

Após utilizar a oção "get started" será exibido um formulário, selecione a opção "Private", informe um nome para o repositório. 
Para confirmar utilize o botão "Create Repository" no final da página.

![](https://github.com/fabiocaettano/docker-deploy-aws/blob/main/images/ecr_create.png)


Selecione o repositório criado e utilize o botão "View push commands":
![](https://github.com/fabiocaettano/docker-deploy-aws/blob/main/images/ecr_commands.png)

Será exibido uma sequencia de 4 comandos para serem copiados.

O primeiro comando é outra autenticação da aws.
Acesse o terminal e cole o comando:
```
$ aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 999999999999.dkr.ecr.us-east-1.amazonaws.com
```
Se tudo der certo será exibido uma mensagem no terminal: Login Successed.


O segundo comando solicita que a imagem seja criada no seu host.
Agora acesse a pasta do projeto pelo terminal.
O arquivo Dockerfile deve estar na raiz do projeto.
Digite o comando no terminal:
```
$ docker build -t nomeDoRepositorio/nomeDaAplicacao:tag .
```

Para visualizar a imagem no seu host:
```
$ docker image ls
```

O terceiro comando eles solicita a execução do comando docker tag (versionamento da aplicação):
```
docker tag vue-hello-world:latest 999999999999.dkr.ecr.us-east-1.amazonaws.com/vue-hello-world:latest
```
O quarto comando é momento de subir imagem para o repositório da Amazon (ECR):
```
docker push 999999999999.dkr.ecr.us-east-1.amazonaws.com/vue-hello-world:latest
```

Volte ao site da AWS e veja a imagem:




Checar a versão do docker-machine:
```
$ docker-machine --version
```



### PASSO 8 - INSTÂNCIA EC2




## PASSO 9 - EXPOR A PORTA 



### PASSO 10 - EXCLUIR RECURSOS



### LINKS DIVERSOS:
[Dockerizando sua aplicação Vue.js](https://br.vuejs.org/v2/cookbook/dockerize-vuejs-app.html)
[Instalação AWS CLI](https://docs.aws.amazon.com/pt_br/cli/latest/userguide/install-cliv2.html)
[Instalação Docker](https://docs.docker.com/engine/install/)
[Instalação Docker-Machine](https://docs.docker.com/machine/install-machine/)



[AWS](https://console.aws.amazon.com)

[DOCKER](https://www.docker.com/)

[DOCKER MACHINE](https://docs.docker.com/machine)



### GLOSSÁRIO:
- aws cli: O aws cli é uma ferramenta que permite interar com os serviços da AWS usando comandos no shell da linha de comando;

- Dockerfile: arquivo de configuração para construção de imagem de um container;

- docker-machine: É uma ferramenta que instala o docker-engine no host virtual, e isto possibilita executar comandos em um data center ou em um cloud provider;

- EC2: O Amazon Elastic Compute Cloud (Amazon EC2) é um serviço da web que fornece capacidade de computação escalável que você pode utilizar para criar e hospedar os seus sistemas de software;

- ECR: O Amazon Elastic Container Registry (Amazon ECR) é um registro de contêineres totalmente gerenciado do Docker que permite que desenvolvedores armazenem, gerenciem e implantem facilmente imagens de contêiner do Docker;

- IAM: O AWS Identity and Access Management (IAM) é um serviço da Web que tem como objetivo controlar o acesso aos serviços da AWS de forma segura. Com o IAM, é possível gerenciar de maneira centralizada usuários, credenciais de segurança, como chaves de acesso e permissões que controlam quais recursos e aplicações da AWS os usuários podem acessar. 

- MutiStage build: processo de otimizar imagens quando do processamento do arquivo Dockerfile;
