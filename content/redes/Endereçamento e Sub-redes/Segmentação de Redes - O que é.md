---
title: Segmentação de Redes - O que é
description: Explicando o conceito de dividir uma rede maior em redes menores
tags:
  - Redes
  - "#Enderecamento_SubRedes"
slug: segmentacao-redes
date: 2025-09-02
lastmod: 2025-09-02
weight: 17
---
---
# Conceito Geral

- **Segmentar uma rede** = dividir uma rede maior em redes menores (sub-redes).
- Cada sub-rede funciona como um **bairro dentro da cidade**, ainda conectado, mas com **fronteiras bem definidas**.
- Pode ser feita em:
    - **Camada 3 (Rede):** via subnets (máscaras de sub-rede, VLANs).
    - **Camada 2 (Enlace):** via switches e VLANs.

---
## 1. Por que segmentar?

### a) Segurança

- Isolar departamentos → se o RH for atacado, o Financeiro não é afetado.
- Facilita aplicação de **firewalls, ACLs e políticas específicas**.

### b) Performance

- Menos **tráfego de broadcast** → a rede não fica “poluída”.
- Mais eficiência no roteamento.

### c) Organização

- Empresas grandes → cada setor tem sua própria sub-rede.
- Facilita controle de endereços IP e troubleshooting.

### d) Escalabilidade

- Planejamento de crescimento → evita bagunça de IPs no futuro.

---
## 2. Exemplos práticos

### Exemplo 1 - Rede simples em uma empresa

Rede original: `192.168.0.0/24`

- Todos os dispositivos (financeiro, TI, RH, impressoras) na mesma rede.
- Problemas: muito broadcast, pouca segurança.

**Segmentando:**

- `192.168.0.0/26` → Financeiro (62 hosts)
- `192.168.0.64/26` → RH (62 hosts)
- `192.168.0.128/26` → TI (62 hosts)
- `192.168.0.192/26` → Impressoras (62 hosts)

Agora cada setor está isolado → ataque de ransomware no RH não derruba o Financeiro.

---
### Exemplo 2 - VLANs em um switch

- VLAN 10 → Rede de usuários.
- VLAN 20 → Rede de servidores.
- VLAN 30 → Rede de impressoras.
- Roteador ou switch de camada 3 interliga VLANs → só o tráfego permitido passa entre elas.

---

### Exemplo 3 - Segurança ofensiva (pentest)

- Sem segmentação: se o atacante entra na rede via um host vulnerável, consegue **escaneamento lateral fácil** (pivoting).
    
- Com segmentação: atacante fica preso na sub-rede → precisa quebrar regras adicionais para avançar.
    

---

## 3. Ferramentas/Comandos úteis

- `ipcalc` → calcular sub-redes.
- `ping` → testar se sub-redes diferentes se comunicam.
- `traceroute` → visualizar caminho entre segmentos.
- `nmap` → mapear hosts em sub-redes diferentes.

---
## **Resumo:**  
Segmentação é dividir para **conquistar controle**: mais segurança, melhor performance e redes mais organizadas.

- **Sem segmentação** → uma invasão se espalha rápido.
- **Com segmentação** → o dano é contido e a rede fica mais eficiente.

---
---
# Análise ofensiva/defensiva

## ​🔸 Uso Ofensivo (Atacante / Pentester)

- **Pivoting lateral mais difícil**
    
    - Se a rede não for segmentada → basta comprometer uma máquina e já é possível escanear toda a rede interna.
        
    - Com segmentação → atacante precisa quebrar **barreiras adicionais** (ACL, firewall, VLAN hopping).
        
- **Ataques direcionados a segmentação**
    
    - **VLAN hopping** → técnicas para sair da VLAN atribuída e acessar outra.
        
    - **Sniffing malicioso** → em rede mal segmentada, o atacante consegue capturar broadcasts de outros segmentos.
        
    - **Bypass de ACLs** → se regras de firewall entre sub-redes forem mal configuradas, dá para explorar serviços internos não protegidos.
        
- **Reconhecimento limitado**
    
    - Segmentação reduz a **superfície de ataque visível**.
        
    - Atacante precisa usar mais engenharia social ou exploração de credenciais para saltar de uma rede para outra.
        

---

## 🔹 Uso Defensivo (Blue Team / SOC / Arquiteto)

- **Contenção de incidentes**
    - Malware em uma sub-rede não se propaga automaticamente para todas as máquinas da empresa.
    - Ajuda em estratégias de **Zero Trust**.
- **Menor superfície de ataque**
    - Serviços críticos (banco de dados, AD, servidores de backup) ficam em segmentos separados → não expostos para todos os hosts.
- **Monitoramento mais eficaz**
    - Tráfego entre segmentos precisa passar por **roteador/firewall** → ponto ótimo para monitorar logs, regras IDS/IPS e SIEM.
- **Aplicação de políticas específicas**
    - Ex: VLAN de convidados sem acesso à rede interna.
    - Segmentos críticos só acessíveis via jumpbox/VPN.

---

## Exemplo prático comparando

**Rede única /24 (sem segmentação):**

- Atacante invade uma máquina → com um `nmap 192.168.0.0/24` descobre todos os serviços da empresa.

**Rede segmentada em /26 (com firewall e VLANs):**

- Atacante invade uma máquina no RH.
- Só consegue enxergar hosts da rede RH.
- Para chegar no Financeiro, precisa quebrar regras de firewall → aumenta chance de ser detectado.

---
## **Resumo:**

- **Ofensivo:** segmentação mal feita = brecha (VLAN hopping, ACLs fracas).
- **Defensivo:** segmentação bem feita = contenção, monitoramento e menor superfície de ataque.

---
# Notas relacionadas:

[[Cálculo de Sub-redes com CIDR]]

---