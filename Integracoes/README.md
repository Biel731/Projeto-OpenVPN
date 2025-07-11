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


## 📁 Estrutura do Projeto
| Pasta	| Descrição | 
| --- | --- |
| `1-Autenticacao-certificados` | Configuração inicial do OpenVPN com autenticação via certificados TLS. |
| `2-Autenticacao-LDPA-RADIUS` | Integração do OpenVPN com FreeRADIUS + OpenLDAP. |
| `3-Integracao-com-Splunk` | Configuração do Splunk para coleta e visualização dos logs de autenticação. |


## 🚧 Status do Projeto
✅ Funcional nas VMs locais
❌ Ainda não dockerizado (documentado para execução manual)


## 📷 Prints (recomendo adicionar aqui)
Tela do OpenVPN funcionando

Resultado do log no Splunk

Linha de comando mostrando sucesso da autenticação


## 📜 Como rodar (manual)
Adicione os passos básicos ou um link para o docs/setup.md com os comandos das etapas.


## 📚 O que aprendi
Estrutura de autenticação real com OpenVPN + RADIUS + LDAP

Leitura e correção de erros do FreeRADIUS
Encaminhamento e visualização de logs no Splunk
Prática com logs, autenticação, integração de serviços e simulação de ambiente real