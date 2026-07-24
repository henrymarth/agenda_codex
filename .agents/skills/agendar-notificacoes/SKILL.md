---
name: agendar-notificacoes
description: Cria, altera e cancela lembretes e revisões da agenda Megamaxi. Use quando o usuário pedir para avisar, lembrar, notificar, agendar, reagendar ou cancelar uma notificação, inclusive em linguagem natural ou áudio transcrito.
---

# Agendar notificações

Use a automação do Codex para criar, atualizar ou remover lembretes. Não crie, altere ou conclua tarefas, exceto registrar `horario` quando um lembrete estiver explicitamente vinculado a uma tarefa existente.

## Contrato de vínculo

Quando um lembrete pertencer a uma tarefa, use sempre a chave canônica da tarefa como identificador estável:

```text
VINCULO-TAREFA: Pendentes/<nome_exato_do_arquivo>.md
```

Repita essa chave no nome e no prompt da automação. Nunca invente um nome de arquivo; derive-o do arquivo real da tarefa localizada.

## Interpretar o pedido

Extraia o assunto, data, hora, fuso horário e todos os momentos de lembrete solicitados. Use o fuso horário do usuário. Converta datas relativas para data e hora absolutas antes de agendar.

- Se o usuário disser “me avise amanhã às 10h”, crie um lembrete individual às 10:00 de amanhã.
- Se houver compromisso e horário, como “reunião às 14h; me avise às 10h”, registre o compromisso no texto da notificação e crie o lembrete às 10:00.
- Se pedir vários intervalos, crie todos os lembretes solicitados.
- Se faltar uma informação material, como a hora de um lembrete que exige precisão, peça esclarecimento.
- Não agende horários no passado. Informe o problema e peça uma nova data ou horário.

## Tipos de agendamento

### Revisão diária

Quando solicitado, crie ou atualize uma única automação chamada `Revisão diária da agenda`, todos os dias às 09:00. Em cada execução, ela deve usar `$buscar-tarefas` para resumir pendências, prazos de hoje, atrasadas e próximas.

Antes de criar, procure uma automação existente com esse nome; atualize-a em vez de duplicá-la.

### Lembretes individuais

Crie uma automação única para cada data e hora de lembrete. Dê um nome descritivo que inclua o assunto e o horário. O prompt da automação deve informar o lembrete de forma direta e curta.

Para lembretes de disparo único, use recorrência com `COUNT=1`. Para lembretes recorrentes vinculados a uma tarefa, não use `COUNT`; mantenha a automação ativa até a tarefa ser concluída ou cancelada.

Um lembrete avulso, sem tarefa explicitamente indicada, cria somente a notificação. Não crie um arquivo em `Pendentes/` por conta própria.

Quando o usuário referir uma tarefa existente, localize-a pelo nome e/ou projeto. Inclua o nome exato do arquivo da tarefa no nome e no prompt de cada automação vinculada e adicione a chave `VINCULO-TAREFA: Pendentes/<nome_exato_do_arquivo>.md`. Se o compromisso possuir hora, registre ou atualize `horario: HH:mm` no cabeçalho da tarefa. Não modifique seu prazo, descrição, prioridade ou status.

### Alterar e cancelar

Ao reagendar ou cancelar, identifique a automação pelo assunto, pelo horário e, quando houver, pela chave `VINCULO-TAREFA`. Atualize ou remova a automação correspondente; nunca crie outra como substituta sem remover a anterior.

## Execução

Use a ferramenta de automações do Codex. Para ações sobre lembretes existentes, examine primeiro os agendamentos atuais e preserve os campos não solicitados. Não mostre expressões técnicas de recorrência ao usuário.

Ao concluir, confirme assunto, data, hora e quantidade de lembretes criados, atualizados ou cancelados.
