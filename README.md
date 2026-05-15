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
```


<img width="1584" height="386" alt="Captura de tela de 2026-05-15 17-40-38" src="https://github.com/user-attachments/assets/1691d092-f9d0-45e2-83de-142cbe38e098" />


Resultados da Operação
A engine identificou a credencial vulnerável em poucos segundos de execução:

HOST: 192.168.1.97,

USER: vagrant,

PASS: vagrant,

STATUS: [SUCCESS]

---

<img width="1129" height="319" alt="Captura de tela de 2026-05-15 17-42-53" src="https://github.com/user-attachments/assets/5706beb6-7c27-4e6b-949f-03d90ad10d1f" />


## 🛑 Protocolos de Hardening (Medidas de Defesa)
> "A melhor defesa é uma arquitetura que não oferece confiança a ninguém."

Para mitigar a eficácia de ataques como a **Operation-BruteForce**, as seguintes camadas de segurança devem ser implementadas no servidor alvo:

### 1. Camadas de Proteção Ativa
| Defesa | Implementação Técnica | Objetivo |
| :--- | :--- | :--- |
| **Intrusion Prevention** | Instalação e configuração do **Fail2Ban** para monitorar logs do serviço FTP. | Banir automaticamente o IP do atacante após 3 tentativas falhas. |
| **Identity Management** | Implementação de **MFA (2FA)** via módulos PAM. | Tornar a senha insuficiente para o acesso, exigindo um token temporário. |
| **Access Control** | Edição do arquivo `/etc/proftpd/proftpd.conf` para desabilitar o login de `root`. | Impedir que contas administrativas sejam alvos de força bruta direta. |

### 2. Fortalecimento de Infraestrutura
* **Substituição de Senhas por Chaves:** Desabilitar a autenticação por senha e permitir apenas chaves SSH/RSA de no mínimo **4096 bits**.
* **Port Knocking:** Configurar o firewall para manter a porta 21 oculta, abrindo-a apenas após uma "batida" específica em outras portas pré-definidas.
* **Monitoramento de Logs:** Centralizar logs em um servidor externo para identificar padrões de varredura (Reconnaissance) antes mesmo do ataque começar.

---
**Status da Operação:** Concluída com sucesso.  
**Recomendação:** Aplicar Hardening imediato no ambiente Metasploitable 3.
