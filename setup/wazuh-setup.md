# Wazuh SIEM — Instalação e Configuração

![Categoria](https://img.shields.io/badge/categoria-Blue%20Team-blue?style=flat-square)
![Ferramenta](https://img.shields.io/badge/ferramenta-Wazuh%204.14.5-blue?style=flat-square)
![Estado](https://img.shields.io/badge/estado-operacional-brightgreen?style=flat-square)

## O que é o Wazuh?

O Wazuh é um SIEM (Security Information and Event Management) open source
usado por empresas reais em todo o mundo. Monitoriza sistemas em tempo real,
recolhe logs, deteta comportamentos suspeitos e gera alertas classificados
pelo framework MITRE ATT&CK.

No lab, o Wazuh é o lado Blue Team — enquanto o Kali ataca,
o Wazuh deteta e regista tudo o que acontece.

## Arquitetura

```
Kali Linux (agente Wazuh instalado)
       ↓ envia logs em tempo real
Wazuh Server (192.168.1.140)
       ↓ processa e classifica
Dashboard (browser Windows)
       ↓ mostra alertas e técnicas MITRE
```

## Instalação do Wazuh Server

1. Descarregar o OVA oficial em documentation.wazuh.com
2. Importar no VirtualBox
3. Configurar RAM: 4096 MB
4. Rede: Bridged Adapter (para acesso pelo browser Windows)
5. Arrancar e fazer login: `wazuh-user` / `wazuh`
6. Aceder ao dashboard: `https://192.168.1.140`
7. Login no dashboard: `admin` / `admin`

> O Wazuh demora 3-5 minutos a arrancar completamente
> após ligar — é normal devido aos vários serviços internos.

## Instalação do Agente no Kali

O Metasploitable 2 é demasiado antigo (Ubuntu 8.04, i386) para
correr o agente Wazuh moderno — incompatibilidade de bibliotecas SSL.
Optámos por instalar o agente no Kali Linux.

```bash
# Descarregar o agente
wget https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.14.5-1_amd64.deb

# Instalar com configuração do servidor
sudo WAZUH_MANAGER='192.168.1.140' WAZUH_AGENT_NAME='kali-attacker' dpkg -i wazuh-agent_4.14.5-1_amd64.deb

# Iniciar o agente
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent

# Verificar estado
sudo systemctl status wazuh-agent
```

## Verificação

Após iniciar o agente, o dashboard mostra:
- **Active (1)** — Kali ligado e monitorizado
- Alertas começam a aparecer automaticamente
- O agente aparece como `kali-attacker` no dashboard

## Notas Técnicas

- O Wazuh Server usa **Bridged Adapter** para ser acessível pelo browser Windows
- O Kali usa **NAT Network (LabNetwork)** para os ataques ao Metasploitable
- O agente comunica com o servidor via IP `192.168.1.140` porta 1514
