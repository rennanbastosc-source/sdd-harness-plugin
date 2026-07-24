---
name: sdd-finish
description: Consolida a Spec Final pós-implementação (as-built), atualiza o estado do projeto (STATE.md) e finaliza com commit convencional, push e squash-merge da PR.
---

# /sdd-finish

Finaliza o ciclo completo do desenvolvimento, registrando a documentação final *as-built*, atualizando o estado do repositório e concluindo o fluxo Git.

## Passos de Execução

1. **Geração da Spec Final Pós-Implementação (*As-Built*):**
   - Consolida e atualiza `docs/specs/spec-*.md` refletindo o estado final exato de como a funcionalidade foi construída no código (registrando quaisquer refinamentos de design ou ajustes técnicos feitos durante o dev).
   - Marca o status de todas as specs como `CONCLUÍDO`.

2. **Atualização do Estado do Repositório:**
   - Atualiza `STATE.md` (se existir) registrando novos invariantes vivos, modelos de banco ou decisões arquiteturais introduzidas.
   - Atualiza `BACKLOG.md` / `STATE_ARCHIVE.md` (se existirem) movendo os itens entregues para concluídos.

3. **Commit Final, Push e Squash-Merge da PR:**
   - Prepara e executa o commit final utilizando **Conventional Commits** em PT-BR (ex: `feat(modulo): conclui implementação de...`).
   - Faz o push da branch de feature (`git push origin feat/<nome-feature>`).
   - Marca a Pull Request como pronta (`gh pr ready`) e a integra via **squash-merge** com título em Conventional Commit, removendo a branch: `gh pr merge --squash --delete-branch`.

---

## 🛑 REGRA OBRIGATÓRIA DE SAÍDA (NEXT COMMAND CALLOUT)

Ao concluir a consolidação e o merge da funcionalidade, o agente **DEVE obrigatoriamente** terminar a resposta exibindo o seguinte aviso em destaque:

> **👉 Próximo Passo Recomendado:**
> A funcionalidade e a documentação *as-built* foram concluídas e integradas com sucesso! Para iniciar o planejamento de um novo produto ou feature:
> `/sdd-plan <nome-da-nova-feature>`
