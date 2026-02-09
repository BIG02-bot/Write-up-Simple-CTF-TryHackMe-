# 🛡️ Simple CTF — TryHackMe Write‑up

<p align="center">
  <img src="https://img.shields.io/badge/TryHackMe-Completed-red?style=for-the-badge&logo=tryhackme" />
  <img src="https://img.shields.io/badge/Category-Linux%20Privilege%20Escalation-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Difficulty-Easy-success?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Focus-Web%20Exploitation%20%7C%20SQLi-orange?style=for-the-badge" />
</p>

> ⚠️ Este write‑up possui fins **educacionais** e não contém spoilers de flags, preservando a integridade da plataforma TryHackMe.

---

## 🎯 Objetivo

Documentar o processo completo de exploração da máquina **Simple CTF**, seguindo a metodologia real de um teste de intrusão:

* Reconhecimento
* Enumeração
* Exploração
* Acesso inicial
* Escalada de privilégios

---

## 🧭 Metodologia de Ataque

Fluxo utilizado durante o pentest:

```
Recon → Enumeração → Exploração → Acesso inicial → Privilege Escalation → Root
```

---

## 1️⃣ Reconhecimento

Realizado **scan completo de portas** com Nmap:

```bash
nmap -sC -sV -p- <IP>
```

### Serviços identificados

* **FTP** — login anônimo habilitado
* **HTTP** — servidor Apache
* **SSH** — executando em porta não padrão (>1000)

---

## 2️⃣ Enumeração Web

Enumeração de diretórios com Gobuster:

```bash
gobuster dir -u http://<IP> -w /usr/share/wordlists/dirb/common.txt
```

Foi identificado um **subdiretório contendo um CMS vulnerável**.

---

## 3️⃣ Identificação da Vulnerabilidade

O CMS identificado foi o **CMS Made Simple**, vulnerável a:

* **SQL Injection**
* **CVE‑2019‑9053**

Exploit público obtido via **Exploit‑DB**.

---

## 4️⃣ Exploração

A execução do exploit de SQL Injection permitiu:

* Extração de **usuário**
* Extração de **hash de senha**

Posteriormente, a senha em texto claro foi obtida e reutilizada para acesso ao sistema.

---

## 5️⃣ Acesso Inicial

Login realizado via **SSH** utilizando as credenciais obtidas.

Após o acesso:

```bash
cat user.txt
```

Confirmação da **user flag**.

---

## 6️⃣ Escalada de Privilégios

Enumeração de privilégios com:

```bash
sudo -l
```

Identificado binário executável como **root sem necessidade de senha**:

* **vim**

Uso da técnica **GTFOBins** para obtenção de shell privilegiado:

```bash
sudo vim -c ':!/bin/bash'
```

Confirmação de privilégio:

```bash
whoami
```

Leitura da **root flag**.

---

## 🧠 Aprendizados

Esta máquina cobre o fluxo completo de um **pentest Linux básico**:

* Reconhecimento de serviços
* Enumeração web
* Exploração por SQL Injection
* Acesso inicial via SSH
* Escalada de privilégios com GTFOBins

---

## 🚀 Próximos Passos

Para evolução em segurança ofensiva:

* Realizar máquinas **Intermediate** no TryHackMe
* Iniciar trilha **Hack The Box**
* Estudar **Linux Privilege Escalation** em profundidade

---

## 👨‍💻 Autor

**Mateus Papaes**
Cybersecurity • Pentest 

<p align="center">
  <sub>Write‑up educacional — sem divulgação de flags.</sub>
</p>


