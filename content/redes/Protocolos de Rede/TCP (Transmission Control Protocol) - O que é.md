---
title: Transmission Control Protocol (TCP) - O que é?
description: Explicando o conceito geral do protocolo de transporte TCP
tags:
  - Redes
  - "#Protocolos_Rede"
slug: tcp-conceito
date: 2025-08-27
lastmod: 2025-08-27
weight: 7
---
---
# Conceito Geral

**TCP (Transmission Control Protocol)** É um protocolo de transporte da **Camada 4** (OSI / TCP-IP). Diferente do UDP, o **TCP é orientado à conexão**: antes de transmitir dados, ele garante que o outro lado está pronto para receber.

---
## Características principais

1. **Confiável** → garante que os dados cheguem no destino.
2. **Ordenado** → os pacotes chegam na mesma sequência em que foram enviados.
3. **Livre de duplicação** → não entrega duas vezes o mesmo dado.
4. **Controle de fluxo** → evita sobrecarregar o receptor.
5. **Controle de congestionamento** → evita saturar a rede.

---
## Como funciona a comunicação

Antes de enviar dados, o TCP faz o famoso **“three-way handshake”** (aperto de mão em 3 passos):

1. Cliente envia **SYN** (pedindo conexão).
2. Servidor responde com **SYN + ACK** (aceitando).
3. Cliente confirma com **ACK**.

Só depois disso a troca de dados começa.

Quando a comunicação termina, há um processo de **encerramento de conexão** (com pacotes FIN/ACK).

---
## Estrutura de um segmento TCP

O cabeçalho é mais robusto que o do UDP:

- Porta de origem e destino
- Número de sequência (ordem dos dados)
- Número de confirmação (ACK)
- Flags (SYN, ACK, FIN, RST, PSH, URG etc.)
- Janela (controle de fluxo)
- Checksum

---
## Exemplos de uso do TCP

Protocolos que **precisam de confiabilidade**:

- **HTTP/HTTPS** (web)
- **FTP** (transferência de arquivos)
- **SMTP/IMAP/POP3** (e-mails)
- **SSH** (acesso remoto seguro)

---
Resumindo: Ele oferece **confiabilidade, ordenação e controle** da comunicação (ideal quando não dá pra perder dados).

---
# Notas relacionadas:

[[TCP e UDP - Diferenças]]

---