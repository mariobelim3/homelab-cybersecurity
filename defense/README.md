# Defense — Blue Team e Monitorização

Documentação das estratégias defensivas, alertas SIEM e análise de logs.

## Ferramentas

- **Wazuh** — SIEM open source para monitorização e deteção de intrusões
- **Security Onion** *(futuro)* — plataforma completa de monitorização de rede

## Conteúdo desta Pasta

| Ficheiro | Descrição |
|---|---|
| `wazuh-alerts.md` | Alertas gerados durante os ataques |
| `detections.md` | Regras e deteções configuradas |
| `incident-response.md` | Notas sobre resposta a incidentes |

## Metodologia Purple Team

Para cada ataque documentado em `attacks/`, existe uma entrada
correspondente aqui com:
- O alerta gerado no Wazuh
- A regra que o detetou
- Como melhorar a deteção
