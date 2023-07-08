poc001- Instalação de um servido Ubuntu Server (última)LST + Instalação e configuração do Node Exporter na máquina via Service
poc001- Instalação de um servido Ubuntu Server (última)LST
        - Atualiza os pacotes, update/upgrade
        - Instalação e configuração do Node Exporter PORTA 9300 na máquina via Service(systemctl)
        - Linux(Pacotes, SystemD), Prometheus(exporters)

        Passos:

        01. Realizar a instalação da virtualbox ou vmware; >>> ok.
        02. Fazer o downloads da iso referente ao sistema operacional ubuntu 22.04 lts >>> ok.
        url: https://ubuntu.com/download/server
        03. configurar uma maquina VM e realizar a instalação do ubuntu-22.04.2-live-server-amd64.iso >>> ok.
                03.1. Atualizar os pacotes update/upgrade.                
                        Comandos:
                                sudo apt update >>> ok.
                                sudo apt upgrade >>> ok.
        04. Realizar a instalação do node exporter
        
                4.1. lista de comando para instalação do prometheus/node exporter
                        4.1.1. Baixe o Node Exporter
                                wget https://github.com/prometheus/node_exporter/releases/download/v1.6.0/node_exporter-1.6.0.linux-amd64.tar.gz
                                
                        4.1.2. Extraia o Node Exporter e mova o binário
                                exxtrair: tar xvf node_exporter-1.6.0.linux-amd64.tar.gz
                                alternar diretorio: cd node_exporter-1.6.0.linux-amd64
                                copiar: sudo cp node_exporter /usr/local/bin
                                remover: # Exit current directory
                                        cd ..
                                        # Remove the extracted directory
                                        rm -rf ./node_exporter-1.3.1.linux-amd64
                                        
                        4.1.3. Criar usuário do exportador de nós
                                sudo useradd --no-create-home --shell /bin/false node_exporter
                                
                                Defina o proprietário do binário node_exporterpara o usuário criado recentemente:
                                
                                sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter

                        4.1.4. Crie e inicie o serviço Node Exporter
                        Crie o node_exporter.servicearquivo com o nano:
                                sudo nano /etc/systemd/system/node_exporter.service
                        E cole o seguinte conteúdo no arquivo:

                                [Unit]
                                Description=Node Exporter
                                Wants=network-online.target
                                After=network-online.target

                                [Service]
                                User=node_exporter
                                Group=node_exporter
                                Type=simple
                                ExecStart=/usr/local/bin/node_exporter

                                [Install]
                                WantedBy=multi-user.target
                                
                        Recarregar o daemon com:

                                sudo systemctl daemon-reload

                        inicie o node_exporterserviço com o seguinte comando:

                                sudo systemctl start node_exporter
                                systemctl restart node_exporter
                                systemctl enable node_exporter

                        4.1.5. Teste o serviço Node Exporter

                                url: http://192.168.100.253:9300/metrics

                        Se a porta 9100 estiver inacessível
                       
                                sudo ufw allow 9100

                        Iptables

                                sudo iptables -I INPUT -p tcp -m tcp --dport 9100 -j ACCEPT
                                
                4.2. Liberar a port 9300
                        4.2.1. Configurar o serviço para Node_Exporter (porta)
                                sudo vim /etc/systemd/system/node_exporter.service
                                ExecStart=/usr/local/bin/node_exporter --web.listen-address=:9300
                                Salvar (wq!)
                                sudo systemctl daemon-reload
                                systemctl restart node_exporter
                                curl http://92.168.100.253:9300/metrics

Aprendizado: 
        01. Instalação do sistema operacional ubuntu 22.04 lts
        02. Execuçao dos comandos Linux(Pacotes, SystemD)                
        03. Instalação do Prometheus(exporters).
        04. Liberação da porta 9300
Tutorial de Instalação ubuntu: https://www.youtube.com/watch?v=3XkHSi0qCkc&t=3s
