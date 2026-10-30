---
name: metricx-analise
description: Use when the user asks about call-center data in MetricX — calls (chamadas), service levels, missed calls, operators, departments, AI quality scores (notas), call summaries or transcripts. Guides which MetricX MCP tool to call and how to write DuckDB SQL for the MetricX catalog.
---

# Análise de dados do MetricX

O servidor MCP `metricx` dá acesso somente leitura aos dados de call center do usuário conectado. Os dados já vêm
restritos às permissões dele (empresa, departamentos e ramais) e são atualizados a cada ~5 minutos.

## Qual ferramenta usar

| Pedido | Ferramenta |
|---|---|
| Volume, taxa de atendimento, duração média, nota média (por dia, semana, mês, hora, departamento, operador, tipo, status) | `obter_indicadores` |
| Lista de chamadas com filtros (tipo, status, departamento, ramal, nota, duração) | `listar_chamadas` |
| Uma chamada específica | `detalhar_chamada`, depois `obter_transcricao` se precisar do diálogo |
| Onde um assunto/palavra aparece nas conversas | `buscar_nas_transcricoes` |
| Qualquer outra análise (cruzamentos, rankings, comparações) | `descrever_dados` uma vez, depois `consultar_sql` |
| O usuário prefere que o próprio MetricX responda | `perguntar_metricx` |

## Escrevendo SQL (`consultar_sql`)

- Dialeto DuckDB; uma única consulta `SELECT`/`WITH`; só as tabelas de `descrever_dados`, sem prefixo de esquema.
- Tabelas principais: `chamadas` (uma linha por chamada), `analises` (nota, motivo, resumo; junte por `chamada_id`),
  `falas` (trechos da transcrição; busque em `texto_busca`, minúsculo e sem acentos), `chamadas_perdidas`, `ramais`,
  `departamentos`.
- Use `dia`, `hora`, `current_date` e `date_trunc('week'|'month', current_date)` para períodos (horário de Brasília).
- Prefira agregações; o resultado é limitado a 1000 linhas.
- Se a consulta for recusada, leia a mensagem de erro, corrija e tente de novo.

## Ao responder

- Diga o período considerado e a data de atualização dos dados (`dados_atualizados_ate`).
- Telefones de clientes são dados pessoais: só os mostre quando o usuário pedir explicitamente.
- Se a ferramenta disser que a chamada não foi encontrada, ela pode não existir ou estar fora do acesso do usuário.
