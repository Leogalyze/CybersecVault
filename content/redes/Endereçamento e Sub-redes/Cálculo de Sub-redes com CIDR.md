---
title: Cálculo de Sub-redes com CIDR
description: Resumo curto do que a nota aborda.
tags:
  - Redes
  - "#Enderecamento_SubRedes"
slug: calculo-subrede-cidr
date: 2025-09-02
lastmod: 2025-09-02
weight: 18
---
---
# Conceito Geral

## 1. O que é CIDR?

- **CIDR (Classless Inter-Domain Routing)** → forma moderna de representar redes.
- Sintaxe: `IP/prefixo`
    - Ex: `192.168.1.0/24`
- O **/n** significa quantos **bits da máscara** são usados para a rede.
    - `/24` → 24 bits rede + 8 bits host.
    - Máscara decimal: `255.255.255.0`.

---
## 2. Passos para calcular uma sub-rede

1. **Identificar a máscara/prefixo** → quantos bits são rede/host.
2. **Calcular número de endereços** → `2^(bits de host)`.
3. **Calcular hosts utilizáveis** → `2^(bits de host) – 2` (rede + broadcast não podem ser usados).
4. **Definir incrementos (block size)** → `256 – valor do último octeto da máscara`.
5. **Listar redes possíveis** → somando o block size.

---
## 3. Exemplos práticos

### Exemplo 1 — /26

Rede: `192.168.1.0/26`
- Máscara: `255.255.255.192`
- Bits de host: 6
- Endereços totais: `2^6 = 64`
- Hosts válidos: `62`
- Block size: `256 – 192 = 64`
- Sub-redes:
    - `192.168.1.0 – 192.168.1.63`
    - `192.168.1.64 – 192.168.1.127`
    - `192.168.1.128 – 192.168.1.191`
    - `192.168.1.192 – 192.168.1.255`

---
### Exemplo 2 — /29

Rede: `10.0.0.0/29`
- Máscara: `255.255.255.248`
- Bits de host: 3
- Endereços totais: `2^3 = 8`
- Hosts válidos: `6`
- Block size: `256 – 248 = 8`
- Sub-redes:
    - `10.0.0.0 – 10.0.0.7`
    - `10.0.0.8 – 10.0.0.15`
    - `10.0.0.16 – 10.0.0.23` …

---
### Exemplo 3 — /20

Rede: `172.16.0.0/20`
- Máscara: `255.255.240.0`
- Bits de host: 12
- Endereços totais: `2^12 = 4096`
- Hosts válidos: `4094`
- Block size: `256 – 240 = 16`
- Sub-redes:
    - `172.16.0.0 – 172.16.15.255`
    - `172.16.16.0 – 172.16.31.255`
    - `172.16.32.0 – 172.16.47.255` …

---
## 4. Fórmulas rápidas

- **Hosts válidos** = `2^(bits de host) – 2`
- **Sub-redes possíveis** = `2^(bits emprestados)`
- **Block size** = `256 – último octeto da máscara`

---
## 5. IPv6

- Mais simples: **sempre /64** para hosts.
- Subnetting usado apenas para **organização hierárquica** (ex: /48 → /64).

---
## 6. Ferramentas úteis

- **Linux:**
    `ipcalc 192.168.1.0/26`
- **Windows:** não tem nativo, mas pode usar sites como subnet-calculator.org.
- **CTFs/Labs:** sempre que pedir planejamento de rede, aplicar esse cálculo.

---
## Resumo:

- CIDR = define quantos bits da máscara são rede.
- Subnetting = dividir redes maiores em menores usando CIDR.
- Fórmulas + block size = sua “calculadora mental” de sub-redes.

---
# Notas relacionadas:

[[Segmentação de Redes - O que é]]

---