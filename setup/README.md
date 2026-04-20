# Setup — Configuração do Ambiente

Documentação de instalação e configuração de cada componente do lab.

## Ficheiros nesta pasta

| Ficheiro | Descrição |
|---|---|
| `virtualbox.md` | Instalação do VirtualBox e configuração da rede isolada |
| `kali-setup.md` | Instalação e configuração do Kali Linux |
| `metasploitable.md` | Instalação do Metasploitable 2 |
| `wazuh-setup.md` | Instalação e configuração do Wazuh SIEM |

## Requisitos de Hardware

- **PC Principal:** Windows, 16GB RAM, ~150GB livres em disco
- **PC Extra:** usado como alvo físico ou para VMs adicionais
- **Rede:** NAT Network isolada no VirtualBox (10.0.2.0/24)

## Ordem de Instalação Recomendada

1. VirtualBox + Extension Pack
2. Criar a rede NAT isolada
3. Kali Linux (máquina de ataque)
4. Metasploitable 2 (alvo)
5. Wazuh SIEM (monitorização)

---
*Cada ficheiro .md desta pasta detalha o processo passo a passo.*
