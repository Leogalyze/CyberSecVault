---
title: Nmap
description: Nmap - O que e
tags:
  - "#Ferramentas"
lastmod: 2025-10-01
date: 2025-10-01
weight: 30
---
---
# Conceito Geral

Nmap (Network Mapper) é uma ferramenta open‑source para descoberta de redes e auditoria de segurança.

Usos principais:
* Descobrir hosts ativos numa rede (network discovery).
* Identificar portas abertas e serviços (port scanning + service discovery).
* Detectar versões de serviços e SO (fingerprinting).
* Rodar scripts automatizados para enumeração e detecção de vulnerabilidades (NSE — Nmap Scripting Engine).
* Gerar evidências (saídas em vários formatos) para relatórios e integração com outras ferramentas.

---
## Conceitos essenciais

- **Open**: porta aceita conexões (serviço escutando).
- **Closed**: porta respondendo, mas sem serviço.
- **Filtered**: probe não recebeu resposta — possivelmente bloqueada por firewall/ACL.
- **SYN scan (-sS)**: “stealth” — só envia SYN, observa resposta (requer privilégios root para raw sockets).
- **Connect scan (-sT)**: usa o stack do SO para abrir conexão completa (sem privilégios root).
- **UDP scan (-sU)**: mais lento e ruidoso; importante para serviços sem TCP.
- **OS detection (-O)** e **version detection (-sV)**: tentam identificar SO e versão de serviços.
- **NSE scripts (--script)**: automação para tarefas (enumeração, brute forcing, checagem de vulnerabilidades, etc).

---
## Comandos práticos

1. **Scan rápido de portas comuns** 
```
   nmap -T4 --top-ports 1000 -oN quick.txt alvo.com
   ```
* `-T4` = timing agressivo para redes não muito instáveis; `--top-ports` = portas mais comuns; `-oN` = output normal.

2. SYN scan + version + OS + scripts “default”
```
   sudo nmap -sS -sV -O -sC -T4 -p- -oA fullscan alvo
   ```
   * `-p-` = todas as portas TCP (1-65535); `-oA` = grava em Nmap normal, XML e grepable; `-sC` = scripts default.

3. Scan UDP (lento)
   ```
   sudo nmap -sU -p 53,67,69,123,161 alvo
   ```

4. Scan stealth para evitar detecção (não infalível)
   ```
   sudo nmap -sS -T2 -p22,80,443 alvo
   ```

5. Pular host discovery (quando firewall bloqueia ICMP/pings)
   ```
   nmap -Pn -p22,80 alvo
   ```

6. Usar scripts para checar vulnerabilidades específicas
   ```
   nmap --script vuln alvo
   ```

   ou

   ```
   nmap --script ssl-enum-ciphers -p 443 alvo
   ```

7. Escanear grandes redes rápido (varredura inicial com masscan + nmap)
   * Use `masscan` para descobrir portas muito rápido, depois `nmap` para detalhes. (Masscan gera lista de IP/ports para nmap).

8. Exportar resultado legível e para integração. ```
```
nmap -sV -oX resultado.xml alvo   # XML para ferramentas e parsing
nmap -sV -oG resultado.gnmap alvo # formato grepable 
``` 
   

---
## Principais opções

- `-sS` — SYN scan (stealth)
- `-sT` — TCP connect (sem privilégios)
- `-sU` — UDP scan
- `-sV` — version detection
- `-O` — OS detection
- `-A` — aggressive (sV + OS + scripts + traceroute) — **use com cuidado**
- `-p` — especificar portas (ex: `-p 22,80,1-1024` ou `-p-` todas)
- `-Pn` — assume host está up (pula ping)
- `-T<0-5>` — timing template (T0 muito lento — T5 muito rápido e ruidoso)
- `--script <categoria|nome>` — rodar scripts NSE (`default`, `discovery`, `vuln`, `auth`, etc)
- `-oN/-oX/-oA/-oG` — formatos de saída (normal, XML, all, grepable)
- `--reason` — mostra razão para status da porta (replied RST/ICMP etc)
- `--open` — mostra apenas portas abertas

---
## Nmap Scripting Engine (NSE)

- Permite scripts Lua para tarefas como enumeração, brute force, discovery, e checagem de vulns.
- Categorias comuns: `auth`, `brute`, `default`, `discovery`, `exploit`, `intrusive`, `vuln`.
- Exemplo: `nmap --script smb-vuln* -p445 alvo` (scripts que checam SMB vulnerabilidades).

**Atenção**: scripts `intrusive`/`exploit` podem causar danos ou crashes — só em laboratório/escopo autorizado.

---
# Interpretação básica de saída

- `22/tcp open ssh` → serviço SSH escutando na porta 22
- `80/tcp filtered http` → firewall bloqueando probes (sem resposta)
- `MAC Address: ... (Vendor)` → pode indicar fabricante do dispositivo

Dica: sempre correlacione `service/version` com banner e evidências (scripts, banners HTTP, etc).

---
## Boas práticas e tuning

- Em redes de produção, **peça permissão escrita** antes de escanear.
- Use `-T3` ou menor em redes sensíveis; `-T4/T5` só em labs ou redes controladas.
- Use `--min-rate`/`--max-rate` para controlar taxa de pacotes em varreduras grandes.
- Combine `-oX` com ferramentas como `xsltproc` ou com parsers para gerar relatórios.
- Atualize Nmap e scripts (`nmap --script-updatedb` pode ajudar dependendo da instalação).

---
## Ferramentas complementares que vale conhecer

- **Masscan** — scan muito rápido em larga escala (usa depois nmap para verificação).
- **Zenmap** — GUI para Nmap (bom para aprendizado/visualização).
- **grep/awk/xsltproc** — processar saídas.
- **Nmap‑Parser** (Python/Perl libs) — para automatizar relatórios.

---
# Aviso legal e ética

**Nunca** execute Nmap contra redes/hosts sem autorização explícita. Scans podem disparar IDS/IPS e gerar incidentes legais. Em contextos profissionais, tenha escopo por escrito.

---