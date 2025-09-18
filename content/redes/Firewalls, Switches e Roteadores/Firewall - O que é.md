---
title: Firewall - O que é ?
description: Explicando o que é e como funciona os Firewalls
tags:
  - Redes
slug: firewall-conceito
date: 2025-09-02
lastmod: 2025-09-02
weight: 22
---
---
# Conceito Geral

## O que é um Firewall?

Um **firewall** é um sistema de segurança que **controla o tráfego de rede** com base em regras definidas.  
Ele decide se um pacote pode **entrar, sair ou ser bloqueado** de acordo com políticas de segurança.

> Pensa nele como o **porteiro de um prédio**: só entra quem tem permissão.

---

## Tipos de Firewalls

1. **Packet Filtering (Camada 3/4 – Rede/Transporte)**
    - Analisa IP, porta, protocolo.
    - Simples e rápido, mas não vê conteúdo.
    - Exemplo: regras `iptables` no Linux.

2. **Stateful Firewall**
    - Mantém **estado da conexão** (TCP handshake).
    - Exemplo: sabe diferenciar `SYN` de `ACK`.
    - Mais seguro que só filtro de pacotes.

3. **Application Firewall (Camada 7 – Aplicação)**
    - Entende protocolos como HTTP, DNS, FTP.
    - Pode bloquear ataques de aplicação.
    - Exemplo: **WAF (Web Application Firewall)** → protege contra SQLi, XSS.

4. **Next-Gen Firewall (NGFW)**
    - Integra IDS/IPS, antivírus, sandbox.
    - Faz inspeção profunda de pacotes (DPI).

---
## Exemplo prático (Linux – iptables)

```
# Bloquear todo tráfego de entrada por padrão
iptables -P INPUT DROP

# Permitir tráfego de saída
iptables -P OUTPUT ACCEPT

# Permitir conexões estabelecidas
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Permitir SSH na porta 22
iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Permitir HTTP/HTTPS
iptables -A INPUT -p tcp -m multiport --dports 80,443 -j ACCEPT
```

> Aqui você cria sua **política default deny** e libera só o que interessa.

---
## **Tipos de implementação**

### Firewall como Dispositivo (Hardware Firewall)

- É um **appliance dedicado** (caixa física) que fica na borda da rede.
- Exemplo: Fortinet FortiGate, Cisco ASA, Palo Alto.
- Normalmente tem **sistema próprio, alto desempenho e múltiplas interfaces**.
- Usado em **empresas** para proteger redes inteiras.

### Firewall como Software (Software Firewall)

- Roda dentro de um **sistema operacional**.
- Pode ser em servidores, desktops ou até em roteadores caseiros.
- Exemplos:
    - **iptables / nftables** (Linux)
    - **Windows Defender Firewall**
    - **pf** (BSD, usado em firewalls como pfSense e OPNsense)

### Firewall Híbrido (Virtual / Cloud)

- Hoje em dia, com **cloud computing**, temos firewalls virtuais.
- São softwares que simulam appliances em nuvem.
- Exemplo: AWS Security Groups, Azure Firewall.

### Como entender a diferença

- **Dispositivo** → especializado, dedicado, físico (mas internamente roda software também).
- **Software** → programa que roda num sistema já existente.

>  O conceito central continua sendo o mesmo: **filtrar e inspecionar pacotes**.  
  O que muda é o **contexto de uso** (casa, servidor, empresa, nuvem).

---
---
# Análise ofensiva/defensiva

## 🔸 Ofensiva (como atacantes lidam com Firewalls)

- **Port Scanning evasivo** (Nmap com técnicas de fragmentação ou slow scan).
- **Tunneling** (usar HTTP/HTTPS para encapsular outro tráfego).
- **Bypass** via serviços mal configurados (ex: porta 22 aberta para o mundo).
- Exploração de **falhas em firewalls NGFW/WAF** (ex: regras mal escritas, bypass de regex).

## 🔹 Defensiva (como proteger com Firewalls)

- **Política default deny** (bloquear tudo, liberar só o necessário).
- Regras granulares por **IP, porta e protocolo**.
- Monitoramento de logs do firewall.
- Uso de **firewall em camadas** (host-based + network-based).
- Revisão periódica das regras → evitar portas esquecidas.

---
## ​❗ Onde Firewalls entram na arquitetura de segurança

- **Na borda da rede** → protege LAN contra a Internet.
- **Internamente** → segmenta redes (ex: servidores críticos vs usuários comuns).
- **No host** → firewall pessoal (Windows Defender Firewall, UFW no Linux).

---
# Notas relacionadas:

[[Segmentação de Redes com VLANs e Firewalls]]
[[Analisando Configurações de Firewalls e Identificando Falhas]]

---