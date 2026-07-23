---
name: sdd
description: Master Index & Hub para a suíte de Spec-Driven Development (PRD -> MVP -> Spec -> Implement -> Validate -> Finish | Audit). Usado para gerenciar fatias e orientar o desenvolvimento com alta qualidade.
---

# /sdd — Spec-Driven Development Harness (Hub & Índice Master)

O SDD é um processo estruturado para transformar requisitos de produto em código de alta qualidade, previsível e sem sobre-engenharia em qualquer repositório.

---

## 🚀 Slash Commands Compostos Diretos

Você pode acionar cada etapa diretamente pelos comandos compostos:

* **`/sdd-plan <nome-feature>`** — Entrevista de produto lapidada e criação do PRD (`docs/prd/`) e MVP fatiado (`docs/mvp/`).
* **`/sdd-spec`** — Mapeamento holístico de arquitetura e geração das specs base de **todas as fatias** (`docs/specs/`).
* **`/sdd-implement`** — Criação da branch (`feat/...`), commit dos docs, PR Draft e desenvolvimento e2e sequencial de ponta a ponta (Backend + UI + Testes).
* **`/sdd-validate`** — Execução automatizada da bateria de qualidade (`tsc`, `lint`, `test`, `e2e` se houver UI).
* **`/sdd-finish`** — Geração da Spec Final pós-implementação (*as-built*), atualização de estado (`STATE.md`), commit final, push e merge.
* **`/sdd-audit`** — Auditoria holística do repositório (Lean code, consistência SDD/STATE.md e gaps de testes).

---

## 📁 Estrutura de Artefatos Gerados no Projeto Local

```text
<raiz-do-projeto>/
└── docs/
    ├── prd/
    │   └── PRD-<feature>.md
    ├── mvp/
    │   └── MVP-<feature>.md
    └── specs/
        └── spec-<feature>-fatia-XX.md
```
