# Blue Team — Deteções Wazuh em Tempo Real

![Categoria](https://img.shields.io/badge/categoria-Blue%20Team-blue?style=flat-square)
![Ferramenta](https://img.shields.io/badge/SIEM-Wazuh-blue?style=flat-square)
![Agente](https://img.shields.io/badge/agente-kali--attacker-red?style=flat-square)

## Objetivo

Demonstrar como o Wazuh deteta em tempo real atividades suspeitas
realizadas no Kali Linux — o lado Blue Team do lab.

## Atividades Realizadas e Alertas Gerados

### 1. Scan de Rede com Nmap
```bash
sudo nmap -sV 10.0.2.4
```

**Alerta gerado:**
- `data.command: /usr/bin/nmap -sV 10.0.2.4`
- `Successful sudo to ROOT executed`
- Severidade: **Low**

O Wazuh registou o comando exato, os argumentos, e que foi
executado com sudo. Um analista SOC vendo este alerta saberia
imediatamente que alguém estava a fazer reconhecimento de rede.

---

### 2. Acesso ao Ficheiro de Passwords
```bash
sudo cat /etc/shadow
```

**Alerta gerado:**
- Acesso a ficheiro sensível `/etc/shadow`
- Severidade: **Low**

O `/etc/shadow` contém os hashes das passwords de todos os
utilizadores. O Wazuh monitoriza acessos a ficheiros críticos
do sistema através do File Integrity Monitoring (FIM).

---

### 3. Criação de Utilizador (Persistência)
```bash
sudo useradd -m teste123
sudo passwd teste123
```

**Alertas gerados:**
- `data.command: /usr/sbin/useradd -m teste123`
- `data.command: /usr/bin/passwd teste123`
- Técnica MITRE: **T1136 - Create Account (Persistence)**
- Severidade: **Low**

Criar um utilizador novo é uma técnica clássica de persistência —
mesmo que a vulnerabilidade original seja corrigida, o utilizador
continua a existir. O Wazuh classificou isto automaticamente como
Persistência no framework MITRE ATT&CK.

---

### 4. Escalada de Privilégios
```bash
sudo su
```

**Alertas gerados:**
- Técnica MITRE: **T1548.003 - Sudo and Sudo Caching**
- Técnica MITRE: **T1078 - Valid Accounts**
- Severidade: **Medium**

O uso de sudo para escalar para root foi automaticamente
classificado como Privilege Escalation pelo Wazuh.

---

## Resumo de Alertas

| Atividade | Alertas | Severidade | Técnica MITRE |
|---|---|---|---|
| Scan Nmap | 3 | Low | Discovery |
| Acesso /etc/shadow | 3 | Low | Credential Access |
| Criar utilizador | 3 | Low | Persistence |
| Escalada sudo | 3 | Medium | Privilege Escalation |

**Total gerado:** 129 alertas (incluindo Security Configuration Assessment)

## Conclusão Purple Team

O mesmo lab que usámos para atacar (Red Team) foi usado para
detetar esses ataques (Blue Team). Ver os próprios ataques
classificados pelo MITRE ATT&CK em tempo real é a essência
do Purple Team — usar conhecimento ofensivo para melhorar
a capacidade defensiva.
