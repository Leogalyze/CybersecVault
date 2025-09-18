---
title: Virtual Local Area Networks (VLANs) - O que são?
description: Entendendo VLANs na teoria e como elas funcionam
tags:
  - Redes
slug: vlan-conceito
date: 2025-09-03
lastmod: 2025-09-03
weight: 23
---
---
# Conceito Geral

## O que são

- **VLAN (Virtual LAN)** é uma forma de **segmentar logicamente uma rede** dentro de um switch.
- Permite dividir uma rede física em várias redes lógicas.
- Permite que dispositivos que **não estão fisicamente próximos** sejam agrupados como se estivessem na mesma rede local.
- Cada VLAN funciona como uma **rede independente** → mesmo switch pode hospedar várias redes isoladas.

---
## Como funcionam

- Cada porta de um switch pode ser associada a uma VLAN específica.
- O switch marca os quadros Ethernet com um **tag VLAN (IEEE 802.1Q)** indicando a qual VLAN aquele tráfego pertence.
- Quando um frame (quadro) sai de uma máquina, o switch **tagueia** esse frame com um identificador chamado **VLAN ID**.
- Esse tag vai no protocolo **802.1Q** (padrão VLAN).
- Comunicação entre diferentes VLANs só ocorre via **roteador** ou **firewall** (Inter-VLAN Routing).

>O tráfego de uma VLAN **não se comunica** com outra VLAN, a não ser que tenha um roteamento intermediário, geralmente via roteador ou **Switch Layer 3 (Roteamento entre VLANs).**

---
## Para que servem

- **Isolamento de tráfego** (segurança): impede que todos os dispositivos estejam no mesmo broadcast domain.
- **Organização lógica**: separar setores da empresa (Financeiro, RH, TI, Visitantes).
- **Performance**: reduz broadcasts desnecessários em toda a rede.
- **Gerenciamento**: facilita aplicar políticas específicas a determinados grupos de máquinas.

---
## Exemplos práticos

### Exemplo 1:

- **Empresa com três setores**:
    - VLAN 10 → Financeiro
    - VLAN 20 → Recursos Humanos
    - VLAN 30 → TI
- Funcionários de RH não conseguem acessar diretamente servidores do Financeiro sem passar pelo firewall.
- Visitantes conectam-se em uma **VLAN de Guest isolada**, sem acesso aos ativos internos.

### Exemplo 2:

Imagina uma oficina:

|Setor|VLAN|IP|Descrição|
|---|---|---|---|
|Recepção|10|192.168.10.0/24|Atendimento ao cliente|
|Oficina|20|192.168.20.0/24|Ferramentas, impressoras|
|Administrativo|30|192.168.30.0/24|Gestão, financeiro|
|Visitantes|40|192.168.40.0/24|Wi-Fi separado e isolado|

- A VLAN 40 (visitantes) **não acessa** a VLAN do administrativo (30).
- Se quiser que alguém da recepção acesse uma impressora na oficina (VLAN 20), o roteamento entre VLANs é configurado.

---
## Termos comuns:


| Termo           | Descrição                                                 |
| --------------- | --------------------------------------------------------- |
| **Access Port** | Porta que conecta um dispositivo a uma VLAN específica.   |
| **Trunk Port**  | Porta que carrega múltiplas VLANs entre switches.         |
| **VLAN ID**     | Número que identifica uma VLAN (0-4095, padrão até 4094). |
| **802.1Q**      | Protocolo usado para tagueamento de VLAN.                 |
| **Native VLAN** | VLAN padrão usada quando o tráfego não tem tag.           |

---
## Resumo:

VLANs são **ferramentas poderosas de segmentação lógica**. Para cibersegurança, você precisa dominar **como configurá-las corretamente**, pois erros simples viram brechas para VLAN hopping e sniffing.

* Segurança: Separa setores (Financeiro, Administrativo, Operacional, Visitantes, IoT, Câmeras, etc.).  
* Organização: Melhora o gerenciamento da rede.  
* Performance: Reduz broadcast — menos ruído na rede.  
* Escalabilidade: Facilita expansão, reorganização e manutenção.

---
---
# Análise ofensiva/defensiva

## 🔸 Análise Ofensiva (Ataques)

- **VLAN Hopping**: explorar má configuração para acessar outra VLAN indevidamente.
    - _Switch Spoofing_: atacante configura interface como trunk e passa para outra VLAN.
    - _Double Tagging_: envia pacotes com duas tags VLAN, enganando o switch.
- **Sniffing inter-VLAN**: se o isolamento não estiver bem configurado, é possível capturar tráfego de outras VLANs.
- **Pivoting**: uma vez em uma VLAN, atacante pode tentar saltar para outra para expandir acesso.

---
## 🔹 Análise Defensiva (Boas Práticas)

- **Desabilitar portas trunk não utilizadas**.
- **Configurar VLAN nativa exclusiva** (e não usar VLAN 1).
- **Port Security**: limitar número de dispositivos por porta.
- **Separar VLANs sensíveis** (ex.: servidores, VoIP, gestão de rede).
- **Firewalls e ACLs**: controlar tráfego entre VLANs de forma rígida.

---
# Notas relacionadas:

[[Segmentação de Redes com VLANs e Firewalls]]

---