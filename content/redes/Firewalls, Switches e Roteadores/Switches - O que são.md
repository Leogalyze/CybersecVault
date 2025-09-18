---
title: Switches - O que são ?
description: Explicando para que serve e como os Switches funcionam.
tags:
  - Redes
slug: switches-conceito
date: 2025-09-02
lastmod: 2025-09-02
weight: 19
---
---
# Conceito Geral

## O que são?

- Dispositivos de **camada 2 (Enlace)** do modelo OSI (alguns podem operar também na camada 3 – faz roteamento básico entre VLANs e sub-redes).
- Sua função principal: **receber quadros, identificar o endereço MAC de destino e encaminhar apenas para a porta correta**.
- Diferem do hub (que “grita” o tráfego para todo mundo) → switch **segmenta o tráfego**.

---
## Para que servem?

- **Organizar a rede local (LAN)**.
- **Reduzir colisões**, criando domínios de colisão separados para cada porta.
- Melhorar performance e segurança → o tráfego só vai para quem realmente precisa receber.
- Permitem configurações avançadas: VLANs, trunking, port security, QoS.

---
## Como usar (na prática)?

- Conectar hosts (PCs, impressoras, servidores) dentro da LAN.
- Criar **VLANs** para segmentar grupos de dispositivos.
- Configurar portas com regras de segurança (port security, 802.1X).
- Em redes corporativas → switches de acesso (usuários), distribuição (consolida VLANs) e core (backbone).

---
## Conceitos importantes

1. **Tabela MAC**: Switch aprende qual MAC está em qual porta.
2. **Flooding inicial**: quando não sabe o destino, envia o quadro para todas as portas (exceto a de origem).
3. **VLAN (Virtual LAN)**: divide a rede física em redes lógicas.
4. **Trunking (802.1Q)**: carrega múltiplas VLANs em uma porta.
5. **STP (Spanning Tree Protocol)**: evita loops de camada 2.

---
## Exemplos visuais de um Switch

* **Switch 8 portas (compacto)**

```
┌─────────────────────────────────────────┐
│  [PWR] [SYS]        8-Port Gigabit SW   │
│ ┌──┐ ┌──┐ ┌──┐ ┌──┐ ┌──┐ ┌──┐ ┌──┐ ┌──┐ │
│ │1 │ │2 │ │3 │ │4 │ │5 │ │6 │ │7 │ │8 │ │
│ └┬─┘ └┬─┘ └┬─┘ └┬─┘ └┬─┘ └┬─┘ └┬─┘ └┬─┘ │
│  │●   │●   │●   │○   │○   │●   │○   │○  │  (● link, ○ down)
└──┴────┴────┴────┴────┴────┴────┴────┴───┘
```

* **Switch 24 portas 1U (frontal de rack)**

```
┌───────────────────────────────────────────────────────────────────────────────┐
│ [PWR] [SYS]                     24-Port 1U Rack Switch                        │
│                                                                               │
│ [1][2][3][4][5][6][7][8]  [9][10][11][12][13][14][15][16]  [17][18][19][20]  │
│ [■■][■■][■■][■■][■■][■■][■■][■■]  [■■][■■][■■][■■][■■][■■][■■][■■]  [■■][■■] │
│ [21][22][23][24]      [SFP+ Uplink A] [SFP+ Uplink B]       [Console][MGMT]  │
└───────────────────────────────────────────────────────────────────────────────┘
Legenda: [■■] = porta RJ-45; SFP+ = uplinks de fibra; Console = serial; MGMT = porta out-of-band
```

* **Versão minimalista (ícones de porta)**

```
┌────────── Switch ──────────┐
│ PWR SYS                    │
│ ▣ ▣ ▣ ▣ ▣ ▣ ▣ ▣           │  (▣ = porta)
│ ▣ ▣ ▣ ▣ ▣ ▣ ▣ ▣           │
│ ▣ ▣ ▣ ▣ ▣ ▣ ▣ ▣  [SFP][SFP]│
└────────────────────────────┘
```

* **Topologia simples com dois hosts**

```
[Host A]───┐
           │  ┌─────────────────────────────┐
           ├──│ [1][2][3][4][5][6][7][8]   │
[Host B]───┘  │           Switch            │
              │      [SFP A]  [SFP B]      │
              └─────────────────────────────┘
                     │
                  [Roteador/Firewall]
```

---
---
# Análise ofensiva/defensiva

## 🔸 Análise Ofensiva (como atacantes exploram switches)

- **ARP Spoofing / ARP Poisoning**: falsificar MACs e enganar a tabela do switch → possibilita MITM.
- **MAC Flooding**: encher a tabela de MACs até o switch “quebrar” e começar a se comportar como hub → tráfego vaza.
- **VLAN Hopping**: exploração de má configuração de trunk/VLAN para saltar de uma rede para outra.
- **DHCP Starvation + Rogue DHCP**: saturar pool de IPs e forçar clientes a pegar IP de servidor falso.

---
## 🔹 Análise Defensiva (boas práticas em switches)

- **Port Security** → limitar quantidade de MACs por porta.
- **DHCP Snooping** → validar servidores DHCP legítimos.
- **Dynamic ARP Inspection (DAI)** → proteger contra ARP Spoofing.
- **VLANs bem configuradas** → separar tráfego de usuários, servidores, VoIP etc.
- **Trunking só quando necessário** → restringir VLANs em trunks.
- **STP ativado** → proteção contra loops.
- **Logs e monitoramento SNMP/Syslog** → detectar comportamentos estranhos.

---
## Resumindo para cibersegurança

- Switch ≠ só “caixinha que conecta PCs”.
- É o **primeiro ponto de defesa na LAN**.
- Se mal configurado → vira um playground para ataques MITM, sniffing e pivoting.
- Um analista de segurança deve entender:
    - Como funciona a tabela MAC.
    - Ataques de camada 2.
    - Ferramentas ofensivas (ex: Ettercap, Bettercap).
    - Defesas (port security, ARP inspection).

---