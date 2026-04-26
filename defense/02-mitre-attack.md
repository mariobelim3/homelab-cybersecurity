# MITRE ATT&CK — Mapeamento das Técnicas Detetadas

![Categoria](https://img.shields.io/badge/categoria-Threat%20Intelligence-purple?style=flat-square)
![Framework](https://img.shields.io/badge/MITRE-ATT%26CK-red?style=flat-square)

## O que é o MITRE ATT&CK?

O MITRE ATT&CK é uma base de dados mundial com todas as táticas
e técnicas usadas por atacantes reais em todo o mundo. É mantida
pelo MITRE Corporation e usada por empresas, governos e analistas
de segurança em todo o mundo.

Cada técnica tem um ID único (ex: T1078) e está organizada por:
- **Tática** — o objetivo do atacante (ex: Persistência)
- **Técnica** — como o atacante atinge esse objetivo (ex: Criar conta)

## Táticas Detetadas no Lab

### Privilege Escalation — 12 alertas
Técnicas usadas para obter permissões mais elevadas no sistema.

| Técnica | ID | Descrição | Como foi detetado |
|---|---|---|---|
| Sudo and Sudo Caching | T1548.003 | Usar sudo para escalar para root | `sudo su`, `sudo nmap` |
| Valid Accounts | T1078 | Usar contas legítimas para acesso | Login com msfadmin/msfadmin |

### Defense Evasion — 12 alertas
Técnicas para esconder atividade maliciosa.

| Técnica | ID | Descrição | Como foi detetado |
|---|---|---|---|
| Sudo and Sudo Caching | T1548.003 | Executar comandos como root | Múltiplos comandos sudo |
| Valid Accounts | T1078 | Usar contas válidas existentes | Acesso com credenciais reais |

### Persistence — 6 alertas
Técnicas para garantir acesso contínuo ao sistema.

| Técnica | ID | Descrição | Como foi detetado |
|---|---|---|---|
| Create Account | T1136 | Criar utilizador novo | `useradd -m teste123` |

### Initial Access — 6 alertas
Técnicas para entrar no sistema pela primeira vez.

| Técnica | ID | Descrição | Como foi detetado |
|---|---|---|---|
| Valid Accounts | T1078 | Usar credenciais válidas | Login SSH com msfadmin |

## Conclusão

O Wazuh mapeou automaticamente todas as ações realizadas no lab
para técnicas reais do MITRE ATT&CK — sem configuração adicional.

Isto demonstra que as técnicas praticadas no lab correspondem
exatamente ao que atacantes reais usam no mundo — e como um
Blue Team as detetaria numa empresa real.

O conhecimento deste framework é essencial para qualquer
profissional de cibersegurança, tanto em Red Team como em Blue Team.
