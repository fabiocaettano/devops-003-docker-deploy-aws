# REALIZANDO UM DEPLOY NA AWS

### TECNOLOGIAS:
- ![AWS](https://console.aws.amazon.com)
- ![DOCKER MACHINE](https://docs.docker.com/machine)


### INSTALAÇÕES NECESSÁRIAS

Checar a versão do aws-cli:
```
$aws --version
```

Checar a versão do docker-machine:
```
$docker-machine --version
```


### AUTENTICAR-SE NO SERVIÇO AWS
Para realizar o deploy na AWS é necessário criar uma conta.

E também criar um usuário através do serviço IAM.

O IAM irá fornecer um KEY ID e ACCESS KEY.

No processo de criação do usuário é necessário vincular as seguintes politicas: 

- AmazonEC2ContainerRegisterFullAccess;
- Administrador Access;
- AdministradorEC2COntainerServiceforEC2Role

Com as credencias acesse o terminal e digite comando:
```
$aws configure
```
Informe as credenciais:
```
$aws configure
```


### DOCKERFILE E MULTISTAGE BUILD

Com a configuração abaixo a imagem obteve o tamanho de 266 MB:



Com o recurso de Multistage Build é possivel otimizar o processo é reduzir o tamanho da imagem para 26 MB:




### AWS - ELASTIC CONTAINER REGISTER (ECR)




### PASSO 8 - INSTÂNCIA EC2




## PASSO 9 - EXPOR A PORTA 



### PASSO 10 - EXCLUIR RECURSOS



### LINKS:
- ![Instalação do AWS CLI](https://docs.aws.amazon.com/pt_br/cli/latest/userguide/install-cliv2.html)


### GLOSSÁRIO:
- aws cli: O aws cli é uma ferramenta que permite interar com os serviços da AWS usando comandos no shell da linha de comando.
- docker-machine: é uma ferramenta que instala o docker-engine em host virtual, isto possibilita executar comandos em um data center ou em um cloud provider.



