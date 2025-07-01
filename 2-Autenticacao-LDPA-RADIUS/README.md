# Integração de autenticação LDPA via RADIUS na VPN OpenVPN.

## ⚙️ Funcionalidade:

Agora, em vez de autenticarmos o usuário por certificados, faremos a autenticação via RADIUS em um servidor LDAP.
Ao executar o arquivo .ovpn, o cliente envia pacotes UDP para o endereço WAN do firewall (192.168.10.109) na porta 1194. Como há regras no firewall permitindo entradas UDP vindas da rede 10.10.10.0/24, o tráfego segue para a etapa de autenticação. Nesse momento, as chaves TLS são trocadas e os certificados (cliente e servidor) são validados.

Em seguida, o OpenVPN solicita as credenciais (usuário e senha cadastrados no LDAP). O cliente as digita e o OpenVPN encaminha um Access-Request no ip 127.0.0.1 (configurado em NAS/Client) ao plugin do FreeRADIUS na porta 1812 (configurada como backend de autenticação no servidor OpenVPN). O FreeRADIUS, por sua vez, realiza uma busca no LDAP em ldap://<IP_do_LDAP>:389 (não em LDAPS/636) de acordo com as definições em Services > FreeRADIUS > LDAP (Base DN, Bind DN, IP/hostname etc.).

Se o LDAP confirmar que o usuário e a senha são válidos, o FreeRADIUS retorna um Access-Accept ao OpenVPN, que finaliza o processo de autenticação (sem encerrar a troca TLS). Ao receber o Access-Accept, o OpenVPN conclui o handshake de dados e estabelece automaticamente o túnel VPN na faixa de IP configurada em VPN > OpenVPN > Servers. A partir daí, o cliente pode trafegar pela rede privada conforme as rotas e políticas definidas.

&nbsp;

## 📍 Etapa 1: Instalando o Plugin FreeRADIUS.

Vá para Package Manager e instale o pacote FreeRADIUS:

![pacote-FreeRADIUS](images/pacote_freeRADIUS.png)

- **Observação:** As informações do DN e senha foram [configuradas na parte do Docker.](configuracoes/config-docker.md)

Visto isso, vamos acessar nosso LDAP por `https://<ip_do_ldap>:6443/` ou `https://localhost:6443/`.

![ldap-login](images/ldap.png)

&nbsp;

## Etapa 2: Configurando o LDAP.

Nosso LDAP está configurado assim. Vamos segui com as explicações sobre cada parte do nosso diretório.

![ldap-DN-completo](images/ldap_dn_completo.png)

### Explicação: 

- **DN (Distinguished Name):** É o endereço completo de um entry no diretório, ou seja o DN seria `cn=lucas luiz,ou=usersEnterprise,dc=minhaempresa,dc=local.` Cada parte antes da vírgula é um RDN.
- **RDNs (Relative Distinguished Names):** São as etiquetas que compõem o DN. No nosso caso, seria:
    - **dc=minhaempresa,** **dc=local:** “dc” vem de Domain Component. Define seu domínio LDAP(minhaempresa.local).
    - **ou=usersEnterprise:** “ou” significa Organizational Unit. É como se fosse uma pasta, onde você pode organizar seu LDAP da forma como queira. No nosso caso, é uma pasta onde vamos registrar todos os usuário que vão logar na vpn.
    - **“cn” significa Common Name**. Geralmente é o nome “amigável” ou “comum” do objeto (aqui, o nome do usuário).

### Visão geral dos tópicos:

| Atributo (RDN) | Significado | Exemplo no seu LDAP |
| --- | --- | --- |
| **dc** | Domain Component (parte do domínio) | `dc=minhaempresa,dc=local` |
| **ou** | Organizational Unit (unidade/pasta) | `ou=usersEnterprise` |
| **cn** | Common Name (nome comum do objeto) | `cn=lucas luiz` |
| **DN completo** | Distinguished Name (endereço completo) | `cn=lucas luiz,ou=usersEnterprise,dc=minhaempresa,dc=local` |

> **Observação:** Caso queira ver a configuração do LDAP (como foi constrído essa árvore), [clique aqui:](configuracoes/config-ldpa.md). Por aqui, vamos focar na construção do projeto (integração das ferramentas + explicação teórica).

&nbsp;

Em `System > User Manager > Authentication Server` clique em `Add` para criar um server de autenticação RADIUS. Preencha assim:

![server-radius](images/serverRadius.png)

| Tópicos | Valores |
| --- | --- |
| **Descriptive Name** | `Nome do Servidor RADIUS` |
| **Type** | `RADIUS` |
| **Protocolo** | `PAP`|
| **Shared Secret** | `Defina uma senha` |
| **Authentication Port** | `1812 (porta padrão do RADIUS) |

> **Observação:** Não perca essa senha. Ela serve para autenticação do FreeRADIUS e assinatura dos pacotes RADIUS. Essa senha será usada quando configurarmos o NAS/Client.

&nbsp;

> **Funcionalidade:** Esse configuração será o backend de autenticação do nosso servidor OpenVPN.