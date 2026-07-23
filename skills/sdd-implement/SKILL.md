---
name: sdd-implement
description: Gerencia governança Git (branch exclusiva + PR Draft) e desenvolve as fatias do MVP em sequência de ponta a ponta (Backend + UI + Testes).
---

# /sdd-implement

Gerencia o ciclo de governança de versão e executa o desenvolvimento em código com base estrita nas especificações técnicas em `docs/specs/`.

## Passos de Execução

1. **Governança de Versão (Branch & PR Draft):**
   - Verifica se o repositório está na branch exclusiva da feature (`feat/<nome-feature>`). Se não estiver, cria e alterna para a branch.
   - Commita os documentos iniciais de planejamento e especificações (`docs/prd/`, `docs/mvp/`, `docs/specs/`).
   - Garante a abertura/identificação de uma Pull Request (Draft/em andamento) com descrição clara do escopo e fatiamento.

2. **Desenvolvimento Ponta a Ponta & Código Enxuto (Escada Ponytail):**
   - Antes de criar novos componentes, funções ou abstrações, aplique a **Escada Ponytail**:
     - *YAGNI:* Não adicione recursos especulativos nem abstrações preparadas para o futuro incerto.
     - *Reuso:* Reutilize utilitários, helpers, componentes de UI e esquemas já existentes no codebase.
     - *Nativo/Stdlib:* Prefira APIs nativas e bibliotecas já instaladas antes de adicionar novas dependências.
     - *Causa Raiz:* Em correções de bugs, corrija a causa raiz na função compartilhada em vez de criar retalhos nos chamadores.
   - Para cada fatia com status `EM ANDAMENTO` ou `PENDENTE` em `docs/specs/spec-*.md`:
     - **Backend / Dados:** Atualiza/cria esquemas de banco, migrações/types, rotas, server actions e regras de negócio.
     - **Frontend / UI:** Constrói/atualiza os componentes visuais, conecta diretamente com o backend e garante UX fluida.
     - **Testes:** Escreve os testes unitários, de integração e cenários E2E descritos na spec.
   - **Regra de Ouro E2E:** NADA deve ser entregue sem começo, meio e fim. NUNCA faça entregas parciais (ex: backend sem UI, ou código sem suíte de testes correspondente).

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

Ao concluir a implementação do código e testes das fatias, o agente **DEVE obrigatoriamente** terminar a resposta exibindo o seguinte aviso em destaque:

> **👉 Próximo Passo Recomendado:**
> O código e os testes de todas as fatias foram implementados de ponta a ponta! Execute a bateria de validação automática:
> `/sdd-validate`
