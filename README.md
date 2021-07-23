# REALIZANDO UM DEPLOY NA AWS

### Recursos utilizados:
- ![AWS](https://console.aws.amazon.com)


### PASSO 1 - CREDENCIAIS
Para realizar o deploy na AWS é necessário criar um usuário através do serviço IAM.

O IAM irá fornecer um KEY ID e ACCESS KEY.

No processo de criação do usuário é necessário vincular as seguintes politicas: 

- AmazonEC2ContainerRegisterFullAccess;
- Administrador Access;
- AdministradorEC2COntainerServiceforEC2Role



### PASSO 2 - INSTALAR AWS 
O aws cli é uma ferramenta que permite interar com os serviços da AWS usando comandos no shell da linha de comando.

Teste foi realizado no ambiente Linux, Distro Ubuntu.
```
$aws --version
```

![ Guia de Instalação da AWS ] (https://docs.aws.amazon.com/pt_br/cli/latest/userguide/install-cliv2.html)

### PASSO 3 - INSTALAR DOCKER-MACHINE

### PASSO 4 - APLICAÇÃO VUE.js

### PASSO 5 - DOCKERFILE E MULTISTAGE BUILD

## PASSO 6 - AUTENTICAR-SE NO SERVIÇO AWS

### PASSO 7 - SUBIR A IMAGEM PARA SERVIÇO AWS

### PASSO 8 - INSTÂNCIA EC2

## PASSO 9 - EXPOR A PORTA 

### PASSO 10 - EXCLUIR RECURSOS





