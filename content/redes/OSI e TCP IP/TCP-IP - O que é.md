---
title: O que é o TCP/IP
description: Conceito geral sobre TCP/IP + Camadas
tags:
  - Redes
  - "#ModeloOSI_TCP/IP"
slug: conceito-tcp-ip
date: 2025-08-24
lastmod: 2025-08-24
weight: 3
---
---
# Conceito Geral

TCP/IP (Transmission Control Protocol/Internet Protocol) é um conjunto de protocolos de comunicação usados para interconectar dispositivos de rede e permitir a troca de informações entre eles na internet. É a base da comunicação na internet e também em redes privadas.

Ele combina o Protocolo de Controle de Transmissão (TCP), responsável pela transmissão de dados, com o Protocolo de Internet (IP), que identifica os computadores e servidores.

As camadas em TCP/IP combinam funções, diferente do modelo OSI, ficando da seguinte forma:

. Camada 4 – **Aplicação**
   - Aplicação (OSI)
   - Apresentação (OSI)
   - Sessão (OSI)
. Camada 3 – **Transporte**
   * Transporte (OSI)
. Camada 2 – **Internet**
   * Rede (OSI)
. Camada 4 – **Acesso à rede**
   * Enlace de Dados (OSI)
   * Física (OSI)

O **modelo TCP/IP** pode ser descrito tanto com **4 camadas** quanto com **5 camadas** porque existem duas formas de interpretar onde fica a parte de **Aplicação/Transporte**.

---
### Camadas do TCP/IP: 

### **Camada de Aplicação**

Se refere aos programas e protocolos que o TCP/IP deve utilizar para iniciar a transmissão de dados.

Um navegador de Internet pode utilizar protocolos como o HTTP e HTTPS para realizar comunicação a partir das URLs. Um cliente de transferência de arquivos como o FileZilla, utiliza FTP. Já um serviço de e-mail usa o protocolo SMTP.

A camada de aplicação contém os protocolos que definem o tipo de serviço a ser utilizado na comunicação, como HTTP, FTP, SMTP, entre outros

---
### **Camada de Transporte (TCP)**

Se refere ao Protocolo de controle de transmissão (TCP), é o que define como os dados serão transmitidos entre as duas partes do processo.

A camada de transporte estabelece os canais de comunicação de transferência de dados.

Aqui os dados são divididos em pacotes e numerados, criando uma sequência lógica que será verificada nas camadas seguintes. Ela define para onde os dados serão enviados e a que taxa de transferência.

---
#### **Portas TCP**

O TCP usa as chamadas portas, elementos numéricos que identificam os pontos de uma transferência de dados. As portas são sempre utilizadas em conjunto com um endereço de rede (como o endereço IP).

Por serem identificadas numericamente num padrão de 16 bits, as portas vão do 0 até o 65535. Alguns números de portas são universalmente utilizados para determinados processos. Por exemplo:

| Porta | Protocolo | Nome                    | Tipo | Função                                      | Comentários                                |
|-------|-----------|-------------------------|------|---------------------------------------------|--------------------------------------------|
| 20    | FTP       | FTP - Dados             | TCP  | Transferência de dados                      | Usada com a porta 21, menos comum em FTPS  |
| 21    | FTP       | FTP - Controle          | TCP  | Comandos de controle e autenticação         | Pode ser alvo em brute force               |
| 22    | SSH       | Secure Shell            | TCP  | Acesso remoto seguro                        | Porta padrão pra pentest e pivoting        |
| 25    | SMTP      | Simple Mail Transfer    | TCP  | Envio de e-mails                            | Usada por spammers, verificação de open relays |
| 53    | DNS       | Domain Name System      | TCP/UDP | Resolução de nomes de domínio           | UDP para requisições simples, TCP para zonas |
| 80    | HTTP      | HyperText Transfer      | TCP  | Navegação web não criptografada             | Sempre alvo para exploração web            |
| 443   | HTTPS     | HTTP Secure (TLS/SSL)   | TCP  | Navegação web segura                        | Certificados, sniffing se TLS mal configurado |

Embora o TCP seja o protocolo mais utilizado na camada de transporte, outros protocolos também podem ser utilizados. Podem ser citados como exemplo o SCTP (Stream Control Transmission Protocol) e o UDP (User Datagram Protocol).

---
### **Camada de Rede (IP)**

Esta camada lida com as interfaces dos hosts e transforma os pacotes de dados em datagramas.

Cada datagrama possui dois componentes principais:

* Cabeçalho (header)
	  Contendo o endereço de IP da origem e do destino e outros dados relevantes

* Carga útil (payload)
	  Contém os dados em si que estão sendo enviados

Além do protocolo IP, a camada de rede também utiliza o protocolo ICMP (Protocolo de Mensagens de Controle da Internet), responsável por fornecer relatórios de erros às fontes de envio de dados. Desta forma, caso haja algum problema na comunicação entre os hosts, a mensagem definirá qual foi o erro ocorrido e ajustes poderão ser realizados para completar o processo de maneira bem-sucedida.

---
### **Camada de Interface**

Também chamada de enlace de dados ou ligação de dados, lida com a transferência em si dos dados entre os hosts. 

A camada de interface é responsável, entre outros aspectos, por definir como os dados serão transmitidos, seja por conexão cabeada como Ethernet ou sem fios como uma rede Wi-Fi.

---
* Aplicação lida com **Dados**
* Transporte lida com **Segmentos**
* Internet lida com **Pacotes**
* Rede lida com **Bits**

---
# Notas relacionadas:

[[OSI e TCP IP - Diferenças]]

---