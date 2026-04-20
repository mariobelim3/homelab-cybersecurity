# Sala 1 — What is Networking?

![Categoria](https://img.shields.io/badge/categoria-fundamentos-blue?style=flat-square)
![Dificuldade](https://img.shields.io/badge/dificuldade-info-lightgrey?style=flat-square)
![Plataforma](https://img.shields.io/badge/TryHackMe-free-red?style=flat-square)

## Objetivo

Compreender o que é uma rede de computadores, como os dispositivos comunicam
entre si e os conceitos básicos que estão na base de toda a cibersegurança.

## Conceitos Abordados

### O que é uma Rede?
Uma rede é um conjunto de dispositivos interligados que comunicam entre si.
Pode ser tão simples como dois computadores ligados por cabo, ou tão complexa
como a internet com milhares de milhões de dispositivos.

### Endereço IP
Cada dispositivo numa rede tem um endereço IP (Internet Protocol) único.
Funciona como uma morada — permite identificar de onde vem e para onde vai a informação.

Exemplo:
- IPv4: `192.168.1.1` (formato mais comum, 4 grupos de números)
- IPv6: `2001:0db8:85a3::8a2e:0370:7334` (formato mais recente, maior capacidade)

### Endereço MAC
O endereço MAC (Media Access Control) é um identificador físico único gravado
em cada placa de rede. Ao contrário do IP (que pode mudar), o MAC é permanente.

Exemplo: `a4:c3:f0:85:ac:2d`

### Protocolos Principais
- **TCP/IP** — base da comunicação na internet, garante que os dados chegam corretamente
- **UDP** — mais rápido que TCP mas sem garantia de entrega (usado em streaming, jogos)
- **HTTP/HTTPS** — comunicação entre browser e servidores web

## O que Ficou em Memória

Antes desta sala sabia que redes existiam mas não compreendia como os dispositivos
se "encontravam" uns aos outros. Agora percebo que o IP é a "morada" e o MAC é
a "identidade" — conceitos completamente diferentes com funções diferentes.

## Ligação à Cibersegurança

Sem entender redes é impossível fazer pentest ou monitorização.
Saber o que é um IP, uma porta e um protocolo é o ponto de partida
para ferramentas como o Nmap (scan de redes) que vou usar no home lab.
