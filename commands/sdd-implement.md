---
name: sdd-implement
description: Implementa UMA fatia por execução (a primeira pendente) de ponta a ponta (Backend + UI + Testes), commitando na PR Draft, e reconvida a próxima fatia até a última.
---

# /sdd-implement

Gerencia o ciclo de governança de versão e executa o desenvolvimento em código com base estrita nas especificações técnicas em `docs/specs/`. Opera como uma **máquina de estados de uma fatia por execução**: cada chamada implementa a próxima fatia pendente, commita e reconvida `/sdd-implement` até que todas estejam concluídas.

## Passos de Execução

1. **Governança de Versão (idempotente — configura uma vez, reusa depois):**
   - **Branch:** Se o repositório não estiver na branch exclusiva da feature (`feat/<nome-feature>`), cria e alterna. Se já estiver, reusa (nunca recria).
   - **Commit dos docs:** Se os documentos de planejamento (`docs/prd/`, `docs/mvp/`, `docs/specs/`) ainda não foram commitados, commita-os agora.
   - **PR Draft:** Se ainda não há PR aberta para a branch, abre uma **Pull Request Draft** (`gh pr create --draft`) com descrição clara do escopo e um **checklist das N fatias**. Se já existir, apenas identifica e reusa. **Nunca abre uma segunda PR.**

2. **Seleção da Fatia Atual (estado explícito):**
   - Lê todas as `docs/specs/spec-*.md`, conta o total `N` de fatias e seleciona a **primeira fatia** cujo `Status` seja diferente de `CONCLUÍDO` (i.e. `PENDENTE` ou `EM ANDAMENTO`). Essa é a **fatia da vez**.
   - Se **nenhuma** fatia estiver pendente (todas `CONCLUÍDO`), pule direto para a Regra de Saída (caminho "todas concluídas").
   - Marca a fatia selecionada como `EM ANDAMENTO` no cabeçalho e na seção "Checkpoint de Execução" da sua spec.

3. **Desenvolvimento Ponta a Ponta & Código Enxuto (Escada Ponytail) — apenas da fatia atual:**
   - Antes de criar novos componentes, funções ou abstrações, aplique a **Escada Ponytail**:
     - *YAGNI:* Não adicione recursos especulativos nem abstrações preparadas para o futuro incerto.
     - *Reuso:* Reutilize utilitários, helpers, componentes de UI e esquemas já existentes no codebase.
     - *Nativo/Stdlib:* Prefira APIs nativas e bibliotecas já instaladas antes de adicionar novas dependências.
     - *Causa Raiz:* Em correções de bugs, corrija a causa raiz na função compartilhada em vez de criar retalhos nos chamadores.
   - Desenvolva **somente a fatia da vez**, de ponta a ponta:
     - **Backend / Dados:** Atualiza/cria esquemas de banco, migrações/types, rotas, server actions e regras de negócio.
     - **Frontend / UI:** Constrói/atualiza os componentes visuais, conecta diretamente com o backend e garante UX fluida.
     - **Testes:** Escreve os testes unitários, de integração e cenários E2E descritos na spec.
   - **Regra de Ouro E2E:** NADA deve ser entregue sem começo, meio e fim. NUNCA faça entregas parciais (ex: backend sem UI, ou código sem suíte de testes correspondente).

4. **Checkpoint & Commit da Fatia (write-back de estado):**
   - Atualiza o `Status` da fatia para `CONCLUÍDO` no cabeçalho e na seção "Checkpoint de Execução" da sua spec.
   - Executa o commit da fatia usando **Conventional Commits** em PT-BR (ex: `feat(<modulo>): implementa fatia <XX> - <nome-da-fatia>`) e faz o push na branch da PR (`git push origin feat/<nome-feature>`).

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

O callout de saída é **condicional**, calculado a partir da contagem de fatias pendentes após o commit desta execução:

- **Se ainda restam fatias pendentes**, o agente **DEVE** terminar exibindo:

  > **👉 Próximo Passo Recomendado:**
  > Fatia **X de N** concluída e commitada na PR! Restam **Y** fatia(s). Execute novamente para implementar a próxima fatia de ponta a ponta:
  > `/sdd-implement`

- **Se esta era a última fatia (todas `CONCLUÍDO`)**, o agente **DEVE** terminar exibindo:

  > **👉 Próximo Passo Recomendado:**
  > Todas as **N** fatias foram implementadas de ponta a ponta e commitadas na PR! Execute a bateria de validação automática:
  > `/sdd-validate`
