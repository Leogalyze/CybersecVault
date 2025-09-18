---
title: Internet Control Message Protocol (ICMP) - O que é ?
description: Explicando o conceito geral do protocolo de rede ICMP
tags:
  - Redes
  - "#Protocolos_Rede"
slug: icmp-conceito
date: 2025-08-28
lastmod: 2025-08-28
weight: 9
---
---
# Conceito geral

ICMP (Internet Control Message Protocol) é um protocolo da camada **Rede** (Modelo OSI) ou da camada **Internet** (Modelo TCP/IP).

Usado para comunicar problemas com a transmissão de dados e diagnósticas problemas na rede.

Ele não serve para transferir dados de usuário como o TCP/UDP, mas sim para **enviar mensagens de controle, diagnóstico e erro** entre dispositivos.

---
## Tipos de mensagens ICMP

| Tipo | Nome                    | Função                               |
| ---- | ----------------------- | ------------------------------------ |
| 0    | Echo Reply              | Resposta ao ping                     |
| 3    | Destination Unreachable | Mostra que o destino não é acessível |
| 8    | Echo Request            | Requisição de ping                   |
| 11   | Time Exceeded           | TTL expirou (usado em traceroute)    |

- **Echo Request / Echo Reply (tipo 8 e 0)** → usados pelo **ping**.
- **Destination Unreachable (tipo 3)** → informa que o host/rede/porta não pode ser alcançado.
- **Time Exceeded (tipo 11)** → usado pelo **traceroute**, indica que o TTL do pacote expirou.
- **Redirect (tipo 5)** → informa um melhor caminho para o roteamento.

---
## Ferramentas que usam ICMP

- **ping** → mede tempo de resposta e verifica se um host está ativo.

- **traceroute** → descobre o caminho (roteadores) entre você e o destino.

- **pathping / mtr** → misto de ping + traceroute.

---
## Exemplo Prático:

**Ping:**

* No CMD: ``ping 8.8.8.8``
* Você vai ver algo assim: ``64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=20.5 ms``

**Tradução**:

-  64 bytes chegaram de volta
-  Isso foi a resposta (Echo Reply)
-  time = latência
-  ttl = tempo de vida restante do pacote

---
## ICMP na Segurança

O ICMP é útil, mas também pode ser explorado:

- **Ping flood / ICMP flood** → ataque DoS enviando pings em massa.
- **Ping of Death** → pacotes ICMP malformados que travavam sistemas antigos.
- **ICMP tunneling** → usado para **exfiltração de dados** escondendo informações dentro de mensagens ICMP (bypassa firewalls mal configurados).

Por isso, em ambientes corporativos:

- ICMP geralmente é **controlado** ou **filtrado** (permitindo apenas tipos específicos).

---
## Resumindo

- ICMP não carrega dados de aplicação, mas mensagens de controle.

- Trabalha junto com o IP, sem portas.

- Serve para diagnóstico e erros de rede.

- Muito usado em **ping** e **traceroute**.

- Precisa ser monitorado, pois pode ser explorado em ataques.

---
---
## Análise ofensiva/defensiva

### 1. Uso legítimo

- **Função**: Protocolo de mensagens de controle e diagnóstico, encapsulado no IP (protocolo nº 1).
- **Principais usos**:
    - **Ping** (Echo Request/Reply) → verificar conectividade e latência.
    - **Traceroute** (Time Exceeded) → mapear o caminho dos pacotes até o destino.
    - Mensagens de erro (Destination Unreachable, Redirect).

---

### 2. Análise ofensiva (como atacantes exploram o ICMP)

- **Ping Sweep** → varredura para descobrir quais hosts estão ativos em uma rede.
- **ICMP Flood** → ataque DoS enviando grande volume de pacotes.
- **Smurf Attack** → uso de broadcast + spoofing de IP para amplificação de tráfego.
- **ICMP Tunneling** → esconder tráfego (exfiltração de dados) dentro de pacotes ICMP, burlando firewalls.
- **Fingerprinting via TTL** → ICMP pode revelar o SO do alvo (diferença no TTL padrão, tamanho de resposta, etc.).

---
### 3. Análise defensiva (mitigação e monitoramento)

- **Hardening**:
    - Desabilitar resposta a ICMP Echo em hosts críticos (ou limitar a apenas hosts internos).
    - Bloquear ICMP Redirect (pode ser abusado para MITM).

- **Mitigação**:
    - Configurar firewalls para permitir apenas tipos de ICMP necessários (ex.: Destination Unreachable, Fragmentation Needed).
    - Rate limiting → limitar requisições ICMP por segundo.

- **Monitoramento**:
    - SIEM/NIDS → gerar alertas em caso de varredura ICMP (muitos Echo Requests).
    - Detectar padrões suspeitos de tunelamento (ICMP com payloads incomuns ou muito grandes).

---
### 4. Lab prático (pra você treinar 🚀)

1. **Captura básica**
    - Use `ping` entre duas VMs (Windows ↔ Linux).
    - Capture no **Wireshark** e analise os pacotes Echo Request/Reply.

2. **Bloqueio de ICMP**
    - No Linux, use `ufw deny icmp` (ou regra iptables).
    - Teste o ping novamente e veja o comportamento.

3. **Varredura ICMP**
    - Use `nmap -sn 192.168.0.0/24` → descobre hosts ativos só com ICMP.

4. **Flood controlado**
    - Use `hping3 --icmp -i u100 192.168.0.10` para simular flood.
    - Observe consumo de CPU no destino.

---
### 5. Insight de carreira

- **Em SOC/Blue Team**: você deve saber diferenciar "host realmente offline" de "host que não responde a ICMP".
- **Em Pentest/Red Team**: ICMP é um dos primeiros passos no reconhecimento (descobrir hosts vivos).
- **Em entrevista técnica**: pode cair algo como:
    > “O ping não respondeu. Isso significa que o servidor está desligado?”  
    > Resposta correta: **não necessariamente, pode estar ativo mas protegido por firewall/ACL bloqueando ICMP.**

---
# Notas relacionadas:

[[Ping - O que é]]

---