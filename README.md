# deploy-aws
Passo-a-passo para subir um projeto na AWS

Esse repositório tem como objetivo mostrar um exemplo básico e prático para colocar um produção qualquer projeto na AWS.
Para que se possa subir um projeto para a nuvem, ou fazer seu deploy, existem algumas condições básicas a serem cumpridas:
1 - Faça seu cadastro junto a AWS (Amazon Web Services)
![image](https://github.com/user-attachments/assets/8390ab43-043d-4bd8-8d28-cfb0f01b35d0)

Antes de iniciar a condifuração de uma nova máquina virtual na AWS, é importante que se tenham as chaves públicas e privadas configuradas em seu computador, para o acesso SSH, à máquina virtual.
Ficam alguns exemplos de como fazer tal configuração, caso a mesma já não tenha sido feita anteriormente.

## Verificando a Existência de um Par de Chaves
Caso existam chaves SSH já configuradas, existirá no diretório de seu usuário, um diretório oculto de nome /.ssh com alguns arquivos dentro.
Para verificar se as mesmas existem, execute o seguinte comando no terminal de seu computador:
![image](https://github.com/user-attachments/assets/0e877fe2-03e8-4c41-a128-caf20adff10c)

Caso existam chaves, como no exemplo acima, ignore os seguintes passos para criação das chaves.

[Git Hub SSH](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
[Hostinger SSH](https://www.hostinger.com.br/tutoriais/como-configurar-chaves-ssh)

# Configuração da VM na AWS.
Após ter se registrado na AWS, podemos começar a configuração de uma máquina para publicar nossa aplicação.

Precisaremos efetuar as seguintes configurações, antes da criação de nossa máquina:

- Criar e configurar uma nova VPC (Virtual Private Cloud).
- Criar e configurar um novo Security Group, ou grupo de segurança.
- Criar e configurar uma nova instância EC2.

