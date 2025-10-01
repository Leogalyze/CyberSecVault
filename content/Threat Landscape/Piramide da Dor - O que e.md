---
title: Pirâmide da Dor
description: Conceito geral da pirâmide da dor
tags:
  - "#Threat_Landscape"
lastmod: 2025-09-28
date: 2025-09-28
weight: 27
---
---
# Conceito Geral

A pirâmide da dor (Pyramid of Pain) é um modelo conceitual criado por David Bianco, muito usado em cibersegurança para classificar indicadores de comprometimento (Indicators of Compromise - IoCs) com base no custo ou "dor" que eles causam a um atacante quando são detectados e bloqueados. O termo "dor" se refere ao esforço que o atacante precisa fazer para mudar suas táticas e ferramentas.

![Pirâmide da Dor](images/img_ThreatLandscape/img_PiramideDaDor/01.png)
A Pirâmide da Dor consiste em sete níveis, do mais fácil ao mais difícil para os atacantes mudarem:

* **Valores de hash** : assinaturas de arquivo exclusivas (por exemplo, SHA1, MD5) que os invasores podem modificar facilmente recompilando malware

* **Endereços IP:** locais de rede que os invasores podem alterar rapidamente trocando de servidores

* **Nomes de domínio** : mais caros do que IPs para substituir, mas ainda administráveis ​​para adversários determinados

* **Artefatos de rede:** padrões observáveis ​​no tráfego, como estruturas de URI ou agentes de usuário incomuns

* **Artefatos do host:** evidências deixadas em endpoints, como chaves de registro, caminhos de arquivo ou processos

* **Ferramentas:** Software de ataque (por exemplo, Mimikatz, Cobalt Strike) que requer esforço significativo para substituir

* **TTPs:** (Táticas, Técnicas, Procedimentos): Os padrões comportamentais do atacante — os mais dolorosos de mudar

---
## Hash de arquivo (Hash Values)

* Trivial

Na base da pirâmide. O hash é uma "impressão digital" única de um arquivo malicioso. É muito fácil para o atacante mudar um hash. Basta fazer uma pequena alteração no arquivo para gerar um novo hash e a defesa quebra. Detectar e bloquear por hash é o nível de "dor" mais baixo para o adversário.

## Endereço de IP (IP Addresses)

* Facíl

Um pouco acima do hash. Um atacante pode facilmente usar VPNs, proxies, ou servidores comprometidos para mudar seu endereço de IP. Bloquear um IP pode deter um ataque por um tempo, mas não afeta a capacidade geral do adversário.

Do ponto de vista da defesa, o conhecimento dos endereços IP utilizados por um adversário pode ser valioso. Uma tática de defesa comum é bloquear, rejeitar ou negar solicitações de entrada de endereços IP no seu parâmetro ou firewall externo . Essa tática geralmente não é infalível, pois é fácil para um adversário experiente se recuperar simplesmente usando um novo endereço IP público.

## Nomes de domínio (Domain Names)

* Simples

Um nível de dor intermediário. Mudar um nome de domínio é um pouco mais trabalhoso que mudar um IP. O atacante precisa registrar um novo domínio, configurá‑lo e direcionar o tráfego para ele. Bloquear domínios pode ser eficaz, mas o atacante pode simplesmente usar outro.

**Punycode** é um esquema de codificação que transforma caracteres que não pertencem ao conjunto ASCII (como letras acentuadas ou alfabetos não latinos) em uma sequência compatível com ASCII. Isso permite que nomes de domínio escritos com caracteres especiais sejam representados por servidores e softwares que só entendem ASCII. Na prática, domínios internacionalizados (IDNs) usam Punycode por baixo dos panos para que navegadores e servidores os processem.

Invasores exploram isso criando domínios que **visualmente parecem legítimos**, mas na verdade usam caracteres parecidos de outro alfabeto ou combinações estranhas, quando convertidos para Punycode aparecem como `xn--…` na forma técnica. Um usuário desatento pode ver algo que parece ser `exemplo.com` na barra do navegador, quando na realidade parte das letras vêm de outro alfabeto e o domínio é diferente. Isso facilita phishing e redirecionamento para sites maliciosos.

## Artefatos de rede (Network)

* Irritante

Subindo na pirâmide. Inclui elementos como padrões de tráfego, strings em pacotes de rede ou a forma como a comunicação é estabelecida. Mudar esses artefatos exige que o atacante altere a maneira como sua ferramenta de ataque se comunica, o que é mais custoso do que simplesmente mudar um IP ou domínio.

Artefatos do host são rastros ou observáveis ​​que os invasores deixam no sistema, como valores de registro, execução de processos suspeitos, padrões de ataque ou IOCs (Indicadores de Comprometimento), arquivos descartados por aplicativos maliciosos ou qualquer coisa exclusiva da ameaça atual.

## Ferramentas (Tools)

* Desafiador

Um nível de dor alto. As ferramentas são os programas ou scripts que o atacante usa (como um software de ransomware, um keylogger, etc.). Desenvolver ou adaptar uma ferramenta para evitar a detecção é algo que requer tempo, habilidade e recursos, tornando este um nível de dor significativo. Se você consegue detectar e bloquear a ferramenta em si, está causando um grande problema para o adversário.

O método Fuzzy Hashing é uma arma poderosa contra ferramentas do invasor, usado para determinar a similaridade entre os arquivos. 

O invasor provavelmente desistirá de tentar invadir sua rede ou voltará e tentará criar uma nova ferramenta com o mesmo propósito.

## Táticas, técnicas e procedimentos (TTPs)

* Difícil

O topo da pirâmide e o nível de dor mais alto. Os TTPs descrevem a "receita" do ataque: como o adversário se move dentro de uma rede, como ele eleva privilégios, como ele se mantém persistente, etc. Mudar os TTPs é a coisa mais difícil para um atacante, pois exige uma mudança fundamental na sua metodologia. Se uma equipe de defesa consegue detectar e responder a ataques baseados em TTPs, ela está realmente causando um impacto e forçando o adversário a repensar toda a sua operação.

Isso inclui toda a Matriz MITRE ATT&CK , que abrange todas as etapas tomadas por um adversário para atingir seu objetivo, desde tentativas de phishing até persistência e exfiltração de dados.

---
# CTEM e AEV

Hoje, esse modelo desempenha um papel fundamental na defesa baseada em ameaças , especialmente à medida que as organizações adotam o **Gerenciamento Contínuo de Exposição a Ameaças (CTEM)** e utilizam a **Validação de Exposição Adversarial (AEV)** para validar as exposições. Ao direcionar os indicadores corretos, as equipes de segurança podem interromper as operações dos adversários e comprovar a eficácia do controle de segurança em todos os níveis.

| Tipo de indicador     | Impacto estratégico                                                                                                                                       | Como validar com AEV                                                                                                    |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Valores de hash       | Oferece valor mínimo a longo prazo, pois os invasores podem facilmente recompilar malware para alterar hashes                                             | Implante arquivos maliciosos conhecidos para validar recursos de antivírus (AV) e detecção e resposta de endpoint (EDR). |
| Endereços IP          | Cria interrupções temporárias, mas requer atualização constante à medida que os invasores rotacionam a infraestrutura                                      | Simule conexões com IPs maliciosos para testar regras de firewall e sistema de prevenção de intrusão (IPS).             |
| Nomes de domínio      | Mais disruptivo que IPs; força os adversários a registrar novos domínios e atualizar seu malware                                                         | Teste proxies da web e filtragem de DNS por meio de domínios maliciosos.                                                |
| Artefatos de rede     | Exige que os invasores modifiquem seus métodos de comunicação e protocolos de comando e controle                                                         | Emule padrões de tráfego suspeitos e protocolos de comando e controle.                                                  |
| Artefatos do host     | Aumenta significativamente os custos ao forçar os invasores a modificar sua pegada nos sistemas alvo                                                     | Crie arquivos benignos imitando comportamentos de malware para validação de EDR.                                        |
| Ferramentas           | Quando bloqueado, exige que os adversários invistam no desenvolvimento ou aquisição de ferramentas personalizadas                                       | Use ferramentas comuns de invasores em um laboratório para validar alertas e controle.                                   |
| TTPs                  | Alvo de maior valor que força a reformulação completa do ataque quando detectado e bloqueado                                                            | Execute cadeias de ataque completas mapeadas para MITRE ATT&CK para testar a postura de segurança holística.            |

---
# Fonte de conteúdo

* https://tryhackme.com/room/pyramidofpainax
* https://www.attackiq.com/glossary/pyramid-of-pain-2/
* https://www.picussecurity.com/resource/glossary/what-is-pyramid-of-pain