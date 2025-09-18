---
title: Roteamento na Pratica - Estático e Dinâmico
description: Exemplos práticos de roteamento e suas configurações
tags:
  - Redes
slug: roteamento-pratica
date: 2025-09-02
lastmod: 2025-09-02
weight: 21
---
---
# Conceito Geral

## O que é Roteamento?

Roteamento é o processo de **escolher o melhor caminho** para que pacotes de dados cheguem de uma rede a outra.

- Pode ser **manual (estático)** ou **automático (dinâmico)**.
    
- Função central dos **roteadores**.
    

---

## 📌 Roteamento Estático

- Configurado manualmente pelo administrador.
- Bom para redes pequenas, controle total.
- Pouca escalabilidade, sujeito a erros humanos.
### Exemplo

Cenário:

- Rede A → `192.168.1.0/24`
- Rede B → `192.168.2.0/24`
- Rede C → `192.168.3.0/24`

```
# No Roteador1 (rede 192.168.1.0/24):
ip route 192.168.2.0 255.255.255.0 10.0.0.2
ip route 192.168.3.0 255.255.255.0 10.0.0.6

# No Roteador2 (rede 192.168.2.0/24):
ip route 192.168.1.0 255.255.255.0 10.0.0.1
ip route 192.168.3.0 255.255.255.0 10.0.0.6
```

> Cada rota diz: **“para chegar nessa rede, use esse gateway”**.

---
## 📌 Roteamento Dinâmico

- Protocolos especializados (RIP, OSPF, BGP, EIGRP).
- Os roteadores trocam informações automaticamente.
- Escalável, resiliente, mas mais complexo.
### Exemplo com OSPF

```
router ospf 1
 network 192.168.1.0 0.0.0.255 area 0
 network 10.0.0.0 0.0.0.3 area 0
```

> O roteador anuncia suas redes → os outros aprendem sozinhos.

---
## Comparação

| Critério            | Estático             | Dinâmico                         |
| ------------------- | -------------------- | -------------------------------- |
| Configuração        | Manual               | Automática                       |
| Escalabilidade      | Baixa                | Alta                             |
| Tolerância a falhas | Baixa                | Alta                             |
| Segurança           | Simples (se fechado) | Exige autenticação de protocolos |
| Uso típico          | Redes pequenas, labs | Redes médias/grandes, ISPs       |

---
---
## Análise ofensiva/defensiva

### 🔸 Ofensiva

- **Estático**: alterar rotas no roteador → redirecionar tráfego.
- **Dinâmico**: ataques de **route injection** (ex: OSPF spoofing), redirecionando pacotes para o atacante.
### 🔹 Defensiva

- Segmentar redes críticas.
- Proteger acessos administrativos (SSH, console).
- **Autenticação em protocolos de roteamento** (MD5/HMAC).
- Monitoramento de tabelas de roteamento para detectar anomalias.

---
# Notas relacionadas:

[[Roteadores - O que são]]

---