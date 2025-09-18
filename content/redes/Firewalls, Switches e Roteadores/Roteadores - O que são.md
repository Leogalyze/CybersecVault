---
title: Roteador - O que é ?
description: Resumo curto do que a nota aborda.
tags:
  - Redes
slug: roteador-conceito
date: 2025-09-02
lastmod: 2025-09-02
weight: 20
---
---
# Conceito Geral

## O que são?

- Função: Interligar **redes diferentes** e rotear pacotes entre elas.
- Dispositivos de **camada 3 (Rede) do modelo OSI**.
- Responsáveis por **encaminhar pacotes** entre redes diferentes.
- Fazem uso de **endereços IP** e **tabelas de roteamento** para decidir o melhor caminho.
- Diferente dos switches (que conectam hosts dentro da mesma rede), os roteadores **conectam redes distintas**.

---
## Funções principais

- **Encaminhar pacotes** entre redes locais e externas.
- **Interligar LANs e WANs**.
- **Escolher rotas** com base em tabelas de roteamento.
- **Traduzir endereços** (NAT/PAT → conectar rede privada com internet).
- **Filtrar tráfego** (ACLs, controle básico de pacotes).

---
## Como usar (na prática de redes)

- Configurar **endereços IP em interfaces** (ex: `GigabitEthernet0/0`).
- Definir **rotas estáticas** ou **usar protocolos de roteamento dinâmico** (RIP, OSPF, BGP).
- Ativar **NAT/PAT** para dar acesso à Internet a redes privadas.
- Aplicar **ACLs (Access Control Lists)** para controlar quem acessa o quê.

---
## Tipos de roteamento

- **Estático** → admin define manualmente cada rota (mais controle, menos flexível).
- **Dinâmico** → protocolos trocam rotas automaticamente (mais adaptável, usado em redes grandes).
- **Padrão (default route)** → rota de saída quando não conhece o destino.

---
---
# Análise ofensiva/defensiva

## 🔸 Análise Ofensiva (Ataques em cima de roteadores)

- **Configurações fracas ou padrão** → credenciais default, portas abertas (Telnet, HTTP sem TLS).
- **Ataques de roteamento**:
    - _Route injection_ → inserir rotas falsas em protocolos dinâmicos (ex: OSPF spoofing).
    - _BGP hijacking_ → redirecionar tráfego global da Internet.
- **DoS/DDoS** → sobrecarregar a tabela de roteamento.
- **Exploração de firmware vulnerável** → acesso root ao roteador.
- **Pivoting** → usar o roteador comprometido como ponto de entrada para atacar a rede interna.

---
## 🔹 Análise Defensiva (Mitigação e boas práticas)

- **Trocar senhas padrão** e usar **SSH/HTTPS** no lugar de Telnet/HTTP.
- **Atualizar firmware** regularmente.
- **Aplicar ACLs** para limitar acesso administrativo.
- **Segregar planos**:
    - _Data plane_ (dados de usuários),
    - _Control plane_ (protocolos de roteamento),
    - _Management plane_ (administração).
- **Protocolos seguros de roteamento** (OSPFv3 com autenticação, BGP com TTL Security e RPKI).
- **Monitoramento e logging** → detectar rotas estranhas ou tráfego suspeito.

---
## Resumo:

- Roteadores **conectam redes diferentes** e **decidem o caminho do tráfego**.
- Ofensivamente → alvo crítico para manipulação de tráfego ou espionagem.
- Defensivamente → precisam de hardening (ACLs, updates, protocolos seguros).

---
# Notas relacionadas:

[[Roteamento na Prática - Estático e Dinâmico]]

---