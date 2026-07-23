---
name: sdd-implement
description: Lê a especificação técnica ativa em docs/specs/ e desenvolve a solução de ponta a ponta (Backend + Frontend + Testes no mesmo ciclo).
---

# /sdd-implement

Executa a construção do código com base estrita na especificação técnica aberta.

## Passos de Execução

1. **Localizar a Spec Ativa:**
   - Procura o arquivo mais recente em `docs/specs/spec-*.md` com Status `EM ANDAMENTO`.

2. **Desenvolvimento Ponta a Ponta:**
   - **Backend / Dados:** Atualiza/cria esquemas de banco, migrações/types, rotas e regras de negócio.
   - **Frontend / UI:** Constrói/atualiza os componentes visuais e conecta diretamente com o backend.
   - **Testes:** Escreve os testes unitários e de integração descritos na spec.
   - **Regra de Ouro:** NUNCA faz entregas parciais (ex: backend sem UI ou sem testes).

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

Ao concluir o código e os testes da fatia, o agente **DEVE obrigatoriamente** terminar a resposta exibindo o seguinte aviso em destaque:

> **👉 Próximo Passo Recomendado:**
> O código e os testes foram implementados! Execute a bateria de validação automática:
> `/sdd-validate`
