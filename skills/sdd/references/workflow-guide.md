# Guia de Condução do Workflow SDD

Este guia orienta o agente durante as 5 etapas do **Spec-Driven Development (SDD)**.

---

## 🎯 Regras de Ouro do SDD

1. **Nunca programe sem Spec:** Antes de alterar qualquer linha de código, crie as specs técnicas base de todas as fatias da funcionalidade.
2. **Governança de Versão:** Toda implementação inicia criando uma branch exclusiva (`feat/<feature>`), commitando a documentação inicial de `docs/` e abrindo uma PR Draft comentada e identificada. Cada fatia gera um commit próprio dentro da PR, e o encerramento no `/sdd-finish` integra tudo via **squash-merge**.
3. **Código Enxuto (Escada Ponytail):** Evite sobre-engenharia. Reutilize helpers, componentes e a stdlib/plataforma nativa antes de inventar novas abstrações. Mantenha o menor diff funcional possível.
4. **Entregas Ponta a Ponta:** Toda fatia deve ser entregue completa (Backend + Frontend/UI + Testes). NUNCA entregue códigos parciais ou sem testes (nada deve ser entregue sem começo, meio e fim).
5. **Loop Engineering Adaptativo:** Validação dinâmica por complexidade. Em falhas, entra em loop de auto-cura baseado em logs. Em UI ou código crítico, aplica testes E2E e revisão Ponytail anti-overengineering.
6. **Spec Final As-Built:** O encerramento no `/sdd-finish` gera a documentação final pós-implementação consolidando o estado real do código antes do merge.
7. **Chamada de Próximo Comando OBRIGATÓRIA (UX):** Todo final de execução de qualquer subcomando (`/sdd-*`) **DEVE** incluir um bloco em destaque com a indicação explícita do próximo comando slash a ser executado pelo usuário.

---

## 🔄 Encadeamento de Comandos (Next Step Matrix)

| Slash Command | Saída Esperada | **Chamada Obrigatória no Final** |
|---|---|---|
| `/sdd` | **Guardião de sessão (multi-worktree):** enumera as worktrees e reconstrói o checkpoint de cada sessão (fase + progresso X/N) a partir de `docs/` e Git; resume a frota apontando o comando e a pasta corretos; ideal após `/clear` | `👉 <próximo comando + pasta, derivados do estado detectado>` |
| `/sdd-plan <feature>` | `PRD` + `MVP` (N fatias) gerados e lapidados em `docs/` | `👉 Próximo Passo Recomendado: /sdd-spec` |
| `/sdd-spec` | Specs Técnicas base de **todas as fatias** em `docs/specs/` | `👉 Próximo Passo Recomendado: /sdd-implement` |
| `/sdd-implement` | **Uma fatia** implementada (Backend + UI + Testes Ponytail) e commitada na PR Draft; governança criada na 1ª execução | `👉 /sdd-implement` (se restam fatias pendentes) **\|** `👉 /sdd-validate` (após a última fatia) |
| `/sdd-validate` | Loop Adaptativo: Self-Healing, Bateria completa, E2E e Ponytail Review 100% verde | `👉 Próximo Passo Recomendado: /sdd-finish` |
| `/sdd-finish` | Spec Final *as-built*, `STATE.md` atualizado, commit final, push e **squash-merge** | `👉 Próximo Passo Recomendado: /sdd-plan <nova-feature>` |
| `/sdd-audit` | Relatório executivo de dívida técnica, código enxuto, consistência SDD e gaps de testes | `👉 Próximo Passo Recomendado: /sdd-implement` ou `/sdd-spec` |
