# Guia de Condução do Workflow SDD

Este guia orienta o agente durante as 5 etapas do **Spec-Driven Development (SDD)**.

---

## 🎯 Regras de Ouro do SDD

1. **Nunca programe sem Spec:** Antes de alterar qualquer linha de código, crie as specs técnicas base de todas as fatias da funcionalidade.
2. **Governança de Versão:** Toda implementação inicia criando uma branch exclusiva (`feat/<feature>`), commitando a documentação inicial de `docs/` e abrindo uma PR Draft comentada e identificada.
3. **Entregas Ponta a Ponta:** Toda fatia deve ser entregue completa (Backend + Frontend/UI + Testes). NUNCA entregue códigos parciais ou desprovidos de testes (nada deve ser entregue sem começo, meio e fim).
4. **Validação Rigorosa e Portão Fechado:** Só considere a validação concluída após passar em typechecker (`tsc`), linter, suíte de testes unitários/integração e testes E2E (se houver alteração de UI). NUNCA mascare erros.
5. **Spec Final As-Built:** O encerramento no `/sdd-finish` gera a documentação final pós-implementação consolidando o estado real do código antes do merge.
6. **Chamada de Próximo Comando OBRIGATÓRIA (UX):** Todo final de execução de qualquer subcomando (`/sdd-*`) **DEVE** incluir um bloco em destaque com a indicação explícita do próximo comando slash a ser executado pelo usuário.

---

## 🔄 Encadeamento de Comandos (Next Step Matrix)

| Comando Executado | Saída Esperada | **Chamada Obrigatória no Final** |
|---|---|---|
| `/sdd-plan <feature>` | `PRD` + `MVP` (N fatias) gerados e lapidados em `docs/` | `👉 Próximo Passo Recomendado: /sdd-spec` |
| `/sdd-spec` | Specs Técnicas base de **todas as fatias** em `docs/specs/` | `👉 Próximo Passo Recomendado: /sdd-implement` |
| `/sdd-implement` | Branch criada, PR Draft aberta, Código + UI + Testes desenvolvidos sequencialmente | `👉 Próximo Passo Recomendado: /sdd-validate` |
| `/sdd-validate` | Bateria completa (`tsc`, `lint`, `test`, `e2e`) 100% verde | `👉 Próximo Passo Recomendado: /sdd-finish` |
| `/sdd-finish` | Spec Final *as-built*, `STATE.md` atualizado, commit final, push e merge | `👉 Próximo Passo Recomendado: /sdd-plan <nova-feature>` |
