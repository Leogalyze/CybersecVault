---
title: TCP e UDP - Diferenças entre protocolos de transporte.
description: Exemplificando diferenças entre os protocolos de transporte TCP e UDP
tags:
  - Redes
  - "#Protocolos_Rede"
slug: tcp-udp-diferencas
date: 2025-08-27
lastmod: 2025-08-27
weight: 8
---
---
# Conceito Geral

A principal diferença entre TCP (protocolo de controle de transmissão) e UDP (protocolo de datagramas do usuário) é TCP é um protocolo baseado em conexão e UDP é sem conexão. O TCP transfere os dados lentamente e é mais confiável, enquanto o UDP funciona mais rapidamente mas é menos confiável. Isso torna cada protocolo adequado para diferentes tipos de transferências de dados.

Dois métodos diferentes para o mesmo trabalho.

---
## Analogia rápida

- **TCP** → É como uma ligação telefônica: antes de falar, você confirma que a outra pessoa está na linha e escutando.

- **UDP** → É como mandar um grito no estádio: você não sabe quem ouviu, só manda e pronto.

---

## Diferenças principais TCP vs UDP

|Característica|**TCP** 🛡️ (Transmission Control Protocol)|**UDP** ⚡ (User Datagram Protocol)|
|---|---|---|
|**Conexão**|Orientado à conexão (3-way handshake)|Sem conexão (fire-and-forget)|
|**Confiabilidade**|Garante entrega, ordem e sem duplicação|Não garante entrega nem ordem|
|**Controle de fluxo**|Tem (usa janela para regular o envio)|Não tem|
|**Controle de congestionamento**|Sim, adapta envio à rede|Não, envia sem se importar|
|**Velocidade**|Mais lento (overhead maior)|Mais rápido (menos cabeçalho)|
|**Tamanho do cabeçalho**|20 a 60 bytes|8 bytes|
|**Uso típico**|Quando **não pode perder dados** (HTTP, e-mail, SSH, FTP)|Quando **não pode atrasar dados** (DNS, streaming, VoIP, jogos)|
|**Método de envio**|Segmentos (com sequência e ACKs)|Datagramas independentes|
|**Orientação**|Orientado a fluxo de dados contínuo|Orientado a mensagens|

---
Em resumo:

- **TCP = confiabilidade acima de velocidade**
- **UDP = velocidade acima de confiabilidade**

---
# Notas relacionadas:

[[TCP-IP - O que é]]
[[UDP (User Datagram Protocol) - O que é]]

---