# 🛡️ Home Lab — Cibersegurança Red & Blue Team

![Status](https://img.shields.io/badge/status-em%20progresso-blue?style=flat-square)
![Red Team](https://img.shields.io/badge/Red%20Team-Kali%20Linux-red?style=flat-square&logo=kalilinux&logoColor=white)
![Blue Team](https://img.shields.io/badge/Blue%20Team-Wazuh%20SIEM-blue?style=flat-square)
![Virtualização](https://img.shields.io/badge/VirtualBox-183A61?style=flat-square&logo=virtualbox&logoColor=white)
![TryHackMe](https://img.shields.io/badge/TryHackMe-em%20progresso-red?style=flat-square&logo=tryhackme&logoColor=white)
![MITRE](https://img.shields.io/badge/MITRE-ATT%26CK-red?style=flat-square)
![Cisco](https://img.shields.io/badge/Cisco-Introduction%20to%20Cybersecurity-blue?style=flat-square&logo=cisco&logoColor=white)
![Licença](https://img.shields.io/badge/uso-pessoal%20%2F%20educacional-green?style=flat-square)

> Repositório de documentação do meu home lab pessoal de cibersegurança.
> Construído para praticar técnicas ofensivas (Red Team) e defensivas (Blue Team),
> com o objetivo de aprofundar conhecimentos para o mestrado em cibersegurança.

---

## 🗺️ Arquitetura do Lab

```
PC Principal (Windows + VirtualBox)          PC Extra
├── 🔴 Kali Linux      → máquina de ataque   └── Alvo físico / VMs adicionais
│   └── Agente Wazuh instalado
├── 🎯 Metasploitable 2 → ambiente vulnerável
└── 🔵 Wazuh SIEM      → monitorização (192.168.1.x)

           Rede NAT Isolada: 10.0.2.0/24
     ⚠️  Nenhum tráfego malicioso sai para a internet
```

---

## 📁 Estrutura do Repositório

```
homelab-cybersecurity/
├── 📂 setup/          → instalação e configuração de cada VM
├── 📂 attacks/        → documentação de ataques controlados
├── 📂 defense/        → alertas SIEM e estratégias defensivas
├── 📂 ctf-writeups/   → soluções de desafios CTF
└── 📂 courses/        → notas e resumos de cursos
```

---

## 🧰 Tecnologias

| Ferramenta | Categoria | Uso |
|---|---|---|
| VirtualBox | Virtualização | Correr todas as VMs |
| Kali Linux | Red Team | Ataques e pentest |
| Metasploitable 2 | Alvo | Ambiente vulnerável para praticar |
| Metasploit Framework | Exploração | Execução de exploits |
| Nmap | Reconhecimento | Scan de portas e serviços |
| John the Ripper | Password Cracking | Quebrar hashes de passwords |
| DVWA | Web Hacking | Aplicação web vulnerável para praticar |
| Wazuh 4.14.5 | Blue Team / SIEM | Monitorização e deteção em tempo real |
| MITRE ATT&CK | Threat Intelligence | Classificação de técnicas de ataque |

---

## 🚦 Estado Atual

- [x] **Fase 1** — Configuração do ambiente (VirtualBox + VMs base) ✅
- [x] **Fase 2** — Primeiro ataque controlado com Metasploit ✅
- [x] **Fase 3** — Pós-exploração (root, shadow, persistência) ✅
- [x] **Fase 4** — SSH com credenciais fracas + escalada de privilégios ✅
- [x] **Fase 5** — Instalação e configuração do Wazuh SIEM ✅
- [x] **Fase 6** — Deteção de ataques em tempo real + MITRE ATT&CK ✅
- [x] **Fase 7** — Samba exploit + MySQL + Password Cracking ✅
- [x] **Fase 8** — SQL Injection no DVWA ✅
- [ ] **Fase 9** — Command Execution + XSS no DVWA
- [x] **Fase 10** — Cisco Introduction to Cybersecurity ← *em progresso*
- [x] **Fase 11** — CTF Writeups (TryHackMe) ← *em progresso*

---

## 🔴 Ataques Documentados

| # | Ataque | Alvo | Resultado | Data |
|---|---|---|---|---|
| 01 | [vsftpd 2.3.4 Backdoor](./attacks/01-vsftpd-exploit.md) | Metasploitable 2 | Root obtido | Abril 2026 |
| 02 | [Pós-Exploração](./attacks/02-pos-exploracao.md) | Metasploitable 2 | Persistência criada | Abril 2026 |
| 03 | [SSH Credenciais Fracas](./attacks/03-ssh-credenciais-fracas.md) | Metasploitable 2 | Root via escalada | Abril 2026 |
| 04 | [Samba Usermap Script](./attacks/04-samba-exploit.md) | Metasploitable 2 | Root obtido | Abril 2026 |
| 05 | [MySQL sem Password](./attacks/05-mysql-sem-password.md) | Metasploitable 2 | Dados extraídos | Abril 2026 |
| 06 | [Password Cracking](./attacks/06-password-cracking.md) | Metasploitable 2 | 6 passwords quebradas | Abril 2026 |
| 07 | [SQL Injection](./attacks/07-sql-injection.md) | DVWA / Metasploitable 2 | Base de dados extraída | Maio 2026 |

---

## 🔵 Defesa e Monitorização

| # | Documento | Descrição | Data |
|---|---|---|---|
| 01 | [Wazuh Setup](./setup/wazuh-setup.md) | Instalação e configuração do Wazuh SIEM | Abril 2026 |
| 02 | [Deteções Blue Team](./defense/01-wazuh-detecoes.md) | Alertas gerados pelos ataques em tempo real | Abril 2026 |
| 03 | [MITRE ATT&CK](./defense/02-mitre-attack.md) | Mapeamento das técnicas detetadas | Abril 2026 |

---

## 🟣 Purple Team — Resultados

Técnicas detetadas pelo Wazuh e mapeadas para o MITRE ATT&CK:

| Tática | Alertas | Técnica |
|---|---|---|
| Privilege Escalation | 12 | T1548.003 — Sudo and Sudo Caching |
| Defense Evasion | 12 | T1078 — Valid Accounts |
| Persistence | 6 | T1136 — Create Account |
| Initial Access | 6 | T1078 — Valid Accounts |

---

## 📚 Formação Complementar

| Curso | Plataforma | Estado |
|---|---|---|
| [Cisco Junior Cybersecurity Analyst](./courses/cisco-junior-cybersecurity-analyst.md) | Cisco NetAcad | 🔄 Em progresso (1/6 cursos) |
| CS50 SQL | Harvard / edX | 📅 Planeado |
| CS50 Cybersecurity | Harvard / edX | 📅 Planeado |
| 💼 Estágio IA.SAÚDE | IA.SAÚDE | 📅 Planeado |

- 🎓 Licenciatura em Engenharia Informática — Universidade da Madeira *(em curso)*
---

## 📝 CTF Writeups

### TryHackMe — Pré-segurança

| Sala | Categoria | Dificuldade | Data |
|---|---|---|---|
| [What is Networking?](./ctf-writeups/tryhackme/pre-security/01-what-is-networking.md) | Fundamentos | Info | Abril 2026 |
| [Offensive Security Intro](./ctf-writeups/tryhackme/pre-security/02-offensive-security-intro.md) | Red Team | Easy | Abril 2026 |
| [Defensive Security Intro](./ctf-writeups/tryhackme/pre-security/03-defensive-security-intro.md) | Blue Team | Info | Abril 2026 |
| [Experience Cyber Security](./ctf-writeups/tryhackme/pre-security/04-experience-cyber-security.md) | Overview | Easy | Abril 2026 |

### TryHackMe — Linux Fundamentals

| Sala | Categoria | Dificuldade | Data |
|---|---|---|---|
| [Linux Fundamentals Part 1](./ctf-writeups/tryhackme/linux-fundamentals/01-linux-fundamentals-part1.md) | Linux | Info | Abril 2026 |

---

## 🏆 Badges TryHackMe

| Badge | Descrição | Data |
|---|---|---|
| First Four | Completar as primeiras 4 atividades | Abril 2026 |

---

## 🎯 Objetivo

Documentar o processo de aprendizagem em cibersegurança, com foco em:

- 🔴 **Red Team** — reconhecimento, exploração de vulnerabilidades, pós-exploração
- 🔵 **Blue Team** — monitorização de logs, deteção de intrusões, resposta a incidentes
- 🟣 **Purple Team** — usar conhecimento ofensivo para melhorar a defesa

Preparação do portfólio para candidatura ao **Mestrado em Cibersegurança — Universidade de Aveiro**.

---

> ⚠️ **Aviso:** Ambiente 100% isolado. Todos os ataques são realizados exclusivamente
> em máquinas próprias, para fins educacionais.
