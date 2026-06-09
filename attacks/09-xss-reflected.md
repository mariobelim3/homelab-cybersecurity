# Ataque 09 — XSS Reflected no DVWA

![Categoria](https://img.shields.io/badge/categoria-web-red?style=flat-square)
![Ferramenta](https://img.shields.io/badge/ferramenta-Browser-blue?style=flat-square)
![Alvo](https://img.shields.io/badge/alvo-DVWA%20%2F%20Metasploitable%202-orange?style=flat-square)
![Resultado](https://img.shields.io/badge/resultado-cookies%20roubados-brightgreen?style=flat-square)
![OWASP](https://img.shields.io/badge/OWASP-Top%2010-red?style=flat-square)

## Objetivo

Explorar a vulnerabilidade XSS Reflected no DVWA para injetar
código JavaScript malicioso e roubar cookies de sessão.

## O que é XSS?

XSS (Cross-Site Scripting) ocorre quando uma aplicação web inclui
input do utilizador na página sem validação ou sanitização.
Um atacante pode injetar código JavaScript que será executado
no browser da vítima.

Existem três tipos de XSS:
- **Reflected** — o script é refletido de volta na resposta HTTP (este ataque)
- **Stored** — o script é guardado na base de dados e executa para todos os utilizadores
- **DOM-based** — manipulação do DOM sem passar pelo servidor

XSS é consistentemente uma das vulnerabilidades mais exploradas
no mundo — está no **OWASP Top 10** há mais de uma década.

## Acesso ao DVWA

1. Firefox no Kali → `http://10.0.2.4`
2. Login: `admin` / `password`
3. **DVWA Security** → **Low**
4. **XSS reflected**

## Exploração

### 1. Teste normal
```
Mario
```
Resultado: `Hello Mario` — a aplicação reflete o input na página

---

### 2. Injeção de JavaScript básica
```html

```
Resultado: janela de alerta aparece com o texto "XSS"

O browser executou o código JavaScript injetado — prova que
a aplicação não valida o input e qualquer script pode ser executado.

---

### 3. Roubo de cookies de sessão
```html

```
Resultado:
```
security=low
PHPSESSID=9...
```

Os cookies de sessão foram expostos! O `PHPSESSID` é o identificador
de sessão do utilizador — no mundo real um atacante usaria este
valor para fazer **Session Hijacking**.

## O que é Session Hijacking?

Com o `PHPSESSID` roubado, um atacante pode:
1. Abrir o browser
2. Substituir o seu próprio cookie pelo cookie roubado
3. Aceder à conta da vítima **sem precisar de password**

É como roubar o cartão de acesso de alguém — mesmo sem saber
o PIN, consegues entrar no edifício.

## Impacto

Com XSS Reflected foi possível:
- Executar código JavaScript arbitrário no browser
- Expor os cookies de sessão do utilizador
- Potencialmente fazer Session Hijacking
- Redirecionar a vítima para sites maliciosos
- Registar teclado (keylogging) via JavaScript

## Diferença entre XSS Reflected e Stored

| | XSS Reflected | XSS Stored |
|---|---|---|
| O script fica guardado? | Não | Sim (base de dados) |
| Quem é afetado? | Só quem clica no link malicioso | Todos os utilizadores |
| Gravidade | Alta | Crítica |
| Exemplo | Link malicioso enviado por email | Comentário num fórum |

## Mitigação (Perspetiva Blue Team)

- **Sanitizar todo o input** — escapar caracteres HTML especiais (`<`, `>`, `"`)
- **Content Security Policy (CSP)** — header HTTP que bloqueia scripts não autorizados
- **HttpOnly cookies** — impede JavaScript de aceder aos cookies
- **Validação do lado do servidor** — nunca confiar apenas na validação do cliente
- **WAF** — detetar e bloquear payloads XSS conhecidos
