---
title: Segmentação de Redes com VLANs e Firewalls
description: Como VLANs são usadas na prática para segmentação, junto com roteadores/firewalls.
tags:
  - Redes
slug: segmentacao-redes-vlans
date: 2025-09-03
lastmod: 2025-09-03
weight: 24
---
---
# Conceito Geral

## O que é

- **Segmentação de redes** é o processo de **dividir uma rede em partes menores e isoladas**, cada uma com **regras e controles próprios**.
- Combinando **VLANs (separação lógica)** + **Firewalls (controle de tráfego)**, criamos **camadas de defesa** que dificultam a movimentação de um atacante.

---
## Como funciona

1. **Switches criam VLANs** → isolam grupos de dispositivos (ex.: usuários, servidores, convidados).
2. **Roteadores ou Firewalls fazem o roteamento entre VLANs** → decidem quem pode falar com quem.
3. **ACLs ou regras de firewall** aplicam políticas de segurança → bloqueiam tráfego desnecessário ou suspeito.

---
## Por que segmentar?

- **Segurança**: limita o alcance de ataques (ex.: malware em uma VLAN não atinge toda a rede).
- **Conformidade**: exigência de normas (ex.: PCI-DSS obriga separar redes de pagamento).
- **Controle**: regras diferentes para setores distintos (ex.: visitas não acessam rede administrativa).
- **Performance**: menos broadcast circulando em toda a rede.

---
## Exemplos práticos

### Cenário 1 → Empresa com três redes principais

- VLAN 10: Financeiro
- VLAN 20: RH
- VLAN 30: TI
- VLAN 99: Guest

Firewall define:

- Financeiro acessa somente servidores contábeis.
- RH acessa sistema de ponto, mas não banco de dados financeiro.
- TI acessa tudo, mas com log e monitoramento.
- Guest só tem acesso à internet.

---
### Cenário 2 → DMZ (Zona Desmilitarizada)

- **DMZ VLAN**: Servidores web e e-mail (visíveis à internet).
- **LAN VLAN**: Rede interna dos colaboradores.
- **Firewall**:
    - Permite internet → DMZ (http/https, smtp).
    - Bloqueia internet → LAN.
    - Permite DMZ → LAN **apenas portas específicas** (ex.: servidor web acessando banco).

---
---
# Análise ofensiva/defensiva

## 🔸 Análise Ofensiva (Ataques)

- **Pivoting limitado**: se a segmentação for mal configurada, atacante consegue saltar de uma VLAN a outra.
- **Firewall mal configurado**: portas abertas demais permitem movimentação lateral.
- **VLAN hopping**: já citado, ainda é vetor comum se não houver boas práticas.
- **Ataques de interconexão**: se DMZ ou VLAN de servidores não tiver regras rígidas, atacante acessa banco de dados via servidor web comprometido.

---
## 🔹 Análise Defensiva (Boas Práticas)

- **Definir zonas de segurança**: separar rede corporativa, servidores, IoT, convidados, gestão.
- **Aplicar ACLs e Firewalls entre VLANs**: permitir só o mínimo necessário.
- **Criar VLAN de Guest isolada**: visitantes só acessam internet, nunca a rede interna.
- **Monitorar tráfego entre zonas**: uso de IDS/IPS ou SIEM para detectar anomalias.
- **Defense in Depth**: segmentação é só uma das camadas → precisa ser combinada com autenticação forte, monitoramento e patches.

---
## Resumo:

* Segmentação via VLANs + Firewalls é uma das armas mais eficazes contra **movimentação lateral** de atacantes. 
* Quem domina isso consegue criar **zonas de segurança robustas**, reduzindo impacto de invasões e malware.

---
# Notas relacionadas:

[[VLANs (Virtual Local Area Networks) - O que são]]
[[Firewall - O que é]]

---