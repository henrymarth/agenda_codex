---
name: gerenciar-tarefas
description: Atualiza prioridade, status e localização de tarefas da agenda Megamaxi. Use quando o usuário pedir para priorizar, iniciar, bloquear, concluir, cancelar, reabrir ou alterar o status de uma tarefa, inclusive em linguagem natural ou áudio transcrito.
---

# Gerenciar tarefas

Altere somente `prioridade`, `status`, localização da tarefa e seus lembretes vinculados. Não altere título, projeto, prazo, horário, data de criação ou descrição.

## Valores permitidos

- `prioridade`: `não definida`, `baixa`, `média`, `alta` ou `urgente`.
- `status`: `pendente`, `em andamento`, `bloqueada`, `cancelada` ou `concluída`.

Localize a tarefa pelo nome, projeto e, se necessário, pelos metadados. Quando houver mais de uma correspondência possível, peça esclarecimento antes de modificar arquivos.

## Atualizar prioridade e status

1. Edite apenas o valor solicitado no cabeçalho da tarefa.
2. Mantenha tarefas com os status `pendente`, `em andamento`, `bloqueada` e `cancelada` em `Pendentes/`.
3. Ao definir `concluída`, edite o status e mova o mesmo arquivo, sem renomeá-lo, de `Pendentes/` para `Concluídos/`.
4. Ao reabrir uma tarefa concluída, mova o arquivo de `Concluídos/` para `Pendentes/` e defina `status: pendente`.
5. Ao reativar uma tarefa cancelada, mantenha-a em `Pendentes/` e defina `status: pendente`.

## Lembretes vinculados

Ao concluir ou cancelar uma tarefa, procure automações cujo nome ou prompt contenha a chave exata `VINCULO-TAREFA: Pendentes/<nome_exato_do_arquivo>.md`. Cancele somente as automações correspondentes. Não cancele a automação `Revisão diária da agenda`.

Ao reabrir ou reativar, não recrie lembretes automaticamente; o usuário pode pedir novos lembretes com `$agendar-notificacoes`.

## Confirmação

Informe a tarefa modificada, os valores anteriores e novos, a pasta final e a quantidade de lembretes cancelados. Se não houver lembretes vinculados, diga isso. Se houver lembretes permanentes vinculados, cancele-os ao concluir ou cancelar a tarefa.
