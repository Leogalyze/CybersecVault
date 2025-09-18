---
title: IPv4 e IPv6 - Funcionamento
description: Explicação e comparativo técnico do IPv4 e IPv6
tags:
  - Redes
  - "#Protocolos_Rede"
slug: ipv4-ipv6-funcionamento
date: 2025-08-27
lastmod: 2025-08-27
weight: 5
---
---
# Conceito Geral

## Funcionamento do IP (Internet Protocol)

O IP (Internet Protocol) é o protocolo de endereçamento e roteamento de pacotes de dados em redes. Ele atua na camada 3 (Rede) do modelo OSI, e define como pacotes são enviados de uma origem até um destino.

Na prática ele funciona da seguinte forma:

1. Divisão em pacotes: Quando você envia dados (ex: acessa um site), tudo é quebrado em pacotes IP.
2. Endereçamento: Cada pacote tem um endereço de origem e destino
3. Roteamento: Os pacotes passam por roteadores que os direcionam para o destino.
4. Entrega de best-effort: O IP não garante entrega, ordem ou integridade dos pacotes; isso é papel do TCP, se usado.

## IPv4 vs IPv6 — Comparativo Técnico

| Característica         | IPv4                                  | IPv6                                        |
|------------------------|----------------------------------------|---------------------------------------------|
| Lançamento             | 1981                                   | 1998                                        |
| Tamanho do Endereço    | 32 bits (ex: 192.168.0.1)              | 128 bits (ex: 2001:0db8:85a3::8a2e:0370:7334) |
| Nº total de endereços  | ~4,3 bilhões                           | 2^128 (mais que grãos de areia na Terra 😅)  |
| Notação                | Decimal, separado por pontos           | Hexadecimal, separado por dois-pontos       |
| Configuração automática| DHCP                                   | SLAAC (auto) + DHCPv6                       |
| Segurança integrada    | Não (IPSec opcional)                   | Sim (IPSec nativo)                          |
| Fragmentação           | Feita pelo roteador                    | Feita apenas pelo host                      |
| Broadcast              | Suportado                              | Não existe (usa multicast)                  |
| Suporte a mobilidade   | Limitado                               | Melhor suporte nativo                       |

## Como saber se um IP é IPv4 ou IPv6?

### IPv4 — Características Visuais

- **Formato**: `d.d.d.d` (quatro blocos de números)
- **Exemplo**: `192.168.1.1`
- Cada bloco vai de **0 a 255**
- Usa **pontos** para separar os octetos

### IPv6 — Características Visuais

- **Formato**: hexadecimal, separado por **dois-pontos**
- **Exemplo**: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- Pode conter `::` para **representar zeros seguidos**
- Usa **letras de A a F** (além dos números)

## Então, na real… o que muda?

|Caso real|Diferença prática|
|---|---|
|Você vai escanear uma rede|Com IPv4, beleza. Com IPv6? Você nem sabe por onde começar se não tiver uma dica do range.|
|Quer proteger uma rede|Tem que lembrar que o IPv6 pode estar ativado, e o firewall pode deixar passar coisas que não deveriam.|
|Quer invadir uma rede|Se o alvo tem IPv6 ativado, pode rolar ataque ND spoofing, ou abusar de pacotes ICMPv6 pra mapear a rede.|
|Quer configurar um servidor|Pode configurar IP público real direto no host (sem precisar de NAT), o que facilita acesso remoto e aumenta o risco se não proteger bem.|

## Analogia rápida:

> IPv4 é tipo uma cidade superlotada onde as casas compartilham o mesmo endereço (NAT).  
> IPv6 é tipo cada casa do planeta ter seu próprio endereço global, direto na rua — **mais simples**, **mais direto**, **mais arriscado se não tiver portão**.


## Curiosidades Importantes

- IPv4 ainda é mais usado, mas os endereços estão praticamente esgotados.
- IPv6 é **mais seguro**, **mais rápido em redes modernas**, e **não precisa de NAT** (Network Address Translation).
- Em pentest, entender **como o IPv6 lida com descoberta de hosts** (ex: ICMPv6, NDP) é essencial — é uma porta de entrada que muitos admins ignoram.

---
# Notas relacionadas:

[[Endereçamento - IPv4 e IPv6]]

---