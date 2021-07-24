# REALIZANDO UM DEPLOY NA AWS


### TECNOLOGIAS:
[AWS](https://console.aws.amazon.com)

[DOCKER MACHINE](https://docs.docker.com/machine)


### Procedimento Docker

Com a configuração abaixo a imagem obteve o tamanho de 266 MB:
```
$ aws --version
```

Com o recurso de Multistage Build foi reduzi o tamanho da imagem para 26 MB:





### Procedimento AWS
Checar a versão do aws-cli:
```
$ aws --version
```

Com as credencias acesse o terminal e digite comando:
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




Checar a versão do docker-machine:
```
$ docker-machine --version
```





### AWS - ELASTIC CONTAINER REGISTER (ECR)




### PASSO 8 - INSTÂNCIA EC2




## PASSO 9 - EXPOR A PORTA 



### PASSO 10 - EXCLUIR RECURSOS



### LINKS:
[Instalação do AWS CLI](https://docs.aws.amazon.com/pt_br/cli/latest/userguide/install-cliv2.html)
[Instalação do Docker-Machine](https://docs.docker.com/machine/install-machine/)


### GLOSSÁRIO:
- aws cli: O aws cli é uma ferramenta que permite interar com os serviços da AWS usando comandos no shell da linha de comando.
- docker-machine: é uma ferramenta que instala o docker-engine em host virtual, isto possibilita executar comandos em um data center ou em um cloud provider.
