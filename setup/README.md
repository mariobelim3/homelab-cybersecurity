# ⚙️ Setup — Configuração do Ambiente

Documentação de instalação e configuração de cada componente do lab.

---

## Ficheiros nesta Pasta

| Ficheiro | Descrição |
|---|---|
| [virtualbox.md](./virtualbox.md) | Instalação do VirtualBox e configuração da rede isolada |
| [kali-setup.md](./kali-setup.md) | Instalação e configuração do Kali Linux |
| [metasploitable.md](./metasploitable.md) | Instalação do Metasploitable 2 |
| [wazuh-setup.md](./wazuh-setup.md) | Instalação e configuração do Wazuh SIEM |

---

## Requisitos de Hardware

- **PC Principal:** Windows, 16GB RAM, ~150GB livres em disco
- **PC Extra:** usado como alvo físico ou para VMs adicionais
- **Rede:** NAT Network isolada no VirtualBox (10.0.2.0/24)

---

## Arquitetura de Rede

```
PC Principal (Windows)
├── VirtualBox
│   ├── Kali Linux (10.0.2.3)        → NAT Network + Bridged Adapter
│   ├── Metasploitable 2 (10.0.2.4)  → NAT Network
│   └── Wazuh SIEM (192.168.1.x)     → Bridged Adapter
│
└── Browser Windows → acede ao dashboard Wazuh via https://192.168.1.x
```

---

## Ordem de Instalação Recomendada

1. VirtualBox + Extension Pack
2. Criar a rede NAT isolada (LabNetwork — 10.0.2.0/24)
3. Kali Linux (máquina de ataque)
4. Metasploitable 2 (alvo)
5. Wazuh SIEM (monitorização)
6. Instalar agente Wazuh no Kali

---

## Notas Importantes

> ⚠️ **OneDrive** — Nunca guardar ficheiros `.vdi` de VMs em pastas
> sincronizadas com OneDrive. Causa erros de leitura e corrupção dos ficheiros.
> Guardar sempre em `C:\VMs\` ou outra pasta local.

> ⚠️ **Wazuh IP** — O Wazuh usa Bridged Adapter e o IP muda a cada arranque.
> Após cada reinício verificar o IP com `ip a` e atualizar a configuração
> do agente no Kali se necessário:
> ```bash
> sudo nano /var/ossec/etc/ossec.conf
> sudo systemctl restart wazuh-agent
> sudo /var/ossec/bin/agent-auth -m [NOVO_IP_WAZUH]
> ```

> ⚠️ **Kali — dois adaptadores** — O Kali tem dois adaptadores de rede:
> - **Adaptador 1:** NAT Network (LabNetwork) — para comunicar com o Metasploitable
> - **Adaptador 2:** Bridged Adapter — para comunicar com o Wazuh

---

*Cada ficheiro .md desta pasta detalha o processo passo a passo.*
