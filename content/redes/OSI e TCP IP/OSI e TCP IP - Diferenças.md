---
title: OSI e TCP IP - Diferença entre modelos
description: Explicando as diferenças entre os dois modelos.
tags:
  - Redes
  - "#ModeloOSI_TCP/IP"
slug: osi-tcpip-diferencas
date: 2025-08-27
lastmod: 2025-08-27
weight: 4
---
---

# Conceito Geral

O modelo OSI com suas 7 camadas é um guia teórico para a compreensão da comunicação de rede. Já o TCP/IP, que possui 4 camadas, é o esqueleto das redes modernas.

Diferente do modelo OSI, o TCP/IP combina funções; por exemplo, a camada de aplicação no modelo OSI corresponde a três camadas no TCP/IP, uma fusão que proporciona a eficiência operacional.

| Modelo OSI                          | Modelo TCP/IP                                                          |
| ----------------------------------- | ---------------------------------------------------------------------- |
| 7 camadas                           | 4 ou 5 camadas                                                         |
| Modelo teórico                      | Modelo prático                                                         |
| Sessão e Apresentação independentes | Incluídas na camada Aplicação                                          |
| Física e Enlace independentes       | Independentes (5 camadas) ou incluídas na camada de Acesso (4 camadas) |

---
![[Pasted image 20250609123633.png]]

---

**Resumo rápido:**

> OSI ensina como pensar.  
> TCP/IP mostra como acontece.

## **Principais diferenças importantes pra frisar**

|Tema|Modelo OSI|Modelo TCP/IP (5 camadas)|
|---|---|---|
|**Origem**|ISO (teórico)|DARPA/DoD (prático)|
|**Nº de camadas**|7|4 ou 5|
|**Camadas Aplicativas**|Aplicação, Apresentação, Sessão|Tudo incluído em Aplicação|
|**Foco**|Clareza conceitual|Implementação funcional|
|**Transporte**|TCP ou UDP|TCP ou UDP|
|**Uso real**|Referência para ensino|Base da internet moderna|

## **Por que o OSI ainda é usado se o TCP/IP domina?**

Porque o OSI ajuda a **diagnosticar, categorizar e entender ataques, falhas e protocolos**. Ele te dá um mapa mental detalhado. No dia a dia de cibersegurança — **especialmente no Red Team ou no SOC** — você consegue:

- **Mapear ataques por camada** (ex: ataque DDoS na camada 3 ou 4, phishing na camada 7).
    
- **Analisar logs com contexto** ("essa falha é de transporte ou de aplicação?").
    
- **Pensar modularmente**: cada camada tem funções, responsabilidades e ferramentas específicas.

## Dica de raciocínio para entrevistas e provas

> “Apesar de o TCP/IP ser o modelo implementado, o modelo OSI oferece uma visão mais detalhada e modular, o que facilita a análise técnica, a modelagem de ameaças e a segmentação de responsabilidades em cibersegurança.”

---
# Notas relacionadas:

[[Modelo OSI - O que é]]
[[TCP-IP - O que é]]

---