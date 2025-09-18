---
title: Dynamic Host Configuration Protocol (DHCP) - O que é?
description: Explicando o conceito do protocolo DHCP
tags:
  - Redes
  - "#Protocolos_Rede"
slug: dhcp-conceito
date: 2025-08-29
lastmod: 2025-08-29
weight: 14
---
---
# Conceito Geral

O DHCP (Dynamic Host Configuration Protocol) é um protocolo da camada de aplicação (modelo OSI), baseado em **UDP** (porta 67 para o servidor, 68 para o cliente).  

A função dele é **atribuir automaticamente configurações de rede** a dispositivos que entram na rede, evitando que você tenha que configurar IP, máscara, gateway e DNS manualmente. 

Ele evita a necessidade de configuração manual de IP. Imagina ter que configurar 500 maquinas em um escritório, uma a uma. O DHCP faz isso de maneira automática e inteligente.

> 🧠 DHCP roda sobre **UDP**, não usa TCP.

|OSI|Camada 7 → Aplicação|
|---|---|
|Transporte|UDP|
|Portas|67 (Servidor) / 68 (Cliente)|

---
## ⚙️Funcionamento

**DORA → Discover, Offer, Request, Acknowledge**

|Etapa|Quem faz|Descrição|
|---|---|---|
|**D** → Discover|Cliente|“**Alguém aí me dá um IP?**” (Broadcast)|
|**O** → Offer|Servidor DHCP|“**Tenho esse IP disponível: 192.168.0.100.**”|
|**R** → Request|Cliente|“**Quero esse IP, por favor reserva pra mim!**”|
|**A** → Acknowledge|Servidor DHCP|“**Feito! IP 192.168.0.100 é seu.**”|

Além de **IP**, o DHCP pode entregar:

- Máscara de rede.
- Gateway padrão.
- DNS.
- Tempo de lease (duração do IP atribuído).
- Até configs mais avançadas (ex.: PXE boot).

---
---
## Análise ofensiva/defensiva

### 🔸Falhas / Ataques (como explorar)

O problema é que o DHCP **não tem autenticação nativa** → qualquer dispositivo na rede pode se passar por servidor ou cliente. Isso abre portas para vários ataques:

1. **DHCP Starvation Attack (Esgotamento de IPs)**
    - O atacante manda milhares de _requests_ falsos com MACs diferentes.
    - O servidor “empresta” todos os IPs disponíveis.
    - Resultado: clientes legítimos ficam sem IP e sem acesso à rede.
    - Ferramenta: `yersinia` ou `dhcpstarv`.

2. **Rogue DHCP Server (Servidor DHCP Malicioso)**
    - O atacante coloca um servidor DHCP falso na rede.
    - Quando o cliente pede IP, pode receber do atacante em vez do servidor legítimo.
    - O invasor pode entregar configs maliciosas, como:
        - Gateway falso (redirecionando tráfego por ele → MITM).
        - DNS malicioso (envenenamento de tráfego).
        - IP inválido (negação de serviço).
    - Ferramenta: `Ettercap`, `dhcpd` modificado, Kali Linux já tem labs disso.

3. **MITM via DHCP Spoofing**
    - Mistura dos dois ataques acima.
    - O invasor se torna o _man-in-the-middle_ colocando o tráfego para passar por ele antes de ir ao gateway real.

---
### 🔹 Defesas / Mitigação (como se proteger)

As medidas dependem se você é **admin da rede** ou apenas **usuário**:

**No lado do administrador (camada de infraestrutura):**

1. **DHCP Snooping (switches gerenciáveis)**
    - Configura quais portas do switch podem ser servidores DHCP (trusted).
    - Bloqueia qualquer DHCP Offer/ACK vindo de portas não confiáveis.

2. **Port Security**
    - Limita quantos MACs podem se registrar por porta.
    - Mitiga ataques de _starvation_.

3. **802.1X (autenticação de rede)**
    - Antes de liberar DHCP, o cliente precisa se autenticar (certificado, usuário/senha).

4. **IP Source Guard / Dynamic ARP Inspection**
    - Trabalha junto com DHCP Snooping para evitar spoofing.


**No lado do usuário/endpoint:**

- Configurar IP estático em casos críticos (não depender de DHCP).
- Monitorar logs de conexão → se aparecerem IPs estranhos de gateway/DNS, pode ser indício de ataque.
- Ferramentas de detecção (IDS/IPS, como Snort/Suricata) podem gerar alertas para pacotes DHCP anômalos.

---
## Resumo:

- DHCP é super prático, mas **sem autenticação nativa** → vulnerável a spoofing/starvation.
- Defesas eficazes estão mais na **camada de rede (switches gerenciáveis)**.
- Para pentester, é alvo clássico em redes corporativas mal configuradas.

---