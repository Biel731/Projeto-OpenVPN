# Projeto: Criar uma VPN com OpenVPN no firewall Pfsense CE 2.7.2.


## Funcionalidade:

O host externo (interface WAN) executará o arquivo .ovpn (configuração da VPN já contendo o cadastro do usuário), o que fará com que pacotes UDP sejam enviados pela porta 1194 (openvpn) ao firewall. Este, por sua vez, permitirá a entrada desses dados via UDP pela WAN, conforme previsto por uma regra de liberação desse protocolo.

Em seguida, será realizada a troca de chaves TLS entre o cliente e o servidor da VPN, estabelecendo uma “pré-conexão” entre as duas partes. Após isso, ocorrerá a validação do certificado do cliente pela autoridade certificadora (CA) e, logo depois, a autenticação das credenciais do usuário (nome de usuário e senha), cadastradas previamente no perfil do cliente no firewall.

Concluídas essas etapas de validação, será estabelecido um túnel VPN seguro e rápido (com criptografia e usando UDP) entre as duas pontas, sendo atribuído ao cliente o IP 10.10.10.X/24.

Com esse IP, e de acordo com as regras configuradas na interface do Firewall e do OpenVPN, o tráfego do cliente terá como destino as sub-redes (hosts) da interface LAN. Assim, o cliente poderá se conectar diretamente e realizar uma varredura (via Nmap) das portas abertas no Metasploitable 2, que está localizado atrás do firewall, no IP 192.168.1.101.
<br>  
<br>
## 📍 Etapa 1: Criando a Autoridade Certificadora (CA) e Certificados Digitais

### 1.1 Entendendo o papel da CA

A **Autoridade Certificadora (CA)** é o órgão central que emite certificados digitais para autenticar identidades na rede. Ela atua como uma "terceira parte confiável", validando que os certificados entregues são legítimos.

Em uma infraestrutura de VPN, a CA cria e assina:

- O certificado do **servidor VPN** (que confirma a identidade do servidor)
- O certificado de cada **cliente VPN** (que autentica cada usuário/host)

Esta assinatura garante que só certificados emitidos pela CA são aceitos, prevenindo conexões não autorizadas.

### 1.2 Criando a CA no pfSense

No pfSense, acesse:

`VPN > OpenVPN > Wizards`

O assistente vai guiar a criação da CA. É fundamental preencher corretamente os dados da CA, como nome, validade, etc. A CA será usada para emitir os certificados seguintes.

### 1.3 Criando o certificado do servidor

No mesmo assistente, você deve criar o certificado do servidor VPN:

- **Server Certificate:** selecione a CA criada para garantir que o certificado seja assinado e validado.
    
![image.png](images/image_1.3.png)
<br>

- **Criptografia:** configuramos o servidor para usar AES-256 com SHA-256.

> Observação: Por que AES-256 e SHA-256?

- **AES (Advanced Encryption Standard) 256 bits**: padrão de criptografia simétrica altamente seguro usado mundialmente, que cifra os dados para manter confidencialidade.
- **SHA-256 (Secure Hash Algorithm 256 bits):** algoritmo de hash que garante a integridade dos dados, detectando qualquer alteração durante o trânsito.

> Continuando com as configurações...
- **IPv4 Tunnel Network:** é a faixa de IP que será atribuída aos clientes VPN ao se conectarem. Escolhi 10.10.10.0/24, uma rede privada dedicada para o túnel VPN, garantindo que não haja conflito com redes existentes.
- **Redirect Gateway:** ao habilitar essa opção, todo o tráfego do cliente é roteado pela VPN. Isso significa que, além do acesso à rede interna, o cliente passa a ter todo seu tráfego de internet encapsulado na VPN, aumentando a privacidade.
[redirectGateway.png](images/redirectGateway.png)

<br>

- **Use TLS Key:** TLS (Transport Layer Security) é o protocolo responsável por criar um canal seguro antes mesmo da autenticação. O uso de uma chave TLS estática evita ataques como DoS e replay.
    - Obs.: Vale ressaltar que a Autoridade Certificadora que você criou deve validar o certificado que você está criando, como é mostrado nos últimos campos da imagem.