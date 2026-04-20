# Sala 3 — Defensive Security Intro

![Categoria](https://img.shields.io/badge/categoria-blue%20team-blue?style=flat-square)
![Dificuldade](https://img.shields.io/badge/dificuldade-info-lightgrey?style=flat-square)
![Plataforma](https://img.shields.io/badge/TryHackMe-free-red?style=flat-square)

## Objetivo

Compreender o que é segurança defensiva e como os profissionais de Blue Team
protegem sistemas, detetam intrusões e respondem a incidentes.

## O que é Segurança Defensiva?

Ao contrário do Red Team (que ataca), o Blue Team defende.
O objetivo é prevenir ataques, detetá-los quando acontecem
e responder de forma eficaz para minimizar o dano.

## Áreas Principais do Blue Team

### SOC (Security Operations Center)
Equipa responsável por monitorizar sistemas 24/7.
Analisam alertas, investigam incidentes e respondem a ameaças em tempo real.

### SIEM (Security Information and Event Management)
Sistema que recolhe logs de toda a infraestrutura e gera alertas
quando deteta comportamentos suspeitos.

No home lab vou usar o **Wazuh** — um SIEM open source gratuito.

### Threat Intelligence
Recolha de informação sobre ameaças conhecidas para antecipar ataques.
Inclui análise de malware, técnicas de atacantes (TTPs) e indicadores de compromisso (IOCs).

### DFIR (Digital Forensics and Incident Response)
Após um ataque, o DFIR investiga o que aconteceu, como entrou o atacante,
o que foi acedido e como evitar que se repita.

## Tarefa Realizada — Análise de Logs no FakeBank

### Cenário
O FakeBank sofreu um ataque. A tarefa era analisar os logs do SIEM
para identificar o IP do atacante e o que foi acedido.

### Processo
1. Abri o SIEM simulado no browser
2. Filtrei os logs por eventos suspeitos
3. Identifiquei um IP externo a aceder repetidamente à página `/bank-transfer`
4. Marquei o evento como incidente e documentei o IP malicioso

## O que Aprendi

A perspetiva defensiva é completamente diferente da ofensiva.
No Red Team pergunto "como posso entrar?", no Blue Team pergunto
"o que é que os logs me estão a dizer?". As duas mentalidades
complementam-se — é por isso que o Purple Team é tão valioso.

## Ligação ao Home Lab

O Wazuh que vou instalar no home lab faz exatamente o que este SIEM
simulado faz, mas em tempo real com as minhas próprias VMs.
