git-clone-repos
=========

Role do Ansible com passos para clonar uma lista de repositórios do Git para a máquina alvo.

Distribuições Suportadas pela Role
------------

- Fedora 30 ou superior
- Linux Mint LMDE 3 ou superior
- Linux Mint 19.0 ou superior
- openSUSE Leap 15.0 ou superior
- openSUSE Tumbleweed
- Ubuntu 18.04 ou superior


Variáveis da Role 
--------------

- url_protocol: Protocolo da URL principal do repositório. Valor padrão: https .
- git_root_url (Obrigatório): Url principal do repositório. Exemplo: github.com .
- repo_names (Obrigatório): Lista com nomes dos repositórios a serem clonados na máquina alvo.
- local_repos_root (Obrigatório): Diretório raiz, na máquina alvo, onde vão ficar todos os repositórios clonados.
- git_username (Obrigatório): Nome de usuário do GitHub (Usuário que fica na url dos repositórios, não o email).
- git_pass: Senha do usuário no GitHub, utilizada para clonar repositórios privados.


Dependências da Role 
--------------

Todos os SO:

- Ter o git instalado na máquina alvo.

Linux Mint e Ubuntu:

- openssh-server. Ex.: sudo apt install openssh-server


Exemplo de Inventario
----------------

Exemplo de arquivo de hosts: pasta_invetario/hosts

    [NOME]
    IP ansible_connection=ssh ansible_ssh_user=USUARIO ansible_ssh_pass=SENHA_URUARIO ansible_become_pass=SENHA_ROOT


Especificar interpretador python 3: pasta_invetario/group_vars/all

    ansible_python_interpreter: "/usr/bin/python3"


Exemplo de Playbook
----------------

Exemplo de uso da Role:

    - hosts: desktop
      vars:
        - root_dir: "environment"
        - gh_username: "userTest"
        - repos:
            - repo_01
            - repo_02
      roles:
         - { 
             role: github-clone-repos,
             repo_names: "{{ repos }}",
             local_repos_root: "{{ root_dir }}",
             git_username: "{{ gh_username }}"
            }


Exemplo de Comandos
----------------

Comando para executar todas as tasks:

    ansible-playbook -i <caminho_inventario> <caminho_playbook>


License
-------

MIT