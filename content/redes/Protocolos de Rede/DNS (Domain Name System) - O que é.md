---
title: Domain Name System (DNS) - O que é?
description: Conceito geral do DNS
tags:
  - Redes
  - "#Protocolos_Rede"
slug: dns-conceito
date: 2025-08-29
lastmod: 2025-08-29
weight: 12
---
---
# Conceito Geral

- **Função:** Traduz nomes de domínio legíveis por humanos (ex: `google.com`) em endereços IP que os computadores entendem (ex: `142.250.190.14`).

- **Estrutura:** É hierárquico e distribuído, não existe um servidor único que sabe tudo. Ele segue essa ordem:
    
    1. **Root (.)** → servidores raiz.
    2. **TLD (.com, .org, .br, etc.)** → top-level domain servers.
    3. **Autoritativo** → servidor do dono do domínio (quem define o IP).
    4. **Recursivo/Resolver** → geralmente do seu provedor (ISP) ou configurado no sistema (Google DNS 8.8.8.8, Cloudflare 1.1.1.1).

- **Exemplo prático (resolução):**  
    Você digita `www.exemplo.com`:
    
    1. Seu PC pergunta ao **resolver**.
    2. O resolver, se não tiver no cache, consulta os servidores raiz.
    3. Vai para o TLD (`.com`).
    4. Vai para o autoritativo do `exemplo.com`, que responde com o IP real.
    5. O resolver guarda no **cache** (TTL) e devolve para você.

---
## Termos importantes:

| Termo             | Explicação simples                                                                         |
| ----------------- | ------------------------------------------------------------------------------------------ |
| **DNS Resolver**  | O primeiro servidor que teu PC pergunta (geralmente o do roteador ou do Google: `8.8.8.8`) |
| **Zona DNS**      | Onde estão registrados os nomes de um domínio                                              |
| **Registro A**    | Nome → IP v4                                                                               |
| **Registro AAAA** | Nome → IP v6                                                                               |
| **Registro MX**   | Registro de e-mail                                                                         |
| **Cache DNS**     | Memória temporária com IPs já resolvidos                                                   |

---
---
# Análise ofensiva/defensiva

## 🔸 **Ofensiva (como atacante pode usar o DNS legitimamente):**

- Fazer **enumeração DNS** para mapear a infraestrutura da vítima: subdomínios (`mail.empresa.com`, `vpn.empresa.com`, etc.).
- Usar ferramentas como `nslookup`, `dig`, `dnsenum`, `amass`.
- Procurar registros específicos:
    - `MX` (email) → pode indicar provedor de e-mail.
    - `TXT` → usado em SPF/DKIM/DMARC (às vezes mal configurados).
    - `SRV` → serviços como VoIP ou AD.

## 🔹 **Defensiva (uso normal do time de segurança):**

- Administrar e proteger o DNS autoritativo da empresa.
- Usar **DNS filtering** (bloquear domínios maliciosos conhecidos).
- Monitorar logs DNS no SOC para detectar tráfego estranho (exfiltração de dados, conexões para C2).

---

## ⚔️ Vulnerabilidades e ataques

Aqui é onde DNS vira um campo de guerra. Principais ataques:

1. **DNS Spoofing / Cache Poisoning**
    - O atacante insere respostas falsas no cache do resolver, redirecionando usuários para sites falsos.
    - Exemplo: você digita `banco.com` → em vez do IP real, vai para o IP do atacante.

2. **DNS Hijacking**
    - Alteração das configurações de DNS do usuário (ex: via malware ou roteador comprometido).
    - Faz com que todo o tráfego vá para um servidor DNS malicioso.

3. **DNS Amplification (DDoS)**
    - Abusa do protocolo UDP (que não tem handshake) para fazer ataques de reflexão/amplificação.
    - Atacante envia requisições pequenas com IP forjado (da vítima), servidores DNS mandam respostas enormes para a vítima.

4. **Zone Transfer (AXFR) mal configurada**
    - Se o servidor autoritativo permite transferência de zona sem restrição, atacante baixa toda a lista de subdomínios.
    - Ferramenta: `dig axfr dominio.com @servidor`.

5. **Tunneling DNS**
    - Transformar requisições/respostas DNS em um canal de comunicação oculto (para bypassar firewalls).
    - Exfiltração de dados ou acesso remoto via DNS.
    - Ferramentas: `iodine`, `dnscat2`.

6. **Typosquatting e Homograph Attacks**
    - Registrar domínios parecidos (`g00gle.com`, `micros0ft.net`) para phishing.
    - Também existe homograph usando caracteres Unicode (`аррӏе.com` em vez de `apple.com`).

---
## 🛡️ Defesa e Mitigação

🔐 **Boas práticas para proteger DNS:**

1. **DNSSEC (Domain Name System Security Extensions)**
    - Adiciona **assinatura digital** nas respostas DNS → impede spoofing/cache poisoning.

2. **Restrições de Zone Transfer**
    - Permitir AXFR só entre servidores autorizados.

3. **Monitoramento de Logs DNS**
    - Detectar acessos a domínios estranhos (exfiltração, C2).
    - Integração com SIEM (Splunk, ELK, Wazuh).

4. **Configuração segura de resolvers**
    - Usar `unbound` ou `bind` bem configurados.
    - Bloquear recursão em servidores que não devem servir ao público.

5. **Proteção contra DDoS**
    - Anycast (Cloudflare, Google DNS).
    - Limitar respostas a queries suspeitas.
6. **Treinamento de usuários**
    - Prevenir phishing de typosquatting/homograph.

---
