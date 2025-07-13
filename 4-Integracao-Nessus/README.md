# Integração com Nessus para análise de vulnerabilidade na rede LAN.

## 🛡️ Funcionalidade:
Neste projeto, integramos o scanner de vulnerabilidades Nessus ao ambiente de rede acessado via VPN. O objetivo é identificar falhas de segurança de forma segura e eficiente, sem impactar os serviços ativos no ambiente.

Após autenticação e recebimento do IP da faixa 10.10.10.0/24, o Nessus é configurado para escanear toda a rede interna 192.168.1.0/24. Ativamos a descoberta de hosts via ping, utilizando métodos como TCP, ARP e ICMP — excetuando o UDP para evitar falsos alertas e interferências em serviços sensíveis como o Splunk e o OpenVPN.

Durante o escaneamento de portas, utilizamos os métodos TCP connect e TCP SYN, garantindo precisão sem comprometer o tempo de execução. Também ativamos a verificação de malwares, direcionada a diretórios padrão de sistemas Windows e Linux.

Por fim, os relatórios gerados destacam os hosts ativos (que responderam ao ping), permitindo melhor visibilidade da superfície de ataque da rede.

&nbsp;

## ✅ Competências Adquiridas:

Esse projeto reuniu conceitos importantes de:

- Configuração de um scanner de vulnerabilidades (Nessus) em ambiente corporativo.
- Definição segura de escopos e métodos de varredura para evitar impactos operacionais.
- Otimização de escaneamentos (evitando UDP, escolhendo métodos eficientes).
- Análise de ativos visíveis na rede e sua exposição a riscos.
- Interpretação de relatórios de vulnerabilidade e identificação de potenciais ameaças.
- Aplicação de boas práticas em varredura de redes protegidas por VPN.