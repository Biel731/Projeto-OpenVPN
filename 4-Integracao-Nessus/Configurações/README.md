# 🧰 Passo a Passo: Instalação do Nessus no Kali Linux (via site oficial).

## 🔹 1. Acesse o site oficial da Tenable
Abra o navegador no Kali e vá para:
🔗 ![acesse aqui](https://www.tenable.com/downloads/nessus)

&nbsp;

## 🔹 2. Escolha a versão para Linux
Na seção “Nessus”, role até encontrar “Linux”.

Selecione o pacote correspondente à sua arquitetura: No nosso caso vamos escolher o .deb para a nossa vm kali.
Clique em “Download”.

`⚠️ Pode ser necessário criar uma conta gratuita na Tenable para obter o link direto de download.`

&nbsp;

## 🔹 3. Instale o pacote .deb
Após o download, navegue até a pasta onde o arquivo foi salvo e instale:

`sudo dpkg -i Nessus-<versao>-debian6_amd64.deb`
(Use TAB para autocompletar o nome do arquivo.)

Se houver dependências pendentes:
`sudo apt --fix-broken install`

&nbsp;

## 🔹 4. Inicie o serviço do Nessus
Após a instalação:

`sudo systemctl start nessusd`
Verifique se está rodando:
`sudo systemctl status nessusd`

&nbsp;

## 🔹 5. Acesse a interface web
Abra o navegador e acesse:
https://localhost:8834

&nbsp;

## 🔹 6. Faça a configuração inicial
- Escolha o tipo de instalação: Nessus Essentials (grátis com registro)
- Crie uma conta de usuário
- Insira o código de ativação (enviado por e-mail após registro)
- Aguarde o download e o carregamento dos plugins (leva alguns minutos)

✅ Pronto!
Após isso, o Nessus estará instalado e pronto para realizar varreduras de vulnerabilidade no seu ambiente.