---
title: Máscara de Rede e Máscaras de Sub-rede, o que são?
description: Explicando o conceito das máscaras de rede e sub-rede
tags:
  - Redes
  - "#Enderecamento_SubRedes"
slug: ""
date: 2025-08-31
lastmod: 2025-08-31
weight: 16
---
---
# Conceito Geral

## ​📌 Máscara de Rede (Classful)

### 1. Conceito

- **Máscara de rede** = define qual parte do endereço IP identifica a **rede** e qual parte identifica o **host**.
- No **modelo antigo (classful)**, cada classe tinha uma máscara **fixa e pré-definida**.
- Isso é feito **alterando a máscara** para “emprestar bits” da parte de host.
- Evita desperdício e melhora organização/segurança da rede.

---

### 2. Classes e Máscaras Padrão

|Classe|Faixa de Endereços|Máscara Padrão|CIDR|Hosts disponíveis|
|---|---|---|---|---|
|A|1.0.0.0 – 126.255.255.255|255.0.0.0|/8|~16 milhões|
|B|128.0.0.0 – 191.255.255.255|255.255.0.0|/16|~65 mil|
|C|192.0.0.0 – 223.255.255.255|255.255.255.0|/24|254|
|D|224.0.0.0 – 239.255.255.255|Multicast|–|–|
|E|240.0.0.0 – 255.255.255.255|Experimental|–|–|

---

### 3. Características

- Simples de entender.
    
- Muito **desperdício de IPs** (uma empresa pequena recebia /16 com milhares de IPs que nunca usava).
    
- Foi substituído pelo modelo **classless (CIDR)**, que é muito mais eficiente.

---
## **Resumo:** 

Máscara de rede (classful) = padrão fixo, ligado às classes A, B e C. Hoje é mais histórico, mas essencial para entender a evolução.

---
---
## 📌 Máscara de Sub-rede (Subnetting com CIDR)

### 1. Conceito

- **Subnetting** = técnica para dividir uma rede maior em várias menores.
    
- Utiliza **CIDR (Classless Inter-Domain Routing)**, que permite máscaras variáveis (`/n`).

---
### 2. Como funciona

- **IP** = rede + host.
- A máscara define onde termina a parte de rede.
- **CIDR Notation:** `/n` (quantos bits são usados para rede).
	* Exemplo:
	  * IP: `192.168.1.10/24` → 24 bits rede, 8 bits host.
	  * Se mudo para `/26` → 26 bits rede, 6 bits host → rede menor.

---
### 3. Fórmulas

- **Número de hosts por rede:** `2^(bits de host) – 2`
- **Número de sub-redes:** `2^(bits emprestados)``

---
### 4. Exemplo prático

Rede original: `192.168.1.0/24`  
Quero 4 redes menores.

- Uso `/26` → 64 endereços por rede (62 utilizáveis).
- Redes criadas:
    - `192.168.1.0 – 192.168.1.63`
    - `192.168.1.64 – 192.168.1.127`
    - `192.168.1.128 – 192.168.1.191`
    - `192.168.1.192 – 192.168.1.255`

---
### 5. Máscaras Comuns (IPv4)

|CIDR|Máscara decimal|Hosts válidos|
|---|---|---|
|/30|255.255.255.252|2|
|/29|255.255.255.248|6|
|/28|255.255.255.240|14|
|/27|255.255.255.224|30|
|/26|255.255.255.192|62|
|/25|255.255.255.128|126|
|/24|255.255.255.0|254|

---
### IPv6

- Sempre dividido em **/64** (64 bits rede + 64 bits host).
- Subnetting no IPv6 é mais sobre **organização hierárquica**, não economia.

---
## Resumo:

- **Máscara de rede** → conceito antigo, classes fixas.
- **Máscara de sub-rede** → conceito moderno (CIDR), flexível, usado em qualquer rede hoje.

---
---
# Análise ofensiva/defensiva

### 🔸Ponto de vista de **Ataque**

1. **Reconhecimento (Scanning):**
    - Quando um atacante descobre o IP de uma máquina, ele vai tentar deduzir a máscara/sub-rede para saber **quantos hosts estão no mesmo segmento**.
    - Exemplo: se o alvo está em `192.168.1.34/24`, o atacante sabe que potencialmente tem **254 máquinas válidas** para escanear no mesmo broadcast domain.
    - Isso amplia a superfície de ataque.

2. **Movimentação lateral:**
    - Em redes **sem segmentação** (uma única /24 ou /16 enorme), se o atacante comprometer uma máquina, ele pode escanear e atacar facilmente as demais, porque estão no mesmo domínio de broadcast.
    - Isso facilita ataques como **ARP spoofing, sniffing e propagação de malware**.

3. **Identificação de redes privilegiadas:**
    - Se um atacante percebe que há **sub-redes diferentes para servidores, usuários e dispositivos de segurança**, ele pode tentar priorizar o acesso à rede “certa”.
    - Exemplo: notar que `10.0.10.0/24` é rede de usuários e `10.0.20.0/24` é rede de banco de dados → alvo valioso detectado.

---
### 🔹Ponto de vista de **Defesa**

1. **Redução da superfície de ataque:**
    - Usando **sub-redes menores (/26, /28)**, você reduz a quantidade de hosts que compartilham o mesmo broadcast domain.
    - Isso dificulta varreduras em massa e limita impacto de ataques de rede locais.

2. **Isolamento por função (Segregação de Rede):**
    - Separar redes de **usuários, servidores, IoT, sistemas críticos, gestão**.
    - Mesmo que um atacante entre em uma máquina de usuário, não terá acesso direto ao banco de dados ou ao firewall.
    - Exemplo: usar VLANs + ACLs + Firewalls para aplicar regras como _“Rede de usuários não acessa diretamente a rede de banco de dados”_.

3. **Monitoramento mais granular:**
    - Com redes segmentadas, o tráfego entre sub-redes passa por roteadores/firewalls → **visibilidade e logs**.
    - Isso permite detectar movimentação lateral suspeita.

4. **Defesa em profundidade:**
    - Um incidente em uma rede não compromete o restante.
    - Exemplo: se um ransomware pega a rede de usuários, a rede de servidores ainda pode estar protegida se bem segmentada.

---
## Resumo:

- **Ataque:** Máscara/sub-rede grande = playground enorme para o invasor.
- **Defesa:** Segmentação e sub-redes pequenas = limitar impacto, aumentar visibilidade e controle.

---