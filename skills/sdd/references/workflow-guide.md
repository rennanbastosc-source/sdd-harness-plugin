# Guia de Condução do Workflow SDD

Este guia orienta o agente durante as 5 etapas do **Spec-Driven Development (SDD)**.

---

## 🎯 Regras de Ouro do SDD

1. **Nunca programe sem Spec:** Antes de alterar código, exija ou crie a spec técnica correspondente.
2. **Entregas Ponta a Ponta:** Toda fatia deve ser entregue completa (Backend + Frontend + Testes). NUNCA faça commits parciais de "só o backend".
3. **Validação Rigorosa:** Só considere a fatia concluída após passar em todos os linters, verificadores de tipo e suíte de testes do projeto.
4. **Sem Sobre-Engenharia:** Crie apenas o código necessário para satisfazer os critérios de aceite definidos no PRD/MVP.
5. **Chamada de Próximo Comando OBRIGATÓRIA (UX):** Todo final de execução de qualquer subcomando (`/sdd-*`) **DEVE** incluir um bloco em destaque com a indicação explícita do próximo comando slash a ser executado pelo usuário.

---

## 🔄 Encadeamento de Comandos (Next Step Matrix)

| Comando Executado | Saída Esperada | **Chamada Obrigatória no Final** |
|---|---|---|
| `/sdd-plan <feature>` | `PRD` + `MVP` gerados em `docs/` | `👉 Próximo Passo Recomendado: /sdd-spec Fatia-01` |
| `/sdd-spec <fatia>` | Spec Técnica em `docs/specs/` | `👉 Próximo Passo Recomendado: /sdd-implement` |
| `/sdd-implement` | Código + UI + Testes desenvolvidos | `👉 Próximo Passo Recomendado: /sdd-validate` |
| `/sdd-validate` | Bateria de testes e linters aprovada | `👉 Próximo Passo Recomendado: /sdd-finish` |
| `/sdd-finish` | `STATE.md` atualizado e commit realizado | `👉 Próximo Passo Recomendado: /sdd-spec Fatia-02` (ou `/sdd-plan`) |
