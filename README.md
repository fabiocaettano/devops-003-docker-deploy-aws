# REALIZANDO UM DEPLOY NO SERVIÇO AWS 

### Objetivo do laboratório:
- Configurar um arquivo Dockerfile com MultiStage Build;
- Armazenar a imagem no repositório da AWS, utilizando o serviço ECR;
- Autenticar-se no serviço da AWS através de comando de linha;
- Realizar um deploy no serviço de cloud da AWS, utilizando a instância EC2;
- Utiizr a ferramenta docker-machine que possibilita interagir com o servidor cloud através de comando de linha.
- Expor a porta do container;
- Acessar aplicação através do browser.


### Pré-requisitos:
- Ter uma conta na AWS Service;
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
Aplicando este conceito o Dockerfile foi modificado com o seguinte detalhe:
- No primeiro FROM é realizado o build da aplicação;
- No segundo FROM a imagem é apenas de execução usando o nginx:alpine , e copiando aenas a pasta dist e reduzindo a imagem para 26 MB.
Estte Dockerfile será utilizado no laboratório:
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

Informe as credenciais:
```
$ AWS Access Key ID:
$ AWS Secret Access Key:
$ Default region name:
$ Default output format:

```
Observação: Estas credenciais são obtidas no cadastro de usuário na AWS, utilizando o serviço IAM.
No processo de cadastro do usuário foi vinculado 3 politicas cito:



### Subindo a imagem para o ECR

No site da AWS,procure o serviço Elastic Container Register (ECR).
![](https://github.com/fabiocaettano/docker-deploy-aws/blob/main/images/ecr_search.png)


Para iniciar o processo é necessário clicar no botão "Get Started".
Na sequencia selecione a opção "Private", informe um nome para o repositório. 
Para finalizar utilize o botão "Create Repository", que se no final do formulário.
![](https://github.com/fabiocaettano/docker-deploy-aws/blob/main/images/ecr_create.png)



Selecione o repositório criado e utilize o botão "View push commands":
![](https://github.com/fabiocaettano/docker-deploy-aws/blob/main/images/ecr_commands.png)


Será exibido uma sequencia de 4 comandos para serem copiados.

1º comando:
É outra autenticação da aws.
Acesse o terminal e cole o comando:
```
$ aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 999999999999.dkr.ecr.us-east-1.amazonaws.com
```
Se tudo der certo será exibido uma mensagem no terminal: Login Successed.

2º comando:
Solicita que a imagem seja criada no seu host.
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

3º comando:
Solicita a execução do comando docker tag para versionamento da aplicação:
```
$ docker tag vue-hello-world:latest 999999999999.dkr.ecr.us-east-1.amazonaws.com/vue-hello-world:latest
```

4º comando:
É momento de subir imagem para o repositório da Amazon (ECR):
```
docker push 999999999999.dkr.ecr.us-east-1.amazonaws.com/vue-hello-world:latest
```

Volte ao site da AWS ppara visualizar a imagem inserida no repositório:





### Criando a instância ECD através de linha de comando

O docker-machine acessa o host virtual como Azure, AWS.

Primeiro vamos checar a versão do docker-machine no terminal:
```
$ docker-machine --version
```

O comando abaxio vai gerar a instância EC2.
```
$ docKer-machine create --driver amazonec2 --amazonec2-instance-type "t2.micro" --amazonec2-region "us-east-1" aws0001
```
Importante a partir do próximo comando iremos acessar o servidor , então os próximos irão refletir no host virtual e não no host da sua máquina.
```
$ eval $(docker-machine env aws0001)
```

Execute os comados abaixo para checar que você está no host virtual:
```
$ docker image ls
$ docker container ls -a
```






## PASSO 9 - EXPOR A PORTA 



### PASSO 10 - EXCLUIR RECURSOS



### LINKS DIVERSOS:
[Consolde AWS](https://console.aws.amazon.com)
[Dockerizando sua aplicação Vue.js](https://br.vuejs.org/v2/cookbook/dockerize-vuejs-app.html)
[Instalação AWS CLI](https://docs.aws.amazon.com/pt_br/cli/latest/userguide/install-cliv2.html)
[Instalação Docker](https://docs.docker.com/engine/install/)
[Instalação Docker-Machine](https://docs.docker.com/machine/install-machine/)


### GLOSSÁRIO:
- aws cli: O aws cli é uma ferramenta que permite interar com os serviços da AWS usando comandos no shell da linha de comando;

- Dockerfile: arquivo de configuração para construção de imagem de um container;

- docker-machine: É uma ferramenta que instala o docker-engine no host virtual, e isto possibilita executar comandos em um data center ou em um cloud provider;

- EC2: O Amazon Elastic Compute Cloud (Amazon EC2) é um serviço da web que fornece capacidade de computação escalável que você pode utilizar para criar e hospedar os seus sistemas de software;

- ECR: O Amazon Elastic Container Registry (Amazon ECR) é um registro de contêineres totalmente gerenciado do Docker que permite que desenvolvedores armazenem, gerenciem e implantem facilmente imagens de contêiner do Docker;

- IAM: O AWS Identity and Access Management (IAM) é um serviço da Web que tem como objetivo controlar o acesso aos serviços da AWS de forma segura. Com o IAM, é possível gerenciar de maneira centralizada usuários, credenciais de segurança, como chaves de acesso e permissões que controlam quais recursos e aplicações da AWS os usuários podem acessar. 

- MutiStage build: processo de otimizar imagens quando do processamento do arquivo Dockerfile;
