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
* **`/sdd-implement`** — Governança na 1ª execução (branch `feat/...`, commit dos docs, PR Draft) e implementação **fatia a fatia** (uma fatia por execução, commit na PR) de ponta a ponta (Backend + UI + Testes). Repita até a última fatia.
* **`/sdd-validate`** — Execução automatizada da bateria de qualidade (`tsc`, `lint`, `test`, `e2e` se houver UI).
* **`/sdd-finish`** — Geração da Spec Final pós-implementação (*as-built*), atualização de estado (`STATE.md`), commit final, push e **squash-merge** da PR.
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

---

## 📚 Referências Globais
- [Template de PRD](references/prd-template.md)
- [Template de MVP](references/mvp-template.md)
- [Template de Spec](references/spec-template.md)
- [Guia do Workflow](references/workflow-guide.md)
- [Guia Ponytail de Código Enxuto](references/ponytail-guide.md)
