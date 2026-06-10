# 🔵 Defense — Blue Team e Monitorização

Documentação das estratégias defensivas, alertas SIEM e análise de logs
gerados pelos ataques realizados no lab.

---

## Ferramentas

- **Wazuh 4.14.5** — SIEM open source para monitorização e deteção de intrusões
- **MITRE ATT&CK** — framework de classificação de técnicas de ataque

---

## Conteúdo desta Pasta

| Ficheiro | Descrição |
|---|---|
| [wazuh-setup.md](../setup/wazuh-setup.md) | Instalação e configuração do Wazuh SIEM |
| [01-wazuh-detecoes.md](./01-wazuh-detecoes.md) | Alertas gerados pelos ataques em tempo real |
| [02-mitre-attack.md](./02-mitre-attack.md) | Mapeamento das técnicas detetadas no MITRE ATT&CK |

---

## Arquitetura de Monitorização

```
Kali Linux (kali-attacker)
    └── Agente Wazuh instalado
           ↓ envia logs em tempo real
    Wazuh Server (192.168.1.x)
           ↓ processa e classifica
    Dashboard (browser Windows)
           ↓ alertas + MITRE ATT&CK
```

---

## Alertas Gerados — Resumo

| Atividade | Severidade | Técnica MITRE |
|---|---|---|
| Scan Nmap com sudo | Low | Discovery |
| Acesso a /etc/shadow | Low | Credential Access |
| Criação de utilizador (useradd) | Low | T1136 — Persistence |
| Escalada de privilégios (sudo su) | Medium | T1548.003 — Privilege Escalation |
| Comandos sudo repetidos | Medium | T1078 — Valid Accounts |

**Total de alertas gerados:** 129+

---

## Táticas MITRE ATT&CK Detetadas

| Tática | Alertas | Técnica |
|---|---|---|
| Privilege Escalation | 12 | T1548.003 — Sudo and Sudo Caching |
| Defense Evasion | 12 | T1078 — Valid Accounts |
| Persistence | 6 | T1136 — Create Account |
| Initial Access | 6 | T1078 — Valid Accounts |

---

## Metodologia Purple Team

Para cada ataque documentado em `attacks/` existe uma análise
defensiva correspondente:

| Ataque (Red Team) | Deteção (Blue Team) | Mitigação |
|---|---|---|
| vsftpd backdoor | Ligação suspeita porta 21 | Atualizar vsftpd |
| SSH credenciais fracas | Múltiplos logins SSH | Fail2ban + passwords fortes |
| Samba exploit | Ligação suspeita porta 445 | Atualizar Samba |
| MySQL sem password | Acesso DB sem autenticação | Configurar password root |
| Password cracking | Acesso a /etc/shadow | Bcrypt + passwords fortes |
| SQL Injection | Queries SQL anómalas | Prepared statements |
| Command Execution | Comandos suspeitos no servidor | Validação de input |
| XSS Reflected | Scripts injetados na página | Sanitização de output |

---

## Conclusão

O lab demonstrou que o Wazuh deteta automaticamente atividades
suspeitas e as mapeia para o framework MITRE ATT&CK — sem
configuração adicional. Isto confirma o valor do Purple Team:
usar conhecimento ofensivo para melhorar a capacidade defensiva.
