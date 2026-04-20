# Home Lab — Cibersegurança Red & Blue Team

Repositório de documentação do meu home lab pessoal de cibersegurança.
Construído para praticar técnicas ofensivas (Red Team) e defensivas (Blue Team),
com o objetivo de aprofundar conhecimentos para o mestrado em cibersegurança.

## Arquitetura do Lab

```
PC Principal (Windows + VirtualBox)
├── VM Kali Linux          → máquina de ataque (Red Team)
├── VM Metasploitable 2    → alvo vulnerável
├── VM Ubuntu Server       → servidor alvo adicional
└── VM Wazuh               → SIEM - monitorização (Blue Team)

PC Extra
└── Alvo físico real / VMs adicionais
```

Todas as VMs estão numa rede NAT isolada (10.0.2.0/24).
Nenhum tráfego malicioso sai para a rede doméstica.

## Estrutura do Repositório

```
homelab-cybersecurity/
├── setup/          → instalação e configuração de cada VM
├── attacks/        → documentação de ataques controlados
├── defense/        → alertas SIEM e estratégias defensivas
└── ctf-writeups/   → soluções de desafios CTF
```

## Tecnologias Utilizadas

- VirtualBox — virtualização
- Kali Linux — testes de penetração
- Metasploitable 2 — ambiente vulnerável
- Wazuh — SIEM open source
- Metasploit Framework — exploração
- Nmap — reconhecimento de rede

## Estado Atual

- [ ] Fase 1 — Configuração do ambiente (VirtualBox + VMs base)
- [ ] Fase 2 — Primeiro ataque controlado com Metasploit
- [ ] Fase 3 — Instalação e configuração do Wazuh SIEM
- [ ] Fase 4 — Integração Red/Blue (deteção de ataques em tempo real)
- [ ] Fase 5 — CTF Writeups (TryHackMe / HackTheBox)

## Objetivo

Documentar o processo de aprendizagem em cibersegurança,
com foco em Red Team (pentest) e Blue Team (monitorização e defesa),
preparando o portfólio para candidatura ao mestrado em cibersegurança.

---
*Ambiente 100% isolado. Todos os ataques são realizados em máquinas próprias.*
