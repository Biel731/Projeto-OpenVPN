# Integração de autenticação LDPA via RADIUS na VPN OpenVPN.

## ⚙️ Funcionalidade:

Agora, em vez de autenticarmos o usuário por certificados, faremos a autenticação via RADIUS em um servidor LDAP.
Ao executar o arquivo .ovpn, o cliente envia pacotes UDP para o endereço WAN do firewall (192.168.10.109) na porta 1194. Como há regras no firewall permitindo entradas UDP vindas da rede 10.10.10.0/24, o tráfego segue para a etapa de autenticação. Nesse momento, as chaves TLS são trocadas e os certificados (cliente e servidor) são validados.

Em seguida, o OpenVPN solicita as credenciais (usuário e senha cadastrados no LDAP). O cliente as digita e o OpenVPN encaminha um Access-Request no ip 127.0.0.1 (configurado em NAS/Client) ao plugin do FreeRADIUS na porta 1812 (configurada como backend de autenticação no servidor OpenVPN). O FreeRADIUS, por sua vez, realiza uma busca no LDAP em ldap://<IP_do_LDAP>:389 (não em LDAPS/636) de acordo com as definições em Services > FreeRADIUS > LDAP (Base DN, Bind DN, IP/hostname etc.).

Se o LDAP confirmar que o usuário e a senha são válidos, o FreeRADIUS retorna um Access-Accept ao OpenVPN, que finaliza o processo de autenticação (sem encerrar a troca TLS). Ao receber o Access-Accept, o OpenVPN conclui o handshake de dados e estabelece automaticamente o túnel VPN na faixa de IP configurada em VPN > OpenVPN > Servers. A partir daí, o cliente pode trafegar pela rede privada conforme as rotas e políticas definidas.

## ✅ Competências Adquiridas:

- Administração de Acesso Centralizado
  - Gerenciamento de autenticação de usuários via LDAP (usuários centralizados).
  - Controle de permissões e autenticação unificada.
- Integração de Serviços em Ambientes Híbridos
  - Conexão entre múltiplos sistemas (LDAP, RADIUS, OpenVPN).
  - Diagnóstico e resolução de falhas de autenticação entre serviços.
- Hardening de Serviços de Autenticação
  - Uso de secrets, autenticação mútua e restrições de client.
  - Prevenção de ataques como credenciais vazadas e autenticação indevida.
- Depuração de Logs e Monitoramento de Autenticação