# Sala 2 — Offensive Security Intro

![Categoria](https://img.shields.io/badge/categoria-red%20team-red?style=flat-square)
![Dificuldade](https://img.shields.io/badge/dificuldade-easy-brightgreen?style=flat-square)
![Plataforma](https://img.shields.io/badge/TryHackMe-free-red?style=flat-square)

## Objetivo

Compreender o que é segurança ofensiva e realizar o primeiro ataque simulado
a um banco fictício (FakeBank) num ambiente completamente controlado e legal.

## O que é Segurança Ofensiva?

Segurança ofensiva consiste em pensar e agir como um atacante para encontrar
vulnerabilidades antes que alguém malicioso o faça. Os profissionais desta área
chamam-se Penetration Testers (ou ethical hackers).

O objetivo não é causar dano — é encontrar fraquezas para que possam ser corrigidas.

## Tarefa Realizada — Hack ao FakeBank

### Cenário
O FakeBank é um site bancário fictício com uma vulnerabilidade intencional.
O objetivo era encontrar uma página escondida que não devia ser acessível.

### Ferramenta Utilizada — GoBuster
O GoBuster é uma ferramenta de brute-force de diretórios web.
Testa automaticamente centenas de nomes de páginas para encontrar
URLs que existem mas não estão linkadas no site.

### Comando Executado
```bash
gobuster dir -u http://fakebank.thm -w wordlist.txt
```

- `dir` — modo de pesquisa de diretórios
- `-u` — URL alvo
- `-w` — wordlist (lista de nomes a testar)

### Resultado
O GoBuster encontrou a página `/bank-transfer` que não estava visível
no site mas existia no servidor. Esta página permitia transferências
sem autenticação — uma vulnerabilidade crítica.

## O que Aprendi

Esta sala mostrou-me que muitas vulnerabilidades não são técnicas complexas —
são simplesmente páginas esquecidas ou mal configuradas. A mentalidade ofensiva
é questionar tudo: "O que é que este sistema tem que não devia ter?"

## Ligação ao Home Lab

No home lab vou usar o Metasploit para explorar vulnerabilidades similares
no Metasploitable 2 — um ambiente vulnerável por design para praticar
exatamente este tipo de técnicas.
