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
                                sudo apt update
                                sudo apt upgrade
        04. Realizar a instalação do nod exporter
                4.1. link procedimento: https://www.cherryservers.com/blog/install-prometheus-ubuntu
                4.2. Liberar a port 9300

        05. Painel Prometeus
        http://192.168.100.250:9090/graph?g0.expr=&g0.tab=1&g0.stacked=0&g0.show_exemplars=0&g0.range_input=1h


Aprendizado: 
        01. Instalação do sistema operacional ubuntu 22.04 lts
        02. Execuçao dos comandos Linux(Pacotes, SystemD)
        03. Instalação do Prometheus(exporters).
        04. Liberação da porta 9300
Tutorial de Instalação ubuntu: https://www.youtube.com/watch?v=3XkHSi0qCkc&t=3s
