# Fazendo Deploy na AWS (Amazon Cloud Services)
### Passo-a-passo para subir um projeto na AWS

Esse repositório tem como objetivo mostrar um exemplo básico e prático para colocar um produção qualquer projeto na AWS.
Para que se possa subir um projeto para a nuvem, ou fazer seu deploy, existem algumas condições básicas a serem cumpridas:
## 1 - Faça seu cadastro junto a AWS (Amazon Web Services)
![image](https://github.com/user-attachments/assets/8390ab43-043d-4bd8-8d28-cfb0f01b35d0)

Antes de iniciar a condifuração de uma nova máquina virtual na AWS, é importante que se tenham as chaves públicas e privadas configuradas em seu computador, para o acesso SSH, à máquina virtual.
Ficam alguns exemplos de como fazer tal configuração, caso a mesma já não tenha sido feita anteriormente.

## 2 - Verificando a Existência de um Par de Chaves
Caso existam chaves SSH já configuradas, existirá no diretório de seu usuário, um diretório oculto de nome /.ssh com alguns arquivos dentro.
Para verificar se as mesmas existem, execute o seguinte comando no terminal de seu computador:
![image](https://github.com/user-attachments/assets/0e877fe2-03e8-4c41-a128-caf20adff10c)

Caso existam chaves, como no exemplo acima, ignore os seguintes passos para criação das chaves. Caso contrário, crie um par de chaves, conforme abaixo:

[Git Hub SSH](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
[Hostinger SSH](https://www.hostinger.com.br/tutoriais/como-configurar-chaves-ssh)

# Configuração da VM na AWS.
Após ter se registrado na AWS, podemos começar a configuração de uma máquina para publicar nossa aplicação.

Precisaremos efetuar as seguintes configurações, antes da criação de nossa máquina:

- Criar e configurar uma nova VPC (Virtual Private Cloud).
- Criar e configurar um novo Security Group, ou grupo de segurança.
- Criar e configurar uma nova instância EC2.
- Copiar e executar nosso projeto, para a instância criada.

### Criar e configurar uma nova VPC (Virtual Private Cloud).

Faça login em sua conta da AWS, e o seguinte console deverá ser apresentado:
![image](https://github.com/user-attachments/assets/73c8e90b-48e1-4db2-8164-8745d1be5837)

Na barra superior digite vpc, para criarmos a nossa:
![image](https://github.com/user-attachments/assets/4ca3fce5-dc0c-4318-a948-b6d9810ae072)
![image](https://github.com/user-attachments/assets/363bbc75-3909-47ab-8428-5e21acafaa73)

Selecione VPC e muito mais.
![image](https://github.com/user-attachments/assets/0ffaa9aa-2096-443a-8012-a41c3c87b90c)

De um nome para sua VPC, nenhuma outra configuração é necessária aqui.
![image](https://github.com/user-attachments/assets/ae149b63-888f-4c2a-b0f7-eb08d116efc6)

Clique em Criar VPC
![image](https://github.com/user-attachments/assets/b2daab18-0802-471d-8afc-60b2bc477c1f)

Verificando VPC criada
![image](https://github.com/user-attachments/assets/e2047358-34c9-486f-990c-ef1e764a3e53)

## Configurando um novo Security Group
Na barra superior, busque por Security Groups
![image](https://github.com/user-attachments/assets/dac30ce0-5995-48b1-82a9-a02a4fc8069f)

Clique em Criar grupo de segurança
![image](https://github.com/user-attachments/assets/eaa7b1b6-d2ee-44f2-b41c-56b49afa001d)

De um nome, ao seu grupo de segurança, e atrele o mesmo, a VPC criada anteriormente:
![image](https://github.com/user-attachments/assets/f1e797d5-af8d-43b9-8459-f303f4691cbf)

Por padrão, na criação de um grupo de segurança novo, somente o tráfego de saída, ou seja VM->Internet é liberado. O tráfego de entrada é totalmente restrito e precisar ser liberado.

Precisaremos liberar a porta 22 (SSH), para acessarmos o console de nossa VM remotamente, e também, a porta 8080, que nesse caso específico, é a porta utilizada por nossa aplicação.
![image](https://github.com/user-attachments/assets/78ff0115-9639-40ce-804d-52f814899ad4)
Como deixamos o acesso irrestrito a essas portas (0.0.0.0/0) recebemos um aviso. É possível, caso os IP's que farão o acesso a VW sejam conhecidos, restringir esse acesso a somente alguns IP's.

Configurados os acesso, é so clicar em criar grupo de segurança:
![image](https://github.com/user-attachments/assets/176e22e6-fb4e-4a8b-8a97-abc53f39cccf)

Grupo de segurança criado.
![image](https://github.com/user-attachments/assets/3867580d-de45-4917-a900-2d6d8294081c)

## Configurando uma Máquina Virtual (VM)
Após criarmos nossa VPC, e um Security Group, podemos criar a nossa VM.

Para isso, busque por EC2, na barra superior:
![image](https://github.com/user-attachments/assets/22ed9236-5b38-44e4-a6b0-be87b3c7ae16)

Ao acessar o painel de controle, clique em Excecutar instância:
![image](https://github.com/user-attachments/assets/7bad5800-a5c8-4e1a-8d66-90a2dca69ea7)

De um nome a sua nova instância (VM)
![image](https://github.com/user-attachments/assets/78fffb07-b895-4bef-8e55-9150f0f48623)

Vamos utilizar o Amazon Linux, que é o SO padrão pré selecionado:
![image](https://github.com/user-attachments/assets/97074f5b-35a2-4f10-a5a7-afa5dc3736ab)

Aqui é necessário indicar qual será o par de chaves SSH a ser utilizado.

Caso não tenha nenhuma cadastrado, procure a opção Keys Pairs para importar o seu par de chaves, criado anteriormente.
![image](https://github.com/user-attachments/assets/7676312b-5454-4509-bb6d-9aa2364c9ff4)

Precisamos editar as configurações de rede de nossa VM, para atrelar nossa VPC, Security Group e IP externos, clicando em editar:
![image](https://github.com/user-attachments/assets/a6ba6a66-4dc7-45e4-974a-aea0ef1b7009)

Certifcar-se, de que a instância está configurada em uma Sub-net public, e que Atribuir IP público está em Habilitar. Também selecionar a VPC e o Security Group anteriormente criados.

Feitas as configurações da instância, podemos executar-lá, clicando em Executar instância:
![image](https://github.com/user-attachments/assets/442c5801-5bff-4c9f-8b56-13e1b1394837)

Tela após a criação da instância:
![image](https://github.com/user-attachments/assets/25bcf174-38e7-463b-826f-be93fbf3357a)

Para verifcarmos se as configurações estão funcionando corretamente, podemos fazer a conexão via SSH, a nossa instância.
Para isso basta clicar em Conectar à sua instância:
Copiar o comando ssh, para fazer a conexão:
![image](https://github.com/user-attachments/assets/0ce47de1-5de8-45fd-92de-d813f2e78c52)

Conectando a instância:
Suas credencias serão necessárias:
![image](https://github.com/user-attachments/assets/0d4fef4a-c9ba-4408-9cba-c8b98925eafb)

## Instalando o JRE na VM
Conectado a VM, agora para rodar nossa aplicação, precisaremos da JRE do Java, para executar nossa aplicação.
Para instalar a JRE 17, basta executar o seguinte comando:
``` bash
sudo yum install java-17-amazon-corretto-headless
```
![image](https://github.com/user-attachments/assets/d2d62d08-87c3-460e-87f8-9b13a79efbef)

Siga os passos necessários para concluir a instalação.

Com a instalação, da JRE, basta agora, copiarmos a nossa aplicação (.jar) de nosso projeto, para a nossa instância.
- Empacotar o jar, no nosso caso utilizando o Maven
![image](https://github.com/user-attachments/assets/a6db29a2-f9a5-404d-bb5b-3e740560b58a)


## Copiar e executar nosso projeto, para a instância criada.

É importante se atentar, que o comando deve ser executado no terminal de nossa máquina, onde está o nosso projeto, e não na VM da Amazon.
```bash
scp meu-projeto.jar ec2-user@meu-ip-ou-meu-dns:/home/ec2-user
```
![image](https://github.com/user-attachments/assets/4e81fd50-9ef8-4b99-a5b2-53a4561dd378)

Em seguida, podemos verificar se o arquivo estão em nossa VM, conectando novamente via SSH e listando os arquivos na /home do ec2-user.
```bash
ls
```
![image](https://github.com/user-attachments/assets/2a90a164-24d4-4ae0-82b9-7ad134071911)

Em seguida podemos executar nossa aplicação:
```bash
java -jar meu-jar.jar
```
![image](https://github.com/user-attachments/assets/33af70b5-8469-42cc-a323-b1758d12aa3b)

Para verificar se aplicação está publicada, podemos acessa-la através de seu IP, na porta 8080:

![image](https://github.com/user-attachments/assets/4664633e-5d9b-44fb-8ff4-f2847ebb35dc)

Agora basta acessar [http://meu-ip:8080/meu-endpoint](http://meu-ip:8080/meu-endpoint)


# Material complementar:

[Fazendo Deploy na AWS](https://www.youtube.com/watch?v=bEkCdlrxF54&t=1117s&pp=ygUKZGVwbG95IGF3cw%3D%3D)

[Amazon Code Deploy](https://aws.amazon.com/pt/codedeploy/)

[Git Hub SSH](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

[Hostinger SSH](https://www.hostinger.com.br/tutoriais/como-configurar-chaves-ssh)

















