- Instalar asdf (obs.: bash + git)

01. Passo: Acessar 
    url: https://asdf-vm.com/pt-br/guide/getting-started.html

    01.1. linux	Aptitude
   
         sudo apt install curl git
    
    01.2. Realizar o download do asdf

        git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.12.0

    01.3. Adicionando ao shell

        Bash & Git:
        - Adicione esta linha no: ~/.bashrc
            - "$HOME/.asdf/asdf.sh"
        - Auto complete é configurado manualmente adicionando a linha ao .bashrc:
            - "$HOME/.asdf/completions/asdf.bash"

- Instalar os plugins asdf
	- kubectl
	- terraform
- Instalar docer (sa containerd)
- Instalar golang


# Instalando e Configurando o Ansible

https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-20-04-pt

Passo 1 — Como instalar o Ansible

    Primeiro, atualize o índice de pacotes do seu sistema com:
    sudo apt update

    Após atualizar, instale o software do Ansible com:
    sudo apt install ansible

    Pressione "Y" quando solicitado a confirmar a instalação.

# Passo 2 — Configurando o arquivo de inventário

    sudo nano /etc/ansible/hosts

    /etc/ansible/hosts
    [servers]
    server1 ansible_host=203.0.113.111
    server2 ansible_host=203.0.113.112
    server3 ansible_host=203.0.113.113

    [all:vars]
    ansible_python_interpreter=/usr/bin/python3


    Sempre que quiser verificar seu inventário, você pode executar:

        ansible-inventory --list -y
        
Passo 3 — Testando a conexão

    ansible all -m ping -u root

Passo 4 — Executando comandos ad hoc (opcional)

    ansible all -a "df -h" -u root
    ansible all -m apt -a "name=vim state=latest" -u root
    ansible servers -a "uptime" -u root
    ansible server1:server2 -m ping -u root

# Instalar o Prometheus no Ubuntu 22.04

Etapa 1 - Atualizar pacotes do sistema

    sudo apt update

Etapa 2 - Criar um usuário do sistema para o Prometheus

    sudo groupadd --system prometheus
    sudo useradd -s /sbin/nologin --system -g prometheus prometheus

Etapa 3 - Crie diretórios para o Prometheus

    sudo mkdir /etc/prometheus
    sudo mkdir /var/lib/prometheus

Etapa 4 - Baixe o Prometheus e extraia os arquivos

    wget https://github.com/prometheus/prometheus/releases/download/v2.45.0/prometheus-2.45.0.linux-amd64.tar.gz

    tar vxf prometheus*.tar.gz

Etapa 5- Navegue até o diretório do Prometheus

    cd prometheus*/

Etapa 6 - Mova os arquivos binários e defina o proprietário

    sudo mv prometheus /usr/local/bin
    sudo mv promtool /usr/local/bin
    sudo chown prometheus:prometheus /usr/local/bin/prometheus
    sudo chown prometheus:prometheus /usr/local/bin/promtool
