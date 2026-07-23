---
name: sdd-validate
description: Executa a bateria de qualidade automatizada detectando a stack do repositório (tsc, lint, vitest/pytest, e2e/verify).
---

# /sdd-validate

Executa a validação rigorosa de qualidade no repositório.

## Passos de Execução

1. **Deteção da Stack do Repositório:**
   - Inspeciona o projeto para identificar os comandos de validação adequados (`tsc`, `lint`, `test`, `e2e`).

2. **Execução da Bateria:**
   - Roda a checagem de tipos, linter e testes.
   - Se houver erro: **NÃO MASCARE O ERRO**. Corrija a causa raiz no código antes de aprovar.

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

Após a validação ser concluída com 100% de sucesso, o agente **DEVE obrigatoriamente** terminar a resposta exibindo o seguinte aviso em destaque:

> **👉 Próximo Passo Recomendado:**
> Toda a bateria de testes e linters passou com sucesso! Execute o comando para registrar a entrega e realizar o commit:
> `/sdd-finish`
