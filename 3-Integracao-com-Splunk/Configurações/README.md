# 🛠️ Passo a Passo: Instalação do Splunk no Kali + Integração com pfSense.

## ✅ 1. Baixar o Splunk para Linux (arquivo .deb).

![Acesse o site oficial:](https://www.splunk.com/en_us/download/splunk-enterprise.html)

Escolha a opção .deb (64-bit) para Debian/Ubuntu.

> Crie uma conta, se necessário.

Copie o link do download direto.
No terminal do Kali:

`wget -O splunk.deb "LINK_DO_ARQUIVO"`


## ✅ 2. Instalar o Splunk.

sudo dpkg -i splunk.deb

Corrija dependências, se necessário:
sudo apt --fix-broken install


## ✅ 3. Iniciar o Splunk pela primeira vez.

sudo /opt/splunk/bin/splunk start --accept-license
Será solicitado criar um usuário e senha para o Splunk Web.

Para os próximos usos:
sudo /opt/splunk/bin/splunk start

Para ativar na inicialização do sistema:
sudo /opt/splunk/bin/splunk enable boot-start


## ✅ 4. Acessar a interface web.

Abra o navegador e acesse:
http://localhost:8000


## ✅ 5. Criar uma entrada de dados (inputs) para logs do pfSense.

No Splunk Web:

`Vá em Settings > Data Inputs`

Clique em UDP e faça:

- Adicione a porta 514
- Escolha um sourcetype genérico como syslog
- Defina um índice (ex: main) ou use default
- Finalize e habilite a entrada
  

## ✅ 6. Configurar o pfSense para enviar logs ao Splunk.

No pfSense:

- Vá em `Status > System Logs > Settings`
- Em Remote Logging Options, ative a opção de log remoto
- No campo `Remote Syslog Servers,` coloque o `IP da máquina Kali + porta 514`, por exemplo: 192.168.1.50:514.

Marque as categorias de log que deseja enviar (firewall, VPN, auth, etc.) ou "everything" para pegar todos os logs e salve.


## ✅ 7. Verificar se os logs estão chegando.

No Splunk Web:

- Vá em Search & Reporting e pesquise pelo índice: `index=main` ou `sourcetype=syslog`.

Você verá os eventos enviados pelo pfSense.