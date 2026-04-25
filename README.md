# 🛡️ Home Lab — Cibersegurança Red & Blue Team

![Status](https://img.shields.io/badge/status-em%20progresso-blue?style=flat-square)
![Red Team](https://img.shields.io/badge/Red%20Team-Kali%20Linux-red?style=flat-square&logo=kalilinux&logoColor=white)
![Blue Team](https://img.shields.io/badge/Blue%20Team-Wazuh%20SIEM-blue?style=flat-square)
![Virtualização](https://img.shields.io/badge/VirtualBox-183A61?style=flat-square&logo=virtualbox&logoColor=white)
![TryHackMe](https://img.shields.io/badge/TryHackMe-em%20progresso-red?style=flat-square&logo=tryhackme&logoColor=white)
![Licença](https://img.shields.io/badge/uso-pessoal%20%2F%20educacional-green?style=flat-square)

> Repositório de documentação do meu home lab pessoal de cibersegurança.
> Construído para praticar técnicas ofensivas (Red Team) e defensivas (Blue Team),
> com o objetivo de aprofundar conhecimentos para o mestrado em cibersegurança.

---

## 🗺️ Arquitetura do Lab

```
PC Principal (Windows + VirtualBox)          PC Extra
├── 🔴 Kali Linux      → máquina de ataque   └── Alvo físico / VMs adicionais
├── 🎯 Metasploitable 2 → ambiente vulnerável
├── 🖥️  Ubuntu Server   → servidor alvo
└── 🔵 Wazuh SIEM      → monitorização

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
└── 📂 ctf-writeups/   → soluções de desafios CTF
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
| Wazuh | Blue Team / SIEM | Monitorização e deteção |

---

## 🚦 Estado Atual

- [x] **Fase 1** — Configuração do ambiente (VirtualBox + VMs base) ✅
- [x] **Fase 2** — Primeiro ataque controlado com Metasploit ✅
- [x] **Fase 3** — Pós-exploração (root, shadow, persistência) ✅
- [x] **Fase 4** — SSH com credenciais fracas + escalada de privilégios ✅
- [ ] **Fase 5** — Instalação e configuração do Wazuh SIEM
- [ ] **Fase 6** — Integração Red/Blue (deteção de ataques em tempo real)
- [x] **Fase 7** — CTF Writeups (TryHackMe) ← *em progresso*

---

## 🔴 Ataques Documentados

| # | Ataque | Alvo | Resultado | Data |
|---|---|---|---|---|
| 01 | [vsftpd 2.3.4 Backdoor](./attacks/01-vsftpd-exploit.md) | Metasploitable 2 | Root obtido | Abril 2026 |
| 02 | [Pós-Exploração](./attacks/02-pos-exploracao.md) | Metasploitable 2 | Persistência criada | Abril 2026 |
| 03 | [SSH Credenciais Fracas](./attacks/03-ssh-credenciais-fracas.md) | Metasploitable 2 | Root via escalada | Abril 2026 |

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

## 🎯 Objetivo

Documentar o processo de aprendizagem em cibersegurança, com foco em:

- 🔴 **Red Team** — reconhecimento, exploração de vulnerabilidades, pós-exploração
- 🔵 **Blue Team** — monitorização de logs, deteção de intrusões, resposta a incidentes
- 🟣 **Purple Team** — usar conhecimento ofensivo para melhorar a defesa

Preparação do portfólio para candidatura ao **Mestrado em Cibersegurança — Universidade de Aveiro**.

---

## 📚 Formação Complementar

- 🎓 Licenciatura em Engenharia Informática — Universidade da Madeira *(em curso)*
- 📜 CS50 SQL — Harvard / edX *(planeado)*
- 📜 CS50 Cybersecurity — Harvard / edX *(planeado)*
- 💼 Estágio — IA.SAÚDE *(planeado)*

---

## 🏆 Badges TryHackMe

| Badge | Descrição | Data |
|---|---|---|
| First Four | Completar as primeiras 4 atividades | Abril 2026 |

---

> ⚠️ **Aviso:** Ambiente 100% isolado. Todos os ataques são realizados exclusivamente
> em máquinas próprias, para fins educacionais.
