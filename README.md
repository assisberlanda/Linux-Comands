# Linux-Comands
Linux Fundamentals [Distros Linux](https://programadorviking.com.br/distros-linux-para-desenvolvedores/)
### [Criando e gerenciando usuários no GNU/Linux](https://www.infowester.com/usuarioslinux.php)
### [Principais comandos do Linux](https://www.linux.ime.usp.br/~albasalo/Apostila/apostila.pdf)
### [Gerência de Pacotes](https://docente.ifrn.edu.br/filiperaulino/disciplinas/isa-redes2n/linux-07-gerencia-de-pacotes)
### [Processos no Linux](https://www.infowester.com/linprocessos.php)
### []()



pwd # visualiza o caminho atual
	
cd / # vai para o diretório root

cd ~ # vai para o diretório do usuário

cd - # vai para o diretório que estava anteriormente

ls | more # visualiza pausadamente

ls /users/berlanda/documents # visualiza arquivos dentro do documents sem entrar nele

find -name arq* # Pesquisa em todos os diretórios que começa com arq

mkdir 'Meus Documentos' # cria diretório com nome com espaço

rm -rf # Apaga arquivos e diretórios recursivamente e forçado

____________________________________  ROOT __________________________________ 

sudo pass root # cria ou muda a senha do usuário Root

su # Vai para o usuário Root

su assis # volta para o usuário


____________________  Fazer o acesso remoto ssh direto pelo root ____________________________ 

nano /etc/ssh/sshd_config

# Alterar a linha

	#PermitRootLogin prohibit-password
	PermitRootLogin yes

systemctl status sshd

systemctl restart sshd


____________________ History comandos  ____________________________ 


history # Lista todos os comandos digitados

!177 # Repete o comando numero 177 do history

history | grep "documentos" # lista todos os comandos que foi usado documentos

export HISTTIMEFORMAT="%c  -  " # Visualiza a lista com datas.

history -c # Apaga o history

history -w # cria um arquivo com o history

set +o history # desabilita o history

set -o history # abilita o history

nano .bashrc # edita o tamanho do arquivo de history
 
____________________ Criação Usuário comandos  ____________________________ 


useradd Joao -m -c "Joao da Silva" -- # Criação de usuário

userdel -r -f Joao # Apaga usuário e a pasta home

chsh -s /bin/bash Joao -- # caso esqueça de indicar na criação qual é o bash

useradd Joao -m -c "Joao da Silva" -s /bin/bash -- # Criação de usuário

passwd Joao -- # Coloca senha


____________________ Criação Usuário Temporário  ____________________________ 


Useradd	guest -c "Convidado" -m -e 26/06/2022

Usermod guest -s /bin/bash

Passwd guest -e # Ou coloca a da de expiração da senha ou se não colocar data ja expira no prossigo acesso

Cat /etc/passwd # informações de usuários


____________________ Criação Usuário com Senha  ____________________________ 


useradd guest -c "Convidado" -m -s /bin/bash -p $(openssl passwd -crypt Senha123)


____________________ Criação Usuário com Script  ____________________________ 

mkdir /scripts -- # no diretório root

nano criar_users.sh -- # Cria script para criação

	#!/bin/bash # para criar um script

	echo "Criando usuários do Sistema...."

	useradd guest1 -c "convidado" -s /bin/bash -m -p $(openssl passwd -crypt Senha123)
	passwd guest1 -e

	useradd guest2 -c "convidado" -s /bin/bash -m -p $(openssl passwd -crypt Senha123)
	passwd guest2 -e

	useradd guest3 -c "convidado" -s /bin/bash -m -p $(openssl passwd -crypt Senha123)
	passwd guest3 -e


chmod +x criar_users.sh -- # Altera permissão para executar

./criar_users.sh -- # Executa o arquivo

Cat passed /etc/passwd -- # Visualiza criação de usuários


____________________ Criação Grupo de Usuário  ____________________________ 

Cat /etc/group
useradd mariana -c "Mariana dos Anjos" -m -s /bin/bash -p $(openssl passwd Senha123) -- # Sem o -crypt
cat /etc/group -- # Ver os grupos
usermod -G sudo,adm mariana

groupadd GRP_ADM -- # Cria grupo
groupdel GRP_ADM -- # Exclui grupo

useradd mariana -c "Mariana dos Anjos" -m -s /bin/bash -p $(openssl passwd Senha123) -G GRP_ADM -- # Cria Usuário ja com o Grupo

usermod -G GRP_ADM Joao -- # Muda o grupo atual

gpasswd -d mariana adm -- # Para somente retirar do grupo atual


____________________ Mudando Grupo de Usuário de um diretório ____________________________ 

ls -l
cat /etc/group
chown debora:GRP_ADM /adm/

# ____________________ Permissões ____________________________ 

### Exemplo:

	-rwxr-xr-x 1 root root 385 nov 11 16:08 criar_users.sh
| DONO | R - Leitura | W - Escrita  | X - Execução |
|-|-|-|-|
| GRUPO | R - Leitura | W - Escrita  | X - Execução |
| OUTROS | R - Leitura | W - Escrita  | X - Execução |


| LEITURA (R) |4 |
|-|-|
| GRAVAÇÃO (W) | 2 |
| EXECUÇÃO (X) | 1 |
| NENHUMA | 0 |

	chmod 750 /adm/
 
















































