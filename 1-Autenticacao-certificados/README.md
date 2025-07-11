# Projeto: Criar uma VPN OpenVPN com autenticação via certificados no firewall Pfsense CE 2.7.2.

## ⚙️ Funcionalidade:

O host externo (interface WAN) executará o arquivo .ovpn (configuração da VPN já contendo o cadastro do usuário), o que fará com que pacotes UDP sejam enviados pela porta 1194 (openvpn) ao firewall. Este, por sua vez, permitirá a entrada desses dados via UDP pela WAN, conforme previsto por uma regra de liberação desse protocolo.

Em seguida, será realizada a troca de chaves TLS entre o cliente e o servidor da VPN, estabelecendo uma “pré-conexão” entre as duas partes. Após isso, ocorrerá a validação do certificado do cliente pela autoridade certificadora (CA) e, logo depois, a autenticação das credenciais do usuário (nome de usuário e senha), cadastradas previamente no perfil do cliente no firewall.

Concluídas essas etapas de validação, será estabelecido um túnel VPN seguro e rápido (com criptografia e usando UDP) entre as duas pontas, sendo atribuído ao cliente o IP 10.10.10.X/24.

Com esse IP, e de acordo com as regras configuradas na interface do Firewall e do OpenVPN, o tráfego do cliente terá como destino as sub-redes (hosts) da interface LAN. Assim, o cliente poderá se conectar diretamente e realizar uma varredura (via Nmap) das portas abertas no Metasploitable 2, que está localizado atrás do firewall, no IP 192.168.1.101.

&nbsp;

## ✅ Competências Adquiridas com o projeto:

Esse projeto reuniu conceitos importantes de:

- Criptografia simétrica e assimétrica
- Infraestrutura de chave pública (PKI)
- Configuração segura de VPN com OpenVPN
- Controle de acesso via certificados
- Autenticação de Certificados.
- Regras de firewall para proteção da rede