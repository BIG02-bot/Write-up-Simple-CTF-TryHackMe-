# Write-up-Simple-CTF-TryHackMe-

⚠️ Este write-up tem fins educacionais e não contém spoilers de flags para preservar a integridade da plataforma.

![Uploading image.png…]()


🎯 Objetivo

Documentar o processo completo de exploração da máquina Simple CTF seguindo a metodologia real de pentest:

Reconhecimento

Enumeração

Exploração

Acesso inicial

Escalada de privilégios

1️⃣ Reconhecimento

Realizado scan completo de portas com Nmap:

nmap -sC -sV -p- <IP>
Serviços identificados

FTP — login anônimo habilitado

HTTP — servidor Apache

SSH — porta não padrão (acima de 1000)

2️⃣ Enumeração Web

Enumeração de diretórios com Gobuster:

gobuster dir -u http://<IP> -w /usr/share/wordlists/dirb/common.txt

Descoberto subdiretório relevante contendo um CMS vulnerável.

3️⃣ Identificação da Vulnerabilidade

O CMS identificado foi CMS Made Simple vulnerável a:

SQL Injection

Referência: CVE-2019-9053

Exploit público utilizado via Exploit‑DB.

4️⃣ Exploração

Execução do exploit de SQL Injection permitiu:

Extração de usuário

Extração de hash de senha

Posteriormente foi possível obter a senha em texto claro e reutilizá‑la para acesso ao sistema.

5️⃣ Acesso Inicial

Login realizado via SSH com as credenciais obtidas.

Após acesso:

cat user.txt

Confirmação da user flag.

6️⃣ Escalada de Privilégios

Enumeração de privilégios com:

sudo -l

Identificado binário executável como root sem senha:

vim

Uso de técnica GTFOBins para spawn de shell privilegiado:

sudo vim -c ':!/bin/bash'

Confirmação de privilégio:

whoami

Leitura da root flag.

🧠 Aprendizados

Esta máquina cobre o fluxo completo de um pentest Linux básico:

Reconhecimento de serviços

Enumeração web

Exploração por SQL Injection

Acesso inicial via SSH

Escalada de privilégios com GTFOBins
