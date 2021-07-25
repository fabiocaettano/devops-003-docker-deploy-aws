# REALIZANDO UM DEPLOY NO SERVIÇO AWS 

Objetivo desse laboratório:
- Realizar um deploy no serviço de cloud da AWS, utilizando a instância EC2;
- Configurar um arquivo Dockerfile para gerar uma imagem da aplicação feita em vue.js;
- Armazenar a imagem no repositório da AWS, utilizando o serviço ECR;
- Autenticar-se no serviço da AWS através de comando de linha;
- Utiizr a ferramenta docker-machine que possibilita interagir com o servidor cloud através de comando de linha.
- Export as porta do container;
- Acessar aplicação através do browser.



### TECNOLOGIAS:
[AWS](https://console.aws.amazon.com)

[DOCKER](https://www.docker.com/)

[DOCKER MACHINE](https://docs.docker.com/machine)




### Criando a Imagem da aplicação Vue.js

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


Com o recurso de Multistage Build reconfigurei o arquivo e reduzi o tamanho da imagem para 26 MB:
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


### Procedimento na AWS
Acessar o terminal do host e verique a versão do aws-cli:
```
$ aws --version
```

Digite comando para configurar o usuário:
```
$ aws configure
```

Informe as credenciais obtidas quando do cadastro do usuário utilizando o serviço IAM:
```
$ AWS Access Key ID:
$ AWS Secret Access Key:
$ Default region name:
$ Default output format:

```


No site da AWS,procure o serviço Elastic Container Register (ECR).
![](https://github.com/fabiocaettano/docker-deploy-aws/blob/main/images/ecr_search.png)

Após utilizar a oção "get started" será exibido o seguinte formulário, selecione a opção particular e informe um nome para o repositório. Para confirmar utilize o botão "Create Repository".

![](https://github.com/fabiocaettano/docker-deploy-aws/blob/main/images/ecr_create.png)


Selecione o repositório criado e utilize o botão "View Push Commands", irá surgir uma página com uma sequencia de 4 comandos para serem copiados. Explico isso logo após a imagem:

![](https://github.com/fabiocaettano/docker-deploy-aws/blob/main/images/ecr_commands.png)


Acesse o seu terminal e cole o comando paa autenticar-se no serviço da aws e permitindo subir as imagens para o serviço aws.
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 999999999999.dkr.ecr.us-east-1.amazonaws.com

Acesse a pasta do projeto aonde está salvo o arquivo Dockerfile e execute o comando:
Para construir a imagem execute o comando no terminal:
```
$ docker build -t nomeDoRepositorio/nomeDaAplicacao:tag .
```

Para visualizar a imagem:
```
$ docker image ls
```

Ainda no terminal

docker tag vue-hello-world:latest 999999999999.dkr.ecr.us-east-1.amazonaws.com/vue-hello-world:latest

Agora vamos subir a imagem para o repositório:
docker push 468981229068.dkr.ecr.us-east-1.amazonaws.com/vue-hello-world:latest



Volte ao site 




Checar a versão do docker-machine:
```
$ docker-machine --version
```



### PASSO 8 - INSTÂNCIA EC2




## PASSO 9 - EXPOR A PORTA 



### PASSO 10 - EXCLUIR RECURSOS



### LINKS:
[Instalação AWS CLI](https://docs.aws.amazon.com/pt_br/cli/latest/userguide/install-cliv2.html)
[Instalação Docker](https://docs.docker.com/engine/install/)
[Instalação Docker-Machine](https://docs.docker.com/machine/install-machine/)


### GLOSSÁRIO:
- aws cli: O aws cli é uma ferramenta que permite interar com os serviços da AWS usando comandos no shell da linha de comando.
- docker-machine: é uma ferramenta que instala o docker-engine em host virtual, isto possibilita executar comandos em um data center ou em um cloud provider.
