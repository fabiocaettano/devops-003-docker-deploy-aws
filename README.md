# REALIZANDO UM DEPLOY NA AWS

### TECNOLOGIAS:
- ![AWS](https://console.aws.amazon.com)
- ![DOCKER MACHINE](https://docs.docker.com/machine)
- ![LINUX - UBUNTU 20.0.4]

### INSTALAÇÕES NECESSÁRIAS
- ![Instalação do AWS CLI](https://docs.aws.amazon.com/pt_br/cli/latest/userguide/install-cliv2.html)

Checar a versão:
```
$aws --version
```

- ![Instalação do Docker-Machine](https://docs.docker.com/machine/install-machine/)

Checar a versão:
```
$docker-machine --version
```











### PASSO 1 - CREDENCIAIS
Para realizar o deploy na AWS é necessário criar um usuário através do serviço IAM.

O IAM irá fornecer um KEY ID e ACCESS KEY.

No processo de criação do usuário é necessário vincular as seguintes politicas: 

- AmazonEC2ContainerRegisterFullAccess;
- Administrador Access;
- AdministradorEC2COntainerServiceforEC2Role



### PASSO 2 - INSTALAR AWS CLI
### PASSO 3 - INSTALAR DOCKER-MACHINE
O docker-machine é uma ferramenta que instala o docker-engine em host virtual, isto possibilita executar comandos em um data center ou em um cloud provider.



### PASSO 4 - APLICAÇÃO VUE.js
O foco desse laboratório é o deploy na AWS,aplicação é bem simples apenas para que possamos realizar o build.


### PASSO 5 - DOCKERFILE E MULTISTAGE BUILD



## PASSO 6 - AUTENTICAR-SE NO SERVIÇO AWS




### PASSO 7 - SUBIR A IMAGEM PARA SERVIÇO AWS




### PASSO 8 - INSTÂNCIA EC2




## PASSO 9 - EXPOR A PORTA 



### PASSO 10 - EXCLUIR RECURSOS

### GLOSSÁRIO:
- aws cli: O aws cli é uma ferramenta que permite interar com os serviços da AWS usando comandos no shell da linha de comando.



