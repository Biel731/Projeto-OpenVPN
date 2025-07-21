# Integração com Wazuh para simulação de endpoint com FIM, Active Response e DLP

## ⚙️ Funcionalidade:
Neste projeto, integramos o Wazuh como solução de monitoramento de endpoints, simulando um sistema real de proteção e resposta a incidentes.

O objetivo foi monitorar a integridade de arquivos sensíveis (FIM - File Integrity Monitoring) e aplicar medidas automatizadas de contenção (Active Response) em caso de alterações suspeitas. Quando um arquivo protegido é editado, o Wazuh dispara um alerta e executa um script de bloqueio de IP via iptables, prevenindo possíveis ações maliciosas ou vazamentos de dados.

Essa automação simula a função de um DLP (Data Loss Prevention) ao impedir a continuidade de ações após a modificação de arquivos sensíveis, como documentos internos ou diretórios críticos. Toda a resposta ocorre diretamente no endpoint, reforçando o conceito de proteção distribuída e ativa.

 
## ✅ Competências Adquiridas:

Esse projeto explorou conceitos fundamentais de:

- Monitoramento de integridade de arquivos em tempo real (FIM).
- Criação e customização de respostas automatizadas a eventos (Active Response).
- Simulação de políticas de prevenção à perda de dados (DLP).
- Integração de agentes Wazuh em ambientes de rede segmentados (Vlan).
- Uso de regras do Wazuh para detectar e responder a comportamentos anômalos no endpoint.
- Aplicação prática de medidas defensivas com iptables.