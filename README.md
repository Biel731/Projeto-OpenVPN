# 🛡️ Projeto OpenVPN com Autenticação Centralizada e Monitoramento

## 📌 Objetivo
Simular um ambiente corporativo seguro com autenticação centralizada via LDAP + RADIUS para acesso VPN (OpenVPN), e monitoramento de logs via Splunk.

## 🧩 Arquitetura

 [Usuário-VPN]
      │
      ▼
[OpenVPN-Server]
      │
      ▼
[FreeRADIUS]
      │
      ▼
  [OpenLDAP]
      │
      ▼
  [Splunk]

&nbsp;

## 📁 Estrutura do Projeto
| Pasta	| Descrição | 
| --- | --- |
| `1-Autenticacao-certificados` | Configuração inicial do OpenVPN com autenticação via certificados TLS. |
| `2-Autenticacao-LDPA-RADIUS` | Integração do OpenVPN com FreeRADIUS + OpenLDAP. |
| `3-Integracao-com-Splunk` | Configuração do Splunk para coleta e visualização dos logs de autenticação. |
| `4-Integracao-com-Nessus` | Integração com Nessus para análise de vulnerabilidades. |

&nbsp;

## 🚧 Status do Projeto
✅ Funcional nas VMs locais <br>
❌ Ainda não dockerizado (documentado para execução manual)

&nbsp;

## 📷 Prints da Funcionalidade:

### Conexão com a VPN e IP atribuído.
![config-vpn](4-Integracao-Nessus/sources/conf-vpn.gif)

### Logs OpenVPN e Radiusd no Splunk
![splunk](4-Integracao-Nessus/sources/splunk.gif)

### Analise de Vulnerabilidade com Nessus.
![nessus](4-Integracao-Nessus/sources/config-nessus.gif)

&nbsp;

## 📜 Como rodar (manual)
- Escolha um software de virtualização que você preferir.
- Instale a imgem do PfSense CE - [link](https://www.pfsense.org/download/)
- Instale o OpenVPN (Windows) - [link](https://openvpn.net/client/)
- Instale o Nessus - [link](https://www.tenable.com/downloads/nessus?loginAttempted=true)

&nbsp;

## 📚 O que aprendi
Estrutura de autenticação real com OpenVPN + RADIUS + LDAP

- Leitura e correção de erros do FreeRADIUS
- Encaminhamento e visualização de logs no Splunk
- Prática com logs, autenticação, integração de serviços e simulação de ambiente real

&nbsp;

## 💪🏻 Desafios enfrentados:
- Comunicação entre RADIUS e LDAP com `radtest`
- Comunicação entre OpenVPN e o plugin FreeRadius
- Regras OpenVPN para acesso do cliente aos hosts da LAN
- Estruração do LDAP