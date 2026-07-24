---
name: sdd
description: Guardião de sessão e máquina de checkpoints do fluxo SDD, ciente de múltiplas worktrees. Após um /clear (ou contexto perdido), enumera as worktrees, reconstrói onde cada programa parou lendo docs/, specs e Git, e resume as sessões apontando qual comando rodar em qual pasta. Também serve de índice master da suíte.
---

# /sdd — Guardião de Sessão & Máquina de Checkpoints (Multi-Worktree)

O `/sdd` reconstrói o estado do fluxo **Spec-Driven Development** a partir dos artefatos em disco e do Git, permitindo **retomar exatamente de onde cada sessão parou** — típico após um `/clear` com o contexto apodrecido. Como o desenvolvimento pode acontecer em **várias git worktrees em paralelo** (uma feature por worktree), o `/sdd` trata **cada worktree como uma sessão independente** e resume a frota inteira.

É read-only: **detecta, reporta e recomenda** o próximo comando e o **local correto** (pasta da worktree) para executá-lo; nunca executa a próxima etapa nem troca de pasta sem sua confirmação.

---

## 🧭 Passos de Execução (Reconstrução de Checkpoints)

1. **Enumerar as worktrees (a frota):**
   - Roda `git worktree list --porcelain` para obter todas as worktrees: `path`, `branch` e `HEAD` de cada uma. A checkout principal também é uma worktree.
   - Se o diretório não for um repositório Git, trate como **worktree única** (o próprio `cwd`).

2. **Reconstruir o checkpoint de CADA worktree (read-only, escopado ao `path` dela):**
   - **Feature ativa:** se a branch for `feat/<feature>`, essa é a feature da sessão; senão, a feature mais recente com fatias pendentes em `docs/`.
   - **Planejamento:** existem `docs/prd/PRD-*.md` e `docs/mvp/MVP-*.md`?
   - **Escopo:** conta `N` = número de fatias enumeradas no MVP (`Fatia 01`, `Fatia 02`, …).
   - **Specs:** em `docs/specs/spec-*.md`, conta quantas existem e lê o `Status` de cada uma (`PENDENTE` / `EM ANDAMENTO` / `CONCLUÍDO`).
   - **Git/PR:** há uma PR (Draft) para a branch (`gh pr list --head <branch>`)? Quantos commits de fatia?
   - **Estado:** `STATE.md` (se existir) registra a feature como concluída/integrada?
   - Uma worktree **sem nenhum artefato SDD** é marcada como "sem sessão SDD" (não é uma sessão retomável).

3. **Derivar a fase de cada worktree** — avalie da linha **mais avançada** para a mais inicial e pare na primeira verdadeira:

   | Estado detectado | Fase | Próximo comando |
   |---|---|---|
   | Sem `docs/prd` e `docs/mvp` | **Zero** | `/sdd-plan <feature>` |
   | PRD/MVP existem, sem `docs/specs` | **Planejado** | `/sdd-spec` |
   | nº de specs ≠ `N` fatias do MVP | **Specs incompletas** | `/sdd-spec` (fechar cobertura) |
   | specs existem, nem todas `CONCLUÍDO` | **Implementando (X de N)** | `/sdd-implement` |
   | todas `CONCLUÍDO`, ainda em `feat/*` | **Implementado** | `/sdd-validate` (e depois `/sdd-finish`) |
   | branch mergeada / `STATE.md` atualizado | **Concluído** | `/sdd-plan <nova-feature>` |

4. **Consolidar e emitir:**
   - **Se houver ≥ 2 worktrees com sessão SDD:** emita o **Painel de Frota** (formato abaixo), ordenado da sessão mais avançada para a mais inicial, e peça ao usuário para escolher qual retomar.
   - **Se houver apenas 1 sessão SDD:** emita o **Checkpoint Detalhado** dessa sessão.
   - Sempre destaque o **local correto** (path) de cada sessão: os subcomandos precisam ser executados na worktree correspondente.

5. **Callout obrigatório** do próximo passo. Ofereça-se para executar o comando recomendado da sessão escolhida, mas **aguarde a confirmação do usuário** (e confirme que ele está na pasta certa) antes de rodá-lo.

---

## 🗂️ Formato do Painel de Frota (≥ 2 sessões)

```text
🗂️  SDD FLEET — 3 sessões ativas

[1] auth              /home/user/proj              main worktree
     Fase: Implementando   ·   2/4 fatias   ·   PR #12 Draft
     👉 na pasta /home/user/proj → /sdd-implement   (Fatia 3 de 4)

[2] billing           /home/user/proj-billing      feat/billing
     Fase: Specs incompletas   ·   3/5 specs
     👉 na pasta /home/user/proj-billing → /sdd-spec

[3] reports           /home/user/proj-reports      feat/reports
     Fase: Implementado   ·   4/4 fatias   ·   aguardando validação
     👉 na pasta /home/user/proj-reports → /sdd-validate

(+1 worktree sem sessão SDD)

Escolha a sessão [1–3] para ver o checkpoint detalhado ou retomar.
```

## 📋 Formato do Checkpoint Detalhado (1 sessão)

```text
🧭 SDD CHECKPOINT: <feature>   (worktree: /home/user/proj)
├─ Fase:      <fase>   (branch: <branch> | PR: #<n> Draft)
├─ Progresso: <X> de <N> fatias concluídas
├─ Pendentes: spec-fatia-03 (EM ANDAMENTO), spec-fatia-04 (PENDENTE)
└─ 👉 Próximo: /sdd-implement   (retomar na Fatia 3 de 4)
```

Se **nenhuma** worktree tiver fluxo SDD, o relatório informa que não há sessão ativa e sugere `/sdd-plan <feature>`.

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

Após o painel/checkpoint, o agente **DEVE** terminar exibindo o próximo passo em destaque, incluindo **a pasta** quando houver múltiplas sessões:

> **👉 Próximo Passo Recomendado:**
> <mensagem contextual da sessão> — execute na pasta `<path-da-worktree>`:
> `<comando derivado>`

---

## 🚀 Índice da Suíte (referência)

O fluxo completo, na ordem `PRD → MVP → Spec → Implement → Validate → Finish | Audit`:

* **`/sdd-plan <nome-feature>`** — Entrevista de produto (com gate de espera) e criação do PRD (`docs/prd/`) e MVP fatiado (`docs/mvp/`).
* **`/sdd-spec`** — Mapeamento holístico de arquitetura e geração das specs base de **todas as fatias** (`docs/specs/`), com verificação de cobertura `N specs == N fatias`.
* **`/sdd-implement`** — Governança na 1ª execução (branch `feat/...`, commit dos docs, PR Draft) e implementação **fatia a fatia** (uma fatia por execução, commit na PR) de ponta a ponta (Backend + UI + Testes). Repita até a última fatia.
* **`/sdd-validate`** — Execução automatizada da bateria de qualidade (detecta a stack: `tsc`, `lint`, `test`, `e2e` / `pytest`).
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
