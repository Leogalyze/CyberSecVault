---
title: Wireshark
description: Wireshark - O que e
tags:
  - "#Ferramentas"
lastmod: 2025-10-01
date: 2025-10-01
weight: 29
---
---
# Conceito geral

Wireshark é um analisador de pacotes (packet sniffer) de rede, usado para capturar e inspecionar o tráfego de dados que passa por uma rede. Ele permite observar os detalhes de cada pacote, desde o endereço IP até o conteúdo das camadas de aplicação. Ideal para investigação de incidentes, validação de detecções e análise forense de rede.

---
## Para que serve

* Análise de tráfego: entender o que está acontecendo na rede.
* Depuração de rede: identificar problemas de conexão, lentidão ou falhas em protocolos.
* Segurança e pentest: detectar tentativas de ataque, tráfego suspeito ou malware.
* Aprendizado e laboratório: estudar protocolos como TCP, HTTP, DNS, etc., em detalhes.

---
## Como usar

1. Captura de pacotes
* Selecione a interface de rede (ex.: Wi-Fi ou Ethernet).
* Clique em Start Capturing Packets.
* O Wireshark começa a capturar todo o tráfego que passa pela interface selecionada.

2. Filtragem de pacotes
Para não perder se perde no excesso de dados, use filtros:
* Por IP: ip.addr == 192.168.0.10
* Por protocolo: tcp, udp, http, dns
* Por porta: tcp.port == 80
* Expressão combinada: ip.src == 192.168.0.10 && tcp.port == 443

3. Análise
* Cada linha é um pacote capturado.
* Clique no pacote para ver detalhes:
 * Camada física: Ethernet
 * Camada rede: IP
 * Transporte: TCP/UDP
 * Aplicação: HTTP, DNS, SMTP, etc.

4. Estatísticas
* Vá em Statistics para visualizar:
 * Protocol Hierarchy: quantidade de pacotes por protocolo.
 * Conversations: quem se comunica com quem.
 * Endpoints: IPs presentes na captura.
 * IO Graphs: gráficos de tráfego por tempo.

---
## Dicas importantes

* Capturar apenas o necessário: grandes redes geram milhões de pacotes rapidamente.
* Salvar capturas: use .pcap ou .pcapng para análise posterior.
* Modo promíscuo: permite capturar pacotes que não são destinados à sua máquina.
* Segurança: não capture tráfego em redes alheias sem permissão — é ilegal.
* Laboratórios: combine Wireshark com VMs ou máquinas de teste para estudar ataques ou protocolos.

---
## Exemplo prático

1. Capture pacotes enquanto você abre um site no navegador.
2. Filtre por HTTP: http.
3. Analise requisições e respostas, observe headers, códigos de status e URLs.
4. Tente filtrar apenas tráfego de um IP específico, ou apenas pacotes TCP.

---