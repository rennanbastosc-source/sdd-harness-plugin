---
name: sdd-validate
description: Executa a bateria de qualidade automatizada e portão fechado detectando a stack do repositório (tsc, lint, vitest/pytest, e2e/playwright).
---

# /sdd-validate

Executa a validação rigorosa de qualidade no repositório com lógica de portão fechado.

## Passos de Execução

1. **Detecção da Stack do Repositório:**
   - Inspeciona o projeto para identificar os comandos de validação adequados (`tsc`, `lint`, `test`, `e2e`).

2. **Execução da Bateria de Qualidade (Portão Fechado):**
   - **Typecheck & Lint:** Valida a integridade estática de tipos e estilos de código.
   - **Testes de Unidade e Integração:** Garante que a lógica de negócio e banco funcionam sem regressão.
   - **Testes E2E (UI):** Se a implementação tocou a interface do usuário ou telas, **OBRIGATORIAMENTE** executa a suíte de testes E2E (ex: Playwright/Cypress) para validar a experiência do usuário end-to-end.
   - **Sem Mascarar Erros:** Se qualquer etapa falhar, o processo para. **NUNCA MASCARE O ERRO**. Corrija a causa raiz no código antes de aprovar.

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

Após a bateria completa ser concluída com 100% de sucesso (tudo verde), o agente **DEVE obrigatoriamente** terminar a resposta exibindo o seguinte aviso em destaque:

> **👉 Próximo Passo Recomendado:**
> Toda a bateria de validação (`tsc`, `lint`, `tests`, `e2e`) passou com 100% de sucesso! Execute o comando para gerar a spec final pós-implementação, atualizar documentos e realizar o commit/push/merge:
> `/sdd-finish`
