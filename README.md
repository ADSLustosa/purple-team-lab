<div align="center">

<img src="assets/banner.svg" alt="Purple Team Lab — Emular · Detectar · Evoluir" width="100%"/>

<br/>

[![Status](https://img.shields.io/badge/status-em_andamento-8b6cc9?style=for-the-badge&labelColor=121312)](#trilha)
[![MITRE ATT&CK](https://img.shields.io/badge/framework-MITRE_ATT%26CK-c8402f?style=for-the-badge&labelColor=121312)](https://attack.mitre.org/)
[![Kali Linux](https://img.shields.io/badge/Kali_Linux-2026.2-3f86a8?style=for-the-badge&logo=kalilinux&logoColor=white&labelColor=121312)](https://www.kali.org/)
[![License](https://img.shields.io/badge/license-MIT-8a8f88?style=for-the-badge&labelColor=121312)](LICENSE)

**Laboratório prático e documentado de Purple Team:** executo técnicas reais de adversários em ambiente isolado,
verifico se a defesa enxerga, crio a detecção que faltava e registro cada decisão.

[🧪 Laboratório](00-lab-setup/) ·
[🗺️ Trilha](#trilha) ·
[🔁 Metodologia](#metodologia) ·
[🏗️ Arquitetura](#arquitetura) ·
[👤 Sobre mim](#sobre-mim)

</div>

---

## 🎯 Por que este repositório existe

Um teste de invasão responde *"conseguimos entrar?"*. Ele raramente responde a pergunta que mais importa para a empresa:

> **"Se um atacante real fizesse isso, nós perceberíamos?"**

Este laboratório existe para responder essa pergunta, técnica por técnica. Cada experimento aqui une os dois lados:

| 🔴 Lado ofensivo | 🔵 Lado defensivo | 🟣 Resultado |
|:---|:---|:---|
| Emular uma técnica do MITRE ATT&CK | Verificar logs, telemetria e alertas | Detecção criada, testada e documentada |
| Testar variações do mesmo procedimento | Medir tempo até a detecção | Lacunas de visibilidade mapeadas |
| Documentar o *como* e o *porquê* | Propor *hardening* e mitigação | Relatório técnico e executivo |

---

<a id="metodologia"></a>

## 🔁 Metodologia: o ciclo Purple

```mermaid
flowchart LR
    A["🔴 <b>Emular</b><br/>técnica ATT#38;CK"] --> B["🔍 <b>Observar</b><br/>gerou log?"]
    B --> C{"🚨 Alerta<br/>disparou?"}
    C -- "Não" --> D["🛠️ <b>Criar / ajustar</b><br/>detecção"]
    D --> A
    C -- "Sim" --> E["📝 <b>Documentar</b><br/>cobertura validada"]
    E --> F["🔄 Próxima<br/>variação"]
    F --> A

    style A fill:#2a1512,stroke:#c8402f,color:#f0d5cf
    style B fill:#1a1c1a,stroke:#8b6cc9,color:#e8e4da
    style C fill:#1a1c1a,stroke:#8b6cc9,color:#e8e4da
    style D fill:#122430,stroke:#3f86a8,color:#d3e7f0
    style E fill:#1d1d1b,stroke:#b9b3a3,color:#ece8de
    style F fill:#1a1c1a,stroke:#8a8f88,color:#e8e4da
```

**Princípio central:** bloquear *um* procedimento não significa estar protegido contra a *técnica*.
Por isso cada técnica é testada em mais de uma variação antes de ser considerada coberta.

---

<a id="trilha"></a>

## 🗺️ Trilha de evolução

| Fase | Módulo | Competências | Entregas | Status |
|:---:|:---|:---|:---|:---:|
| **00** | [🧪 Laboratório](00-lab-setup/) | Virtualização, redes, segmentação, integridade | Lab isolado e documentado | ![](https://img.shields.io/badge/-em_andamento-8b6cc9?style=flat-square) |
| **01** | [📡 Reconhecimento](01-recon/) | Nmap, enumeração, OSINT | Write-ups e automação de recon | ![](https://img.shields.io/badge/-planejado-3a3f39?style=flat-square) |
| **02** | [🌐 Segurança Web](02-web/) | OWASP Top 10, Burp Suite, APIs | Relatórios de pentest web | ![](https://img.shields.io/badge/-planejado-3a3f39?style=flat-square) |
| **03** | [🔵 Blue Team](03-blue/) | Sysmon, Wazuh (SIEM), análise de logs | SIEM funcional e dashboards | ![](https://img.shields.io/badge/-planejado-3a3f39?style=flat-square) |
| **04** | [🟣 Purple Team](04-purple/) | Atomic Red Team, regras Sigma | Matriz de cobertura ATT&CK | ![](https://img.shields.io/badge/-planejado-3a3f39?style=flat-square) |

<details>
<summary><b>📈 Fases avançadas (clique para expandir)</b></summary>
<br/>

| Fase | Módulo | Competências |
|:---:|:---|:---|
| **05** | 🏢 Active Directory | Kerberoasting, Pass-the-Hash, BloodHound e suas detecções |
| **06** | ⚙️ Detection Engineering | Detection-as-Code, CI/CD, Threat Hunting, automação em Python |
| **07** | 🎭 Emulação de Adversários | Planos baseados em grupos reais, Caldera, métricas e relatório executivo |

</details>

---

<a id="arquitetura"></a>

## 🏗️ Arquitetura do laboratório

```mermaid
flowchart TB
    subgraph HOST["💻 Host · Windows · Ryzen 7 5700X · 16 GB"]
        direction TB
        subgraph LAB["🔒 LabNet · 10.10.10.0/24 · Rede NAT isolada"]
            direction LR
            KALI["🐉 <b>Kali Linux</b><br/>atacante"]
            WIN["🪟 <b>Windows</b><br/>vítima · <i>fase 03</i>"]
            SIEM["📊 <b>Wazuh</b><br/>SIEM · <i>fase 03</i>"]
            WEB["🌐 <b>DVWA / Juice Shop</b><br/>alvos web · <i>fase 02</i>"]
            KALI -. ataque .-> WIN
            KALI -. ataque .-> WEB
            WIN -- logs --> SIEM
        end
    end
    LAB -- "NAT (somente saída)" --> NET(("🌍 Internet"))

    style HOST fill:#070807,stroke:#3a3f39,color:#c4bfb2
    style LAB fill:#121312,stroke:#8b6cc9,color:#e8e4da
    style KALI fill:#2a1512,stroke:#c8402f,color:#f0d5cf
    style WIN fill:#122430,stroke:#3f86a8,color:#d3e7f0
    style SIEM fill:#122430,stroke:#3f86a8,color:#d3e7f0
    style WEB fill:#2a1512,stroke:#c8402f,color:#f0d5cf
    style NET fill:#1a1c1a,stroke:#8a8f88,color:#e8e4da
```

> As máquinas marcadas com *fase* serão adicionadas conforme a trilha avança. A rede do laboratório
> **não alcança** a rede doméstica: nenhuma VM usa modo *Bridge*. Detalhes e justificativas em [`00-lab-setup`](00-lab-setup/).

---

## 🧰 Stack

<div align="center">

**Ofensivo**<br/>
![Kali](https://img.shields.io/badge/Kali_Linux-3f86a8?style=flat-square&logo=kalilinux&logoColor=white)
![Nmap](https://img.shields.io/badge/Nmap-4a6fa5?style=flat-square)
![Burp Suite](https://img.shields.io/badge/Burp_Suite-ff6633?style=flat-square&logo=burpsuite&logoColor=white)
![Metasploit](https://img.shields.io/badge/Metasploit-2596cd?style=flat-square)

**Defensivo**<br/>
![Wazuh](https://img.shields.io/badge/Wazuh-3f86a8?style=flat-square)
![Sysmon](https://img.shields.io/badge/Sysmon-0078d4?style=flat-square)
![Sigma](https://img.shields.io/badge/Sigma_Rules-8b6cc9?style=flat-square)

**Infraestrutura e automação**<br/>
![VirtualBox](https://img.shields.io/badge/VirtualBox-183a61?style=flat-square&logo=virtualbox&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776ab?style=flat-square&logo=python&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4eaa25?style=flat-square&logo=gnubash&logoColor=white)
![Git](https://img.shields.io/badge/Git-f05032?style=flat-square&logo=git&logoColor=white)

</div>

---

## 📂 Estrutura do repositório

<details>
<summary><b>Ver árvore de diretórios</b></summary>

```text
purple-team-lab/
├── 00-lab-setup/     🧪 Montagem do laboratório e decisões de arquitetura
├── 01-recon/         📡 Reconhecimento e enumeração
├── 02-web/           🌐 Segurança de aplicações web
├── 03-blue/          🔵 Telemetria, SIEM e análise de logs
├── 04-purple/        🟣 Emulação ATT&CK e engenharia de detecção
├── templates/        📝 Modelos padronizados de write-up
└── assets/           🎨 Banners, diagramas e evidências
```

</details>

Todo experimento segue o mesmo [modelo de write-up](templates/WRITEUP_TEMPLATE.md): **objetivo → mapeamento ATT&CK → execução → telemetria → detecção → mitigação → lições aprendidas**.

---

<a id="sobre-mim"></a>

## 👤 Sobre mim

<table>
<tr>
<td width="68%" valign="top">

**João Pedro Lustosa** · Fortaleza, CE 🇧🇷

Coordenador de TI em ambiente industrial e desenvolvedor front-end (React · TypeScript),
pós-graduando em **Segurança da Informação** e em **Direito Digital e Proteção de Dados (LGPD)**.

Minha vantagem é enxergar o sistema inteiro: **como ele é construído** (desenvolvimento),
**como ele roda** (infraestrutura, redes, servidores) e **como precisa ser protegido** (segurança e conformidade).
Este laboratório é onde essas três visões se encontram na prática.

</td>
<td width="32%" valign="top">

**🎯 Áreas de interesse**
- Purple Team e Detection Engineering
- Application Security (AppSec)
- Segurança de ambientes industriais (OT)
- GRC e Proteção de Dados

</td>
</tr>
</table>

<div align="center">

[![LinkedIn](https://img.shields.io/badge/LinkedIn-adslustosa-0a66c2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/adslustosa)
[![GitHub](https://img.shields.io/badge/GitHub-ADSLustosa-24292f?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ADSLustosa)

</div>

---

## ⚖️ Aviso ético e legal

> [!WARNING]
> Todo o conteúdo deste repositório foi produzido em **ambiente próprio e isolado** ou em plataformas que
> **autorizam expressamente** os testes (como TryHackMe, HackTheBox e PortSwigger Academy).
> As técnicas aqui documentadas têm finalidade **exclusivamente educacional e defensiva**.
> Utilizá-las contra sistemas sem autorização formal é crime no Brasil (Lei nº 12.737/2012 · art. 154-A do Código Penal).

<div align="center">
<br/>
<sub>🟣 Construído com método, documentado com propósito.</sub>
</div>
