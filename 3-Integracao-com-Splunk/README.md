# Integração com SIEM Splunk para análise de logs.

## ⚙️ Funcionalidade:

Neste projeto, o Splunk foi instalado em uma máquina Kali Linux com o objetivo de centralizar e visualizar logs de segurança de forma prática. O foco principal é monitorar eventos relacionados ao ambiente VPN com autenticação via OpenVPN + RADIUS + LDAP, já previamente configurado.

O Splunk atua como um SIEM leve e visual. Após a instalação, configuramos uma entrada de dados via UDP na porta 514, permitindo o recebimento de logs de firewall, tentativas de autenticação e falhas diversas. O pfSense foi configurado para enviar seus logs via syslog diretamente para o IP da máquina Kali, onde o Splunk está escutando.

Assim, toda a movimentação da rede — incluindo tentativas de conexão VPN, autenticações válidas ou negadas pelo FreeRADIUS, e mensagens geradas pelo LDAP — pode ser monitorada em tempo real. Além disso, o Splunk permite aplicar filtros e criar dashboards com base nos dados recebidos, facilitando a análise forense ou a detecção de comportamentos anômalos no ambiente.


## ✅ Competências Adquiridas:

✅ Competências Adquiridas com o projeto:

Esse projeto reuniu conceitos importantes de:

- Instalação de uma solução SIEM.
- Coleta e centralização de logs de segurança em tempo real.
- Integração de dispositivos de rede (como pfSense) com ferramentas de monitoramento.
- Análise e identificação de eventos suspeitos a partir de logs.
- Gerenciamento de logs de autenticação e falhas de acesso
- Noções de segurança operacional e visibilidade em redes corporativas