---
title: Cyber Kill Chain
description: Descrevendo a Cyber Kill Chain
tags:
  - "#Threat_Landscape"
lastmod: 2025-09-30
date: 2025-09-30
weight: 28
---
---
# # Cyber Kill Chain

O **Cyber Kill Chain** é um framework desenvolvido pela Lockheed Martin que descreve as etapas de um ataque cibernético.  
Ele ajuda analistas a **entender, detectar e interromper** ataques em diferentes fases do ciclo de invasão.

---

## Etapas do Cyber Kill Chain

1. **Reconhecimento (Reconnaissance)**  
   O atacante coleta informações sobre o alvo, como endereços IP, domínios, portas abertas, serviços ativos e usuários.
   * OSINT, redes sociais, sites.

3. **Armas (Weaponization)**  
   Criação de ferramentas maliciosas, como malware ou exploits, que serão usados para explorar vulnerabilidades.
   * Malware, exploit, documento infectado.

4. **Entrega (Delivery)**  
   O vetor inicial do ataque: e-mail de phishing, sites maliciosos, mídias removíveis, entre outros.
   * Phishing, USB, sites comprometidos

5. **Exploração (Exploitation)**  
   O código malicioso é executado, explorando falhas de software, configurações inseguras ou credenciais fracas.

6. **Instalação (Installation)**  
   O atacante estabelece persistência no sistema (ex.: backdoors, trojans, web shells).

7. **Comando e Controle (C2)**  
   Comunicação entre o sistema comprometido e a infraestrutura do atacante, permitindo controle remoto.

8. **Ações sobre o Objetivo (Actions on Objectives)**  
   Execução do propósito final do ataque: roubo de dados, ransomware, sabotagem, espionagem ou movimentação lateral na rede.

---
## Por que é importante?

- Defensores podem identificar em qual fase um ataque está e agir rapidamente.  
- Facilita a criação de controles de segurança em múltiplas camadas.  
- Ajuda na resposta a incidentes, criando pontos de detecção e mitigação.

---
## Críticas e Limitações

- Modelo linear: ataques reais podem pular etapas ou segui-las em ordem diferente.  
- Foco em ameaças externas: ataques internos ou avançados podem não seguir o fluxo.  
- Complementa, mas não substitui, outros frameworks como o MITRE ATT&CK.

---
## Resumindo

O Cyber Kill Chain é um **guia estratégico**: mostra como o atacante age e como o defensor pode **quebrar a corrente** em qualquer etapa para evitar que o ataque chegue ao objetivo final.

---
# Fonte de conteúdo

* https://tryhackme.com/room/cyberkillchainzmt
* https://hackersec.com/o-que-e-cyber-kill-chain/
* https://training.fortinet.com/course/view.php?id=40558

---


