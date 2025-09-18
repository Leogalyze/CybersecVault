---
title: Address Resolution Protocol (ARP) - O que é?
description: Explicando o conceito, falhas e defesas sobre o protocolo de rede ARP
tags:
  - Redes
  - "#Protocolos_Rede"
slug: arp-conceito
date: 2025-08-29
lastmod: 2025-08-29
weight: 13
---
---
# Conceito Geral

O **ARP** é um protocolo de camada **2,5 (entre Enlace e Rede)** que serve para **mapear endereços IP (lógicos) em endereços MAC (físicos)** dentro de uma rede local.

ARP basicamente serve para descobrir um endereço MAC desconhecido de um endereço IP conhecido. Após utilizar

---
## ⚙️ Funcionamento

1. Um host sabe o **IP** de destino (ex: 192.168.1.10), mas não sabe o **MAC**.
2. Ele envia uma **ARP Request** em broadcast na rede perguntando:
    > "Quem tem o IP 192.168.1.10?"
3. O host dono do IP responde com uma **ARP Reply**, informando seu MAC.
4. O host solicitante guarda essa relação IP ↔ MAC na **ARP Cache** (memória temporária) para não precisar perguntar sempre.

Sem ARP, máquinas em uma LAN não conseguiriam se comunicar de forma direta usando apenas IPs.

---

| Etapa       | Acontecimento                                |
| ----------- | -------------------------------------------- |
| ARP Request | Broadcast: "Quem tem IP `X.X.X.X`?"          |
| ARP Reply   | Unicast: "Eu, IP `X.X.X.X`, meu MAC é Y:Y:Y" |
| Cache       | Dispositivo guarda IP ↔️ MAC na tabela ARP   |
### Exemplo de ARP Request:

- **Operação:** Request
- **Remetente IP:** `192.168.0.105`
- **Remetente MAC:** `11:22:33:44:55:66`
- **Destino IP:** `192.168.0.1`
- **Destino MAC:** `00:00:00:00:00:00` (não sabe ainda)
- Mensagem: **"Quem tem `192.168.0.1`? Me responda!"

### Exemplo de ARP Reply

- **Operação:** Reply
- **Remetente IP:** `192.168.0.1`
- **Remetente MAC:** `AA:BB:CC:DD:EE:FF`
- **Destino IP:** `192.168.0.105`
- **Destino MAC:** `11:22:33:44:55:66`
- Mensagem: **"Eu tenho `192.168.0.1`, meu MAC é `AA:BB:CC:DD:EE:FF`."

---
### Próximo passo após a resolução ARP

1. **Host A quer falar com Host B**
    - Ele sabe o **IP** do destino (ex: `192.168.1.20`).
    - Ele usou o ARP para descobrir que o **MAC** correspondente é `aa:bb:cc:dd:ee:ff`.

2. **Encapsulamento no modelo OSI**
    - Camada 3 (Rede): cria um pacote **IP** com origem/destino (`192.168.1.10 → 192.168.1.20`).
    - Camada 2 (Enlace): encapsula esse pacote IP dentro de um **quadro Ethernet**, usando:
        - **MAC de origem:** `11:22:33:44:55:66` (do Host A)
        - **MAC de destino:** `aa:bb:cc:dd:ee:ff` (descoberto pelo ARP)

3. **Transmissão na rede local**
    - O quadro Ethernet é enviado pelo cabo/Wi-Fi.
    - Switches usam o **endereço MAC de destino** para encaminhar o quadro até o host correto.

4. **Receptor (Host B)**
    - A camada 2 recebe o quadro, vê que o **MAC de destino é o dele**, e aceita o pacote.
    - Entrega para a camada 3, que vê o **IP de destino**, processa e responde.

Esse processo se repete sempre que necessário. O ARP só entra em cena **quando não há entrada no cache**. Depois que já temos o MAC, a comunicação segue fluindo normalmente via **Ethernet + IP**.

---
---
## Análise ofensiva/defensiva

### 🔸 Falhas / Ataques (como podem ser explorados)

O ARP **não tem autenticação nem verificação de integridade**. Isso abre a porta para ataques:

1. **ARP Spoofing / Poisoning**
    - O atacante envia respostas ARP falsas, associando **seu MAC a um IP que não é dele** (por exemplo, o gateway).
    - Resultado: o tráfego passa a ir para o atacante.
    - Pode levar a **MITM (Man-in-the-Middle)**, sniffing, modificação de pacotes, ou DoS.

2. **DoS por ARP Flooding**
    - O invasor envia milhares de pacotes ARP falsos para **encher a cache** das vítimas.
    - Isso gera instabilidade e pode travar dispositivos de rede.

3. **Redirecionamento de tráfego**
    - O atacante “se apresenta” como o gateway (default gateway).
    - Assim, todo tráfego para fora da rede passa primeiro por ele → perfeito para sniffing credenciais.

4. **Pivoting em pentest**
    - Em redes internas, o pentester usa ARP Spoofing para interceptar pacotes e escalar acesso lateralmente.

Ferramentas comuns: **arpspoof, ettercap, Bettercap, Cain & Abel**.

---
### 🔹 Defesas / Mitigação (como se proteger)

1. **ARP Inspection / Segurança em switches**
    - **DAI (Dynamic ARP Inspection)** nos switches Cisco: valida ARP Replies com base em tabelas confiáveis (DHCP Snooping).
    - Bloqueia pacotes falsos.

2. **Uso de ARP estático**
    - Configurar manualmente IP ↔ MAC em máquinas críticas (ex: gateway, servidores).
    - Pouco escalável em redes grandes, mas útil em ambientes sensíveis.

3. **Ferramentas de detecção**
    - **arpwatch, XArp**: monitoram mudanças na ARP Table e alertam sobre spoofing.
    - SIEM pode correlacionar logs de anomalias ARP.

4. **Segmentação de rede**
    - VLANs reduzem a superfície de ataque → atacante só consegue envenenar quem está na mesma broadcast domain.

5. **Uso de IPv6 (ND com segurança)**
    - Em IPv6 o ARP foi substituído por NDP (Neighbor Discovery Protocol), que tem extensões de segurança (SEND).
    - Ainda tem problemas, mas menos trivial que o ARP do IPv4.

---
## **Resumo:**

- ARP = "Qual IP tem esse MAC?"
- Vulnerável porque **acredita em qualquer resposta**.
- Ataque clássico = **ARP Spoofing** → MITM, sniffing, DoS.
- Defesa = **DAI, monitoramento, tabelas estáticas, segmentação**.

---