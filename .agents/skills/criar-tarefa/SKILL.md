---
name: criar-tarefa
description: Cria arquivos Markdown de tarefas pendentes na agenda Megamaxi. Use quando o usuário pedir para adicionar, registrar, anotar, lembrar ou criar uma tarefa, prazo ou pendência, inclusive em linguagem natural ou a partir de áudio transcrito.
---

# Criar tarefa

Registre uma nova tarefa em `Pendentes/` sem alterar tarefas existentes.

## Extrair informações

Identifique, quando presentes:

- título da tarefa;
- projeto associado;
- prazo; e
- horário, quando informado; e
- contexto ou descrição.

Trate a data mencionada como prazo. Converta-a para `dd-mm-aaaa`, usando a data atual e o fuso horário do usuário para datas relativas. Quando não houver prazo, use `SD`.

Use o nome do projeto apenas se ele for explicitamente informado ou inequivocamente reconhecível no pedido. Se a solicitação não permitir determinar o título da tarefa, peça esclarecimento antes de criar o arquivo.

## Criar o arquivo

1. Converta título e projeto para minúsculas, sem acentos e com palavras separadas por `_`.
2. Use um destes nomes:

   ```text
   projeto_nome_da_tarefa_dd-mm-aaaa.md
   nome_da_tarefa_dd-mm-aaaa.md
   projeto_nome_da_tarefa_SD.md
   nome_da_tarefa_SD.md
   ```

3. Crie o arquivo em `Pendentes/`. Se já existir um arquivo com o mesmo nome, não o sobrescreva: informe o conflito e peça confirmação ou um título diferente.
4. Use este conteúdo, substituindo os valores entre colchetes:

   ```md
   ---
   projeto: [nome do projeto ou vazio]
   prazo: [dd-mm-aaaa ou SD]
   horario: [HH:mm ou SD]
   criada_em: [dd-mm-aaaa]
   prioridade: não definida
   status: pendente
   ---

   # [Título da tarefa]

   [Descrição ou contexto opcional]
   ```

5. Preserve a descrição em linguagem natural, sem inventar detalhes. Se não houver contexto adicional, deixe uma linha vazia após o título.
6. Se `prazo` não for `SD`, crie lembretes individuais às 09:00 no dia anterior e às 09:00 no dia do prazo, usando a automação do Codex. Inclua o nome exato do arquivo em cada nome e prompt de automação. Se o usuário tiver solicitado horários ou intervalos específicos de lembrete, crie os solicitados e não substitua por lembretes-padrão duplicados.
7. Ao concluir, informe o nome do arquivo criado, o prazo interpretado e os lembretes agendados.

## Exemplos

Pedido: “Lembrar de revisar o catálogo da Megamaxi até sexta.”

Resultado esperado: `Pendentes/megamaxi_revisar_catalogo_17-07-2026.md` quando a sexta-feira correspondente for 17-07-2026.

Pedido: “Organizar os documentos.”

Resultado esperado: `Pendentes/organizar_documentos_SD.md`.
