# 🔴 Attacks — Ataques Controlados

Documentação de todos os ataques realizados no ambiente isolado do lab.
Cada ataque é documentado com objetivo, metodologia, comandos utilizados e conclusões.

> ⚠️ Todos os ataques são realizados exclusivamente em máquinas próprias,
> num ambiente de rede isolado, para fins de aprendizagem.

---

## Índice de Ataques

| # | Ataque | Alvo | Ferramenta | Resultado | Data |
|---|---|---|---|---|---|
| 01 | [vsftpd 2.3.4 Backdoor](./01-vsftpd-exploit.md) | Metasploitable 2 | Metasploit | Root obtido | Abril 2026 |
| 02 | [Pós-Exploração](./02-pos-exploracao.md) | Metasploitable 2 | Shell / Linux | Persistência criada | Abril 2026 |
| 03 | [SSH Credenciais Fracas](./03-ssh-credenciais-fracas.md) | Metasploitable 2 | Metasploit / SSH | Root via escalada | Abril 2026 |
| 04 | [Samba Usermap Script](./04-samba-exploit.md) | Metasploitable 2 | Metasploit | Root obtido | Abril 2026 |
| 05 | [MySQL sem Password](./05-mysql-sem-password.md) | Metasploitable 2 | MySQL CLI | Dados extraídos | Abril 2026 |
| 06 | [Password Cracking](./06-password-cracking.md) | Metasploitable 2 | John the Ripper | 6 passwords quebradas | Abril 2026 |
| 07 | [SQL Injection](./07-sql-injection.md) | DVWA | Browser | Base de dados extraída | Maio 2026 |
| 08 | [Command Execution](./08-command-execution.md) | DVWA | Browser | RCE no servidor web | Maio 2026 |
| 09 | [XSS Reflected](./09-xss-reflected.md) | DVWA | Browser | Cookies de sessão roubados | Maio 2026 |

---

## Categorias de Ataques

### 🖥️ Exploits de Sistema (Metasploitable 2)
Ataques a serviços vulneráveis a correr no Metasploitable 2 —
FTP, SSH, Samba, MySQL. Foco em obter acesso root e técnicas
de pós-exploração.

### 🌐 Ataques Web (DVWA)
Ataques a aplicações web vulneráveis — SQL Injection, Command
Execution e XSS. Todas vulnerabilidades do **OWASP Top 10**,
as mais exploradas no mundo real.

---

## Estrutura de Documentação

Cada ataque é documentado com:

- **Objetivo** — o que se pretende aprender
- **Contexto** — porquê esta vulnerabilidade existe
- **Reconhecimento** — como foi identificada a vulnerabilidade
- **Exploração** — comandos e passos utilizados passo a passo
- **Resultado** — o que foi obtido
- **Mitigação** — como se defenderia este ataque (perspetiva Blue Team)

---

## Ferramentas Utilizadas

| Ferramenta | Uso |
|---|---|
| Nmap | Reconhecimento — scan de portas e serviços |
| Metasploit Framework | Execução de exploits (vsftpd, Samba, SSH) |
| John the Ripper | Password cracking — quebrar hashes MD5/crypt |
| MySQL CLI | Acesso direto à base de dados |
| Browser (Firefox) | Ataques web — SQL Injection, XSS, Command Execution |

---

## Ambiente de Teste

```
Kali Linux (10.0.2.3)     →     Metasploitable 2 (10.0.2.4)
     Atacante                         Alvo

           Rede NAT Isolada: 10.0.2.0/24
```

Todos os ataques são realizados numa rede completamente isolada.
Nenhum tráfego malicioso sai para a internet ou rede doméstica.
