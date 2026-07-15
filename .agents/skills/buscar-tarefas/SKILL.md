---
name: buscar-tarefas
description: Consulta e lista tarefas da agenda Megamaxi sem alterar arquivos. Use quando o usuário pedir para ver, buscar, encontrar, listar, revisar ou resumir pendências, tarefas concluídas, prazos, prioridades ou status, inclusive em linguagem natural ou áudio transcrito.
---

# Buscar tarefas

Consulte tarefas sem criar, editar, mover ou excluir arquivos.

## Escopo e resultado

- Busque em `Pendentes/` por padrão. Inclua `Concluídos/` somente quando o usuário mencionar tarefas concluídas, histórico ou ambos os grupos.
- Para um pedido genérico como “o que tenho para fazer?”, mostre todas as pendências, ordenadas por prazo crescente e com `SD` ao final.
- Aceite filtros por texto, projeto, prazo/data, prioridade, status e datas relativas como “hoje”, “esta semana”, “atrasadas” e “sem prazo”.
- Apresente título, projeto quando houver, prazo, prioridade, status e caminho do arquivo. Seja conciso.
- Quando nada corresponder, informe isso claramente.

## Busca em camadas

Economize leitura e contexto nesta ordem:

1. Liste somente os nomes dos arquivos `.md` da pasta aplicável.
2. Filtre pelos dados presentes no nome: projeto, palavras do título e prazo.
3. Leia apenas as primeiras 8 linhas dos arquivos candidatos para obter o cabeçalho:

   ```md
   ---
   projeto: ...
   prazo: ...
   horario: ...
   criada_em: ...
   prioridade: ...
   status: ...
   ---
   ```

4. Leia a descrição somente se a busca depender de contexto que não esteja no nome ou no cabeçalho, e apenas depois de reduzir os candidatos com as etapas anteriores.

Para listar todas as pendências, é necessário ler o cabeçalho de cada arquivo pendente, mas nunca a descrição sem necessidade.

## Interpretação

- Trate `prazo` como data-alvo. Converta datas relativas para `dd-mm-aaaa` usando a data atual e o fuso horário do usuário.
- Considere `SD` como sem prazo; não o trate como data desconhecida nem como tarefa atrasada.
- Para “atrasadas”, inclua apenas tarefas pendentes com prazo anterior à data atual.
- Se uma busca textual no nome não resolver a ambiguidade, avance para o cabeçalho e depois, se necessário, para a descrição.
