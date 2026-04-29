# Ataque 06 — Password Cracking com John the Ripper

![Categoria](https://img.shields.io/badge/categoria-password%20cracking-red?style=flat-square)
![Ferramenta](https://img.shields.io/badge/ferramenta-John%20the%20Ripper-blue?style=flat-square)
![Alvo](https://img.shields.io/badge/alvo-Metasploitable%202-orange?style=flat-square)
![Resultado](https://img.shields.io/badge/resultado-6%20passwords%20quebradas-brightgreen?style=flat-square)

## Objetivo

Usar o John the Ripper para quebrar os hashes de passwords
extraídos do ficheiro `/etc/shadow` do Metasploitable 2.

## O que é o John the Ripper?

O John the Ripper é uma das ferramentas mais famosas de password
cracking. Testa milhares de combinações por segundo contra hashes
de passwords usando três métodos:

1. **Single mode** — variações do nome de utilizador
2. **Wordlist** — lista de passwords comuns
3. **Incremental** — força bruta com todas as combinações possíveis

## Extração dos Hashes

```bash
# No Kali — copiar o /etc/shadow do Metasploitable
ssh -o "HostKeyAlgorithms=+ssh-rsa" msfadmin@10.0.2.4 \
"sudo cat /etc/shadow" > hashes.txt
```

## Execução do John the Ripper

```bash
john hashes.txt
```

## Resultados — Passwords Descobertas

| Utilizador | Password |
|---|---|
| postgres | postgres |
| user | user |
| msfadmin | msfadmin |
| service | service |
| klog | 123456789 |
| sys | batman |

**6 passwords quebradas em segundos!**

## Análise dos Resultados

Os resultados mostram padrões de passwords fracas muito comuns:

- **Password = nome de utilizador** — postgres, user, msfadmin, service
  são todos exemplos de utilizadores que usam o próprio nome como password.
  É o erro mais comum e o primeiro que qualquer atacante testa.

- **Password numérica simples** — `123456789` do klog é uma das
  passwords mais usadas no mundo e está em qualquer wordlist.

- **Palavra do dicionário** — `batman` do sys é uma palavra comum
  que qualquer ataque de dicionário encontra em segundos.

## O que isto demonstra

Passwords fracas são o vetor de ataque mais explorado no mundo real.
Um atacante com acesso aos hashes (via /etc/shadow, base de dados,
ou dump de memória) consegue descobrir passwords fracas em segundos.

A diferença entre uma password quebrada em 1 segundo e uma que
demora anos está na complexidade:

| Tipo | Exemplo | Tempo para quebrar |
|---|---|---|
| Nome de utilizador | msfadmin | < 1 segundo |
| Sequência numérica | 123456789 | < 1 segundo |
| Palavra do dicionário | batman | < 1 segundo |
| Frase longa aleatória | Tr0ub4dor&3 | Anos |
| Password gerada | x7K#mP2$vQ | Séculos |

## Mitigação (Perspetiva Blue Team)

- Usar passwords longas e aleatórias (mínimo 16 caracteres)
- Nunca usar o nome de utilizador como password
- Usar um gestor de passwords (Bitwarden, KeePass)
- Implementar autenticação de dois fatores (2FA)
- Usar algoritmos modernos de hash (bcrypt, Argon2) em vez de MD5
- Monitorizar tentativas de acesso ao /etc/shadow com SIEM
