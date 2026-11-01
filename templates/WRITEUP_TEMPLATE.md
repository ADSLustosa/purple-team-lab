<div align="center">

<a href="../README.md">🏠 Início</a> · <a href="./">📂 Fase</a>

# 🟣 [Título do experimento]

**[Uma frase: o que foi testado e qual foi o resultado principal.]**

![Tática](https://img.shields.io/badge/tática-Execution-c8402f?style=for-the-badge&labelColor=121312)
![Técnica](https://img.shields.io/badge/técnica-T1059.001-8b6cc9?style=for-the-badge&labelColor=121312)
![Detecção](https://img.shields.io/badge/detecção-validada-7fae45?style=for-the-badge&labelColor=121312)
![Dificuldade](https://img.shields.io/badge/nível-iniciante-3f86a8?style=for-the-badge&labelColor=121312)

</div>

> Status da detecção: `validada` (verde `7fae45`) · `parcial` (amarelo `febc2e`) · `sem cobertura` (vermelho `c8402f`)

---

## 📋 Resumo executivo

| | |
|:---|:---|
| **Objetivo** | O que este experimento quer provar |
| **Ambiente** | VMs e versões envolvidas |
| **Resultado** | Detectado? Em quanto tempo? Por qual fonte de log? |
| **Risco para o negócio** | Em linguagem não técnica: o que um atacante conseguiria |
| **Recomendação principal** | A ação de maior impacto |

---

## 🗺️ Mapeamento MITRE ATT&CK

| Tática | Técnica | Sub-técnica | Referência |
|:---|:---|:---|:---|
| Execution | Command and Scripting Interpreter | PowerShell | [T1059.001](https://attack.mitre.org/techniques/T1059/001/) |

---

## 🔴 Execução (Red)

<details open>
<summary><b>Procedimento</b></summary>

```bash
# comandos executados, com comentário explicando cada etapa
```

</details>

**Por que funciona:** fundamento técnico da técnica.

---

## 🔵 Telemetria (Blue)

| Fonte | Evento | Gerou log? | Gerou alerta? |
|:---|:---|:---:|:---:|
| Sysmon | Event ID 1 · Process Creation | ✅ | ❌ |
| Windows Security | Event ID 4688 | ✅ | ❌ |

<details>
<summary><b>Evidência bruta</b></summary>

```json
{ "log": "trecho relevante, com dados sensíveis mascarados" }
```

</details>

---

## 🛠️ Detecção

<details open>
<summary><b>Regra Sigma</b></summary>

```yaml
title: 
status: experimental
logsource:
  product: windows
  category: process_creation
detection:
  selection:
  condition: selection
level: medium
```

</details>

| Métrica | Antes | Depois |
|:---|:---:|:---:|
| Detectado | ❌ | ✅ |
| Tempo até o alerta | — | |
| Falsos positivos em 24h | — | |

---

## 🧱 Mitigação e hardening

- [ ] Ação preventiva 1
- [ ] Ação preventiva 2

---

## 🎓 Lições aprendidas

1. 
2. 

## 📚 Referências

- [MITRE ATT&CK](https://attack.mitre.org/)
