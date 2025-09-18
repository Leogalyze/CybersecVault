---
title: HTTP e HTTPS - o que é e suas diferenças
description: Explicando os protocolos HTTP e HTTPS e suas diferenças
tags:
  - Redes
  - "#Protocolos_Rede"
slug: http-https-conceito
date: 2025-08-29
lastmod: 2025-08-29
weight: 11
---
---
# Conceito Geral

Ambos são **protocolos da camada de aplicação** (OSI camada 7), usados para trocar dados entre cliente (navegador, curl, burp, etc.) e servidor web.

---
## Comparação direta

| Protocolo | Porta | Segurança                                 | Vulnerabilidade principal                                 |
| --------- | ----- | ----------------------------------------- | --------------------------------------------------------- |
| HTTP      | 80    | Nenhuma                                   | Dados em texto puro (sniffing, MITM)                      |
| HTTPS     | 443   | Criptografia + Integridade + Autenticação | Má config. de TLS, certificados falsos, ataques avançados |

---
⚔️ Em termos de **pentest ofensivo**, você (como Red Team) exploraria:

- Em HTTP → sniffar credenciais, injetar conteúdo, capturar cookies.
- Em HTTPS → checaria configurações fracas, testaria downgrade, exploraria servidores desatualizados (OpenSSL vulnerável, por exemplo).

🛡️ Em **defesa (Blue Team/SOC)**, você buscaria:

- Forçar HTTPS sempre.
- Detectar tráfego não criptografado.
- Monitorar certificados e alertar sobre uso de protocolos/cifras fracas.

---
## HTTP (HyperText Transfer Protocol)

### ⚙️ Funcionamento

- Protocolo de comunicação da **camada de aplicação** (OSI → Camada 7).
- Baseado em **requisição-resposta** entre cliente (navegador) e servidor.
- Exemplo:
    - Cliente → `GET /index.html`
    - Servidor → retorna HTML do site.
- **Texto puro**: os dados trafegam **sem criptografia** (login, senha, cookies, etc. viajam “abertos” pela rede).
- Usa normalmente a **porta 80**.

### 🔸 Vulnerabilidades / Ataques

1. **Sniffing** → tráfego pode ser capturado com Wireshark, tcpdump, etc.
2. **MITM (Man-in-the-Middle)** → atacante intercepta/edita requisições e respostas.
3. **Session Hijacking** → roubo de cookies de sessão.
4. **Phishing** → sites falsos usando HTTP podem enganar usuários.
5. **Data Tampering** → como não há integridade, o conteúdo pode ser alterado em trânsito.

### 🔹 Defesa / Mitigação

- Evitar uso de HTTP em sites que envolvam dados sensíveis.
- Forçar redirecionamento para **HTTPS**.
- Implementar **segurança em transporte** (VPN, TLS, HSTS).

---
## HTTPS (HyperText Transfer Protocol Secure)

### ⚙️ Funcionamento

- É o HTTP + **TLS (Transport Layer Security)**.
- Traz **3 pilares principais**:
    1. **Confidencialidade** → criptografia dos dados (AES, etc.).
    2. **Integridade** → impede alteração do tráfego em trânsito.
    3. **Autenticação** → via **certificado digital SSL/TLS** emitido por uma Autoridade Certificadora (CA).
- Normalmente na **porta 443**.
- Exemplo: quando você acessa seu banco ou Gmail, está sob HTTPS.

### 🔸 Vulnerabilidades / Ataques

1. **Configuração fraca de TLS**
    - Uso de versões antigas (SSLv2, SSLv3, TLS 1.0/1.1).
    - Cifras fracas (RC4, DES).
    - Ataques como **POODLE**, **BEAST**, **Heartbleed**, **CRIME**.
2. **Certificados inválidos/falsos**
    - MITM com certificado autoassinado enganando usuários.
    - CA comprometida emitindo certificados falsos.
3. **Downgrade Attack**
    - Forçar a conexão a cair de HTTPS → HTTP.
4. **Mixed Content**
    - Site HTTPS que carrega scripts ou imagens via HTTP.
5. **Phishing ainda existe**
    - HTTPS não significa “site confiável”, apenas que a conexão é criptografada.

### 🔹 Defesa / Mitigação

- Usar **TLS 1.3** sempre que possível.
- Habilitar apenas **cifras fortes** (AES-GCM, ChaCha20).
- Implementar **HSTS (HTTP Strict Transport Security)** para impedir downgrade/HTTP.
- Monitorar validade e integridade dos certificados.
- Segurança de aplicação (mesmo sob HTTPS, ainda existe risco de **SQLi, XSS, CSRF**, etc.).

---
## Resumo:  
**HTTP é como mandar uma carta sem envelope.**  
**HTTPS é mandar dentro de um envelope lacrado, mas se o lacre for frágil ou falso, ainda dá ruim.**

---