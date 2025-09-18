---
title: Endereçamento - IPv4 e IPv6
description: Estudando o conceito de endereçamento para IPv4 e IPv6
tags:
  - Redes
  - "#Enderecamento_SubRedes"
slug: ipv4-ipv6-enderecamento
date: 2025-08-30
lastmod: 2025-08-30
weight: 15
---
---
# Conceito Geral

**IP (Internet Protocol)**: identificador único para cada dispositivo na rede, funcionando como um “endereço de casa” para comunicação. Atua na **Camada 3 (Rede) do modelo OSI**.

|Característica|IPv4|IPv6|
|---|---|---|
|Tamanho|32 bits|128 bits|
|Formato|Decimal|Hexadecimal|
|Capacidade|~4,3 bilhões|Quase infinito|
|NAT|Essencial|Opcional|
|Broadcast|Sim|Não (usa Multicast)|
|Segurança|Opcional (IPSec)|Nativo (IPSec embutido)|
|Configuração|Manual/DHCP|SLAAC (auto) ou DHCPv6|
> **Regra visual:**  
> Se tem **pontos**, é IPv4.  
> Se tem **dois-pontos**, é IPv6.

## Estrutura do Endereço

- **IPv4 (32 bits)** → Rede + Host
    - Exemplo: `192.168.1.10/24`
- **IPv6 (128 bits)** → Prefixo + Interface ID
    - Exemplo: `2001:db8:abcd:1234::1/64`

---
## Máscara / Prefixo

- **CIDR (/n)** define onde termina a parte de rede e começa a parte de host.
- **IPv4** → máscara de sub-rede (ex: /24 = 255.255.255.0).
- **IPv6** → prefixos maiores (/64, /48), foco em organização.

---
## Tipos de Endereços

### IPv4

- **Rede (Network ID):** primeiro IP do bloco.
- **Host:** IP utilizável para máquina.
- **Broadcast:** último IP (ex: `192.168.1.255`).
- **Privado:** (10/8, 172.16/12, 192.168/16).
- **Público:** roteável na internet.
- **Loopback:** `127.0.0.1`.
- **APIPA:** `169.254.0.0/16`.

### IPv6

- **Unicast Global:** equivalente ao IPv4 público.
- **Link-local:** `fe80::/10`, obrigatório.
- **Loopback:** `::1`.
- **Multicast:** `ff00::/8`.
- **Anycast:** mesmo IP em vários hosts → roteamento p/ o mais próximo.

---
## Escopos de Endereçamento

- **Privado vs Público (IPv4).**
- **Global vs Local (IPv6).**
- Define o alcance da comunicação.

---
## Sub-redes (Subnetting)

- **Dividir redes em partes menores.**
- **IPv4:** otimização e isolamento de segmentos.
- **IPv6:** abundância de endereços → foco em hierarquia e organização.

---
## 📌 IPv4

- **Tamanho:** 32 bits (4 octetos → 0 a 255 cada).
- **Formato:** decimal com pontos → `192.168.0.1`.
- **Capacidade:** ~4,3 bilhões de endereços.
- **Problema:** escassez de endereços (por isso surgiu o IPv6).

### Classes (conceito clássico, não muito usado hoje, mas importante saber)

- **Classe A:** 1.0.0.0 – 126.255.255.255 → redes grandes.
- **Classe B:** 128.0.0.0 – 191.255.255.255 → médias.
- **Classe C:** 192.0.0.0 – 223.255.255.255 → pequenas.
- (D → multicast | E → experimental)

### Tipos de endereços IPv4

- **Público**: roteável na internet.
- **Privado**: só funciona em LAN (NAT necessário p/ internet).
    - 10.0.0.0/8
    - 172.16.0.0/12
    - 192.168.0.0/16
- **Loopback:** 127.0.0.1 (localhost).
- **APIPA:** 169.254.0.0/16 (quando não consegue DHCP).
- **Broadcast:** último IP de uma rede (ex: `192.168.1.255`).
- **Rede (Network ID):** primeiro IP da rede (ex: `192.168.1.0`).

---
## 📌IPv6

- **Tamanho:** 128 bits.
- **Formato:** hexadecimal, 8 blocos separados por “:”.  
    Ex: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`  
    (Pode encurtar zeros: `2001:db8:85a3::8a2e:370:7334`)
- **Capacidade:** praticamente infinita (3,4×10^38 endereços).

### Tipos de endereços IPv6

- **Unicast Global:** equivalente ao IPv4 público.
- **Link-Local:** obrigatório, prefixo `fe80::/10` (funciona dentro do segmento local, como o ARP no IPv4).
- **Loopback:** `::1`.
- **Multicast:** substitui broadcast (`ff00::/8`).
- **Anycast:** mesmo endereço em múltiplos hosts, roteado p/ o mais próximo.
### Características Importantes

- Sem NAT (cada dispositivo pode ter IP público).
- Segurança integrada (IPSec obrigatório).
- Autoconfiguração (SLAAC).

---
## Resumo: 
Endereçamento é a **linguagem de endereços da rede** → como identificar máquinas, separar redes, definir alcance (local/global), e calcular blocos de endereços (sub-redes).

---
# Notas relacionadas:

[[IP (v4 e v6) - Funcionamento]]

---