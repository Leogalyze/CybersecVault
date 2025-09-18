---
title: User Datagram Protocol (UDP) - O que é?
description: Explicando o conceito geral do protocolo de transporte UDP
tags:
  - Redes
  - "#Protocolos_Rede"
slug: udp-conceito
date: 2025-08-27
lastmod: 2025-08-27
weight: 6
---
---
# Conceito Geral

O **UDP** é um protocolo de transporte da camada 4 do modelo OSI (e da camada de transporte no TCP/IP). Ele é chamado de **“sem conexão”** porque **não estabelece uma conexão antes de enviar os dados**. Ele simplesmente pega os dados, coloca dentro de um **datagrama** e joga na rede.

Diferente do **TCP**, o UDP **não garante**:

- Que os dados cheguem ao destino
- Que cheguem na ordem correta
- Que não haja duplicação

Ou seja, **não tem controle de fluxo nem retransmissão automática**.

---
### Estrutura básica de um datagrama UDP

Um pacote UDP é bem simples (8 bytes de cabeçalho):

- **Porta de origem (16 bits)** → quem enviou
- **Porta de destino (16 bits)** → para quem vai
- **Comprimento (16 bits)** → tamanho total do pacote
- **Checksum (16 bits)** → verificação básica de erro

Depois vem os **dados da aplicação**.

---
### Vantagens

- **Rápido e leve** (sem a burocracia do TCP)
- **Baixa latência** → ideal para apps em tempo real
- Funciona bem em **broadcast e multicast** (enviar para vários de uma vez)

---
### Exemplos de uso do UDP

- **DNS** (resolver nomes → IP)
- **VoIP** (ligações por internet)
- **Streaming de vídeo e áudio** (YouTube, Twitch, Spotify ao vivo)
- **Jogos online** (FPS, MOBA etc.)
- Protocolos como **DHCP, SNMP, TFTP**

---
Resumindo: **UDP é velocidade acima de confiabilidade**. Você usa quando **é mais importante ser rápido do que ser perfeito**.

---
# Notas relacionadas:

[[TCP e UDP - Diferenças]]

---