![Banner Dark Tech](https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExZ2Z0djBuZXhncm1jaHNpazVyN2k4eTVrdjJjZmI2bjBmdzlnM2owMiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/d3mn0OYWkFeegIa4/giphy.gif)

# 🛡️ Operation: Brute-Force Medusa // Metasploitable 3
> "A persistência é a chave para abrir portas que deveriam estar trancadas."

Este repositório documenta o desafio prático de simulação de ataques de força bruta utilizando a ferramenta **Medusa** contra um ambiente controlado (**Metasploitable 3**), com foco em auditoria de protocolos e validação de segurança.

---

## 🛠️ O Cenário de Ataque

O objetivo foi testar a resiliência do protocolo **FTP (ProFTPD 1.3.5)** contra tentativas de autenticação automatizadas.

* **Atacante:** Kali Linux (Medusa v2.3)
* **Alvo:** Metasploitable 3 (Ubuntu 14.04)
* **Protocolo:** FTP (Porta 21)
<img width="1584" height="386" alt="Captura de tela de 2026-05-15 17-40-38" src="https://github.com/user-attachments/assets/b10d1207-7d74-4388-bcda-dade17926e82" />

---

## ⚡ Execução do Protocolo

### 1. Preparação das Wordlists
Foram criadas wordlists personalizadas para otimizar o tempo de varredura:
- `users.txt`: Dicionário de usuários comuns.
- `pass.txt`: Lista de senhas prováveis.

<img width="832" height="326" alt="Captura de tela de 2026-05-15 17-38-28" src="https://github.com/user-attachments/assets/2dd1a6f7-68ce-4279-8b6a-8ea9146ea42e" />


### 2. O Ataque (Medusa)
O comando utilizado para iniciar a força bruta modular foi:

```bash
medusa -h 192.168.1.97 -u users.txt -P pass.txt -M ftp

![Uploading Captura de tela de 2026-05-15 17-40-38.png…]()
