---
name: sdd
description: Master Index & Hub para a suíte de Spec-Driven Development (PRD -> MVP -> Spec -> Implement -> Validate -> Finish). Usado para gerenciar fatias e orientar o desenvolvimento com alta qualidade.
---

# /sdd — Spec-Driven Development Harness (Hub & Índice Master)

O SDD é um processo estruturado para transformar requisitos de produto em código de alta qualidade, previsível e sem sobre-engenharia em qualquer repositório.

---

## 🚀 Slash Commands Compostos Diretos

Você pode acionar cada etapa diretamente pelos comandos compostos:

* **`/sdd-plan <nome-feature>`** — Entrevista de produto e criação do PRD (`docs/prd/`) e MVP (`docs/mvp/`).
* **`/sdd-spec <fatia>`** — Criação da especificação técnica detalhada (`docs/specs/`).
* **`/sdd-implement`** — Desenvolvimento guiado de ponta a ponta (Backend + Frontend + Testes).
* **`/sdd-validate`** — Execução automatizada da bateria de validação (`tsc`, `lint`, `test`, `e2e`).
* **`/sdd-finish`** — Atualização de documentação de estado (`STATE.md`) e commit final.

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
