# Ansible SSH Key Generation

## Visão Geral
Este projeto contém um playbook Ansible para gerar pares de chaves SSH em servidores remotos.

Neste playbook:

O módulo setup coleta as informações sobre o sistema, incluindo o hostname.
As chaves SSH são nomeadas usando adminssh-key-{{ ansible_hostname }}, onde ansible_hostname é o nome da máquina coletado durante a execução.
A chave privada é movida para fora da máquina com o nome apropriado.
A chave pública é mantida na máquina remota.

## Arquivos
- `inventory/hosts`: Arquivo de inventário com detalhes dos servidores.
- `playbooks/create_ssh_key.yml`: Playbook para gerar chaves SSH.


## Uso
1. Atualize o arquivo `inventory/hosts` com os detalhes do seu servidor.

## IP
IP: Este é o endereço IP do host ao qual o Ansible se conectará para executar as tarefas. Pode ser um endereço IP ou um nome de domínio.

## ansible_user

ansible_user=nomedousuário: Define o nome de usuário usado para se conectar ao host remoto. Neste caso, nomedousuário será usado como o nome de usuário SSH.

## ansible_ssh_pass

ansible_ssh_pass=senhadousuário: Define a senha usada para autenticação SSH. senhadousuário será usada como a senha para se autenticar no host remoto.

## ansible_become_pass

ansible_become_pass=senhadousuário: Define a senha que será usada para elevar privilégios (sudo). Isso é útil quando o usuário precisa executar comandos como superusuário (root).

## ansible_ssh_common_args

ansible_ssh_common_args='-o StrictHostKeyChecking=no': Define argumentos adicionais para a linha de comando SSH. A opção -o StrictHostKeyChecking=no desativa a verificação da chave de host SSH. Isso é útil em ambientes onde os hosts são dinâmicos ou quando você deseja evitar a verificação manual das chaves de host. No entanto, pode ser uma prática insegura, pois desativa uma camada de proteção contra ataques de "man-in-the-middle".


2. Execute o playbook com:

```sh
ansible-playbook -i inventory/hosts playbooks/create_ssh_key.yml




