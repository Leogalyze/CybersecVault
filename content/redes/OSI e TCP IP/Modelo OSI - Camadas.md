---
title: Camadas do Modelo OSI
description: Entendendo as camadas do OSI
tags:
  - Redes
  - "#ModeloOSI_TCP/IP"
slug: camadas-modelo-osi
date: 2025-08-24
lastmod: 2025-08-24
weight: 2
---
---

# Conceito Geral

O Modelo OSI (Open Systems Interconnection) é um modelo conceitual que padroniza a comunicação entre sistemas de redes em **7 camadas**, onde cada camada executa funções específicas e se comunica apenas com as camadas adjacentes.

---
### Camada 7 - **Aplicação**

**A interface do usuário, onde os aplicativos e usuários interagem com a rede.** Onde os dados são traduzidos da sintaxe em que foram convertidos em algo que o usuário pode ler.

A camada de aplicação permite que o usuário interaja com a aplicação ou rede sempre que o usuário escolher por ler mensagens, transferir arquivos ou executar outras tarefas relacionadas à rede.

Navegadores como Chrome usam protocolos da camada de aplicação como HTTP/HTTPS. Aplicativos de e-mail como Outlook usam SMTP, POP3 ou IMAP.

---
### Camada 6 - **Apresentação**

**Lida com a tradução, criptografia e compactação de dados para garantir a compatibilidade entre diferentes sistemas.**

A camada e apresentação funciona como um tradutor de dados da rede, ele garante que as camadas de aplicação dos sistemas do receptor e do emissor sejam capazes de interpretar as informações enviadas/recebidas.

Ela pode lidar com diferentes codificações de caracteres (ex: UTF-8, ASCII).

---
* **Apresentação -> Aplicação(Receptor)**
	A camada de apresentação traduz ou formata dados para a camada de aplicação com base na semântica ou sintaxe que a aplicação aceita.

* **Apresentação(Emissor) -> Sessão**
	A camada de apresentação comprime os dados que vêm da camada de aplicativo antes de enviá-los para a Camada 5, a camada de sessão.

---
### Camada 5 - **Sessão**

**Estabelece, gerencia e encerra sessões de comunicação entre dispositivos.**

A camada de sessão estabelece a abertura e fechamento das comunicações entre dois dispositivos na rede. Esta camada garante que a sessão fique aberta tempo suficiente para que todos os dados necessários sejam enviados. Em seguida, ela fecha a sessão para evitar gastar recursos desnecessários.

Esta camada inclui a autenticação e reconexão após uma interrupção.

Protocolos como NetBIOS RPC e PPTP operam nessa camada.

Além disto, se uma grande quantidade de dados estiver sendo enviada, a camada sessão pode configurar pontos de verificação para caso a transferência seja interrompida antes da conclusão, os pontos de verificação permitem que a transmissão possa ser retomada sem precisar reiniciar do início.

---
### Camada 4 - **Transporte**

**A camada de transporte gerencia a comunicação de ponta a ponta dos dispositivos que interagem entre si, garantindo que os dados cheguem de forma confiável e na ordem correta.**

Isto envolve pegar os dados na camada sessão e dividi-los em partes chamadas de segmentos. A camada transporte no dispositivo que recebe a comunicação lida com a remontagem desses segmentos em dados que serão consumíveis pela camada sessão.

**É aqui que as comunicações selecionam os números das portas TCP para categorizar e organizar as transmissões de dados na rede.**

Nesta camada, são utilizados o Protocolo de Controle de Transmissão (TCP) e o Protocolo de Datagrama de Usuário (UDP).

TCP garante entrega e ordem. UDP é mais rápido, mas sem garantias — ideal para voz/vídeo em tempo real.

---
### Camada 3 - **Rede**

**A camada de rede concentra-se em roteamento e endereçamento lógico**, sendo o IP um protocolo comum nesta camada.

*Esta camada transforma os segmentos da camada de transporte (Camada 4) em pacotes*. A divisão dos segmentos em pacotes acontece nos dispositivo do remente e eles são remontados no dispositivo receptor.

A camada de rede é responsável por fornecer os meios para transferir pacotes de informações entre os nós conectados, por meio de uma ou mais redes.

A camada de rede também funciona como ferramenta de eficiência, ele descobre o caminho físico ideal necessário para levar os dados ao seu destino, essa função é chamada de "roteamento.

Os dispositivos utilizados nessa camada são os roteadores e alguns switches.

Do ponto de vista TCP/IP, é aqui que os endereços IP são aplicados para fins de roteamento.

Além do IP, a camada 3 também usa protocolos como ICMP (usado no comando ping).

---
### Camada 2 - **Enlace**

A camada de enlace **é responsável por criar um enlace confiável entre nós conectados diretamente**, geralmente envolvendo endereços MAC.

**Ela facilita a transferência de dados entre dois dispositivos que utilizam a mesma rede**, além de gerenciar o controle de fluxo e erros das informações.

Nesta camada os pacotes são divididos em partes chamadas de frames. Dentro dela temos duas subcamadas, ade controle de acesso à mídia (MAC) e controle de link lógico (LLC).

Esta camada também permite a transmissão de dados para a Camada 3, a camada de rede, onde são endereçados e roteados.

---
### Camada 1 - **Física**

**A camada física é o "hardware", lida com cabos, switches e a transmissão de bits.**

Ela também incluiu uma variedade de componentes como cabos, frequência de rádio usada para transmitir dados, Wi-Fi e outras estruturas físicas para transmitir dados, como pinos, tensões necessárias e tipos de portas.

Ele determina como as conexões físicas com a rede são configuradas e como os bits são representados em sinais previsíveis à medida que são transmitidos eletricamente, opticamente ou por ondas de rádio.

---
# Notas relacionadas:

[[Modelo OSI - O que é]]

---