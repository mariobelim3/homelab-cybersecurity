# Pós-Exploração — Metasploitable 2

![Categoria](https://img.shields.io/badge/categoria-pós--exploração-red?style=flat-square)
![Acesso](https://img.shields.io/badge/acesso-root-brightgreen?style=flat-square)
![Alvo](https://img.shields.io/badge/alvo-Metasploitable%202-orange?style=flat-square)

## Objetivo

Após obter acesso via exploit vsftpd, explorar o sistema comprometido
usando técnicas de pós-exploração — recolha de informação e persistência.

## O que é Pós-Exploração?

É o conjunto de ações realizadas depois de entrar num sistema.
Um atacante usa esta fase para recolher informação, escalar privilégios,
e garantir que consegue voltar ao sistema mesmo que a vulnerabilidade
original seja corrigida.

## Comandos Executados

### Informação do sistema
```bash
sysinfo
```
Resultado:
```
Computer  : metasploitable.localdomain
OS        : Ubuntu 8.04
```

O sistema é um Ubuntu de 2008 — extremamente desatualizado.
Quanto mais antigo o sistema, mais vulnerabilidades conhecidas existem.

### Identificar o utilizador atual
```bash
getuid
```
Resultado: `root`

Ter acesso root é como estar no topo da pirâmide com controlo total
sobre o sistema. Podias apagar ficheiros, criar utilizadores, instalar
programas — sem qualquer restrição.

### Entrar na shell nativa do sistema
```bash
shell
whoami
```
Resultado: `root`

O comando `shell` abre a shell nativa do sistema alvo — como se
estivesses fisicamente à frente do Metasploitable a escrever comandos.

### Ver todos os utilizadores
```bash
cat /etc/passwd
```
Lista todos os utilizadores do sistema com as suas pastas e shells.
Útil para identificar contas com privilégios e planear próximos movimentos.

### Ver passwords encriptadas
```bash
cat /etc/shadow
```
Mostra os hashes das passwords de todos os utilizadores.
Só o root consegue ler este ficheiro. No mundo real um atacante
copiaria estes hashes e tentaria quebrá-los com ferramentas como
John the Ripper ou Hashcat.

### Configuração perigosa — .rhosts
```bash
cat /home/msfadmin/.rhosts
```
Resultado: `+ +`

Esta é uma das configurações mais perigosas que existem.
O `+ +` significa "qualquer máquina, qualquer utilizador pode entrar
sem password". É como ter um alarme topo de gama mas dar as chaves
de casa a toda a vizinhança — toda a gente pode entrar e sair
quando quiser.

### Criar persistência
```bash
useradd -m hacker123
cat /etc/passwd | grep hacker123
```
Resultado:
```
hacker123:x:1003:1003::/home/hacker123:/bin/sh
```

Criar um novo utilizador garante **persistência** — mesmo que a
backdoor original seja descoberta e fechada, este utilizador
continua a existir no sistema e permite voltar a entrar.

## Resumo das Vulnerabilidades Encontradas

| Vulnerabilidade | Gravidade | Descrição |
|---|---|---|
| vsftpd 2.3.4 backdoor | Crítica | Acesso root sem autenticação |
| Ubuntu 8.04 desatualizado | Alta | Dezenas de CVEs conhecidos |
| .rhosts com `+ +` | Crítica | Qualquer utilizador pode entrar |
| Passwords fracas | Alta | msfadmin/msfadmin |

## Mitigação (Perspetiva Blue Team)

- Atualizar o sistema operativo imediatamente
- Remover ou corrigir o ficheiro .rhosts
- Implementar política de passwords fortes
- Monitorizar criação de novos utilizadores com SIEM
- Auditar regularmente contas de utilizador existentes
