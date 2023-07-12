# Instalar asdf (obs.: bash + git)

01. Passo: Acessar 
    url: https://asdf-vm.com/pt-br/guide/getting-started.html

    01.1. Instalando as dependências
   
         sudo apt install curl git
    
    01.2. Realizar o download do asdf

        git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.12.0

    01.3. Adicionando ao shell

        Bash & Git:
        - Adicione esta linha no: ~/.bashrc
            - "$HOME/.asdf/asdf.sh"
        - Auto complete é configurado manualmente adicionando a linha ao .bashrc:
            - "$HOME/.asdf/completions/asdf.bash"

02. Instalando um plugin

Instalar os plugins asdf

	- kubectl : https://github.com/asdf-community/asdf-kubectl

        asdf plugin-add kubectl https://github.com/asdf-community/asdf-kubectl.git
	
    - terraform
    asdf plugin list
    
    https://github.com/asdf-community/asdf-hashicorp

        asdf plugin-add boundary https://github.com/asdf-community/asdf-hashicorp.git
        asdf plugin-add consul https://github.com/asdf-community/asdf-hashicorp.git
        asdf plugin-add levant https://github.com/asdf-community/asdf-hashicorp.git
        asdf plugin-add nomad https://github.com/asdf-community/asdf-hashicorp.git
        asdf plugin-add packer https://github.com/asdf-community/asdf-hashicorp.git
        asdf plugin-add sentinel https://github.com/asdf-community/asdf-hashicorp.git
        asdf plugin-add serf https://github.com/asdf-community/asdf-hashicorp.git
        asdf plugin-add terraform https://github.com/asdf-community/asdf-hashicorp.git
        asdf plugin-add terraform-ls https://github.com/asdf-community/asdf-hashicorp.git
        asdf plugin-add tfc-agent https://github.com/asdf-community/asdf-hashicorp.git
        asdf plugin-add vault https://github.com/asdf-community/asdf-hashicorp.git
        asdf plugin-add waypoint https://github.com/asdf-community/asdf-hashicorp.git

03. Install Docker Engine on Ubuntu
    - Instalar dokcer (usa containerd)

https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

Etapa 1: Configurar o repositório: Atualize o aptíndice do pacote e instale os pacotes para permitir apto uso de um repositório por HTTPS:

    sudo apt-get update
    sudo apt-get install ca-certificates curl gnupg

Etapa 2: Adicione a chave GPG oficial do Docker:

     sudo install -m 0755 -d /etc/apt/keyrings
     curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
     sudo chmod a+r /etc/apt/keyrings/docker.gpg

Etapa 3: Use o seguinte comando para configurar o repositório:

     echo \
    "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
    "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

Etapa 4: Instalar Docker Engine: Atualize o aptíndice do pacote:

     sudo apt-get update

Instale o Docker Engine, o containerd e o Docker Compose.

Etapa 5: Para instalar a versão mais recente, execute:

    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

Etapa 6: Verifique se a instalação do Docker Engine foi bem-sucedida executando a hello-worldimagem.

    sudo docker run hello-world

Este comando baixa uma imagem de teste e a executa em um contêiner. Quando o contêiner é executado, ele imprime uma mensagem de confirmação e sai.

Agora você instalou e iniciou o Docker Engine com sucesso.


# INSTALAR O GOLANG NO UBUNTU

- Instalar golang

Etapa 1: Abra o terminal e atualize o sistema operacional:

    sudo apt update
    sudo apt upgrade -y

Etapa 2: Agora, execute a instalação do Golang no Ubuntu, utilizando o apt.

    sudo apt install golang-go

Etapa 3: Para testar a instalação no Ubuntu e verificar a versão do Go instalada, utilize:

     go version


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
https://prometheus.io/docs/prometheus/2.45/getting_started/
https://www.cherryservers.com/blog/install-prometheus-ubuntu#step-4---start-prometheus-service

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

Etapa 7 - Mova os arquivos de configuração e defina o proprietário

    sudo mv consoles /etc/prometheus
    sudo mv console_libraries /etc/prometheus
    sudo mv prometheus.yml /etc/prometheus
    sudo chown prometheus:prometheus /etc/prometheus
    sudo chown -R prometheus:prometheus /etc/prometheus/consoles
    sudo chown -R prometheus:prometheus /etc/prometheus/console_libraries
    sudo chown -R prometheus:prometheus /var/lib/prometheus

    sudo nano /etc/prometheus/prometheus.yml

Etapa 8 - Criar o serviço Prometheus Systemd

    sudo nano /etc/systemd/system/prometheus.service

Inclua essas configurações no arquivo, salve e saia:

[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target

Etapa 9 - Recarregue o Systemd

    sudo systemctl daemon-reload

Etapa 10 - Inicie o serviço Prometheus

    sudo systemctl enable prometheus
    sudo systemctl start prometheus

Etapa 11- Verifique o status do Prometheus

    sudo systemctl status prometheus

Etapa 12 - Com o Prometheus rodando com sucesso, você pode acessá-lo através do seu navegador web usando localhost:9090 ou <ip_address>:9090

# Instale o Grafana no Debian Ubuntu

Conclua as etapas a seguir para instalar o Grafana a partir do repositório APT:

Para instalar os pacotes necessários e baixar a chave de assinatura do repositório Grafana, execute os seguintes comandos:

sudo apt-get install -y apt-transport-https
sudo apt-get install -y software-properties-common wget
sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key

Para adicionar um repositório para lançamentos estáveis, execute o seguinte comando:

echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

Para adicionar um repositório para versões beta, execute o seguinte comando:

echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com beta main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

Execute o seguinte comando para atualizar a lista de pacotes disponíveis:

# Updates the list of available packages
sudo apt-get update

Para instalar o Grafana OSS, execute o seguinte comando:

# Installs the latest OSS release:
sudo apt-get install grafana

Para instalar o Grafana Enterprise, execute o seguinte comando:

# Installs the latest Enterprise release:
sudo apt-get install grafana-enterprise
