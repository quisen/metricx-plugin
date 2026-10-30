# MetricX — plugins para Claude Code e Codex

Conecta o seu agente (Claude Code, Codex) ao **MetricX**: chamadas, indicadores de atendimento, notas de qualidade
por IA e transcrições, sempre **somente leitura** e com as permissões do seu usuário do MetricX.

> Repositório: https://github.com/quisen/metricx-plugin · O servidor MCP é
> `https://api-metricx.baldussi.com.br/mcp` (Streamable HTTP, OAuth 2.1).

## Instalar

**Claude Code**
```
/plugin marketplace add quisen/metricx-plugin
/plugin install metricx@metricx
```
Depois rode `/mcp`, escolha `metricx` e faça login com o e-mail e a senha do MetricX.

Sem plugin: `claude mcp add --transport http metricx https://api-metricx.baldussi.com.br/mcp`

**Codex**
```
codex plugin marketplace add quisen/metricx-plugin
```
Depois, dentro do Codex, abra `/plugins` e instale **MetricX**. O login abre no navegador.

Sem plugin: `codex mcp add metricx --url https://api-metricx.baldussi.com.br/mcp` e `codex mcp login metricx`.

## Autenticação

Ao conectar, o aplicativo abre a página de login do MetricX (OAuth 2.1 com PKCE). Use o mesmo e-mail e senha do
MetricX. O acesso depende de o módulo de agente estar habilitado para o seu usuário. Você pode revogar uma conexão a
qualquer momento em **Integrações → Agente MCP** no MetricX.

## Ferramentas

| Ferramenta | O que faz |
|---|---|
| `descrever_dados` | Tabelas, colunas, regras e exemplos de SQL |
| `consultar_sql` | Consulta SQL de leitura (DuckDB) nos dados do usuário |
| `perguntar_metricx` | Pergunta em linguagem natural respondida pelo agente do MetricX |
| `obter_indicadores` | Volume, atendimento, duração e nota média, com agrupamentos |
| `listar_chamadas` | Lista de chamadas com filtros |
| `detalhar_chamada` | Metadados e análise de qualidade de uma chamada |
| `obter_transcricao` | Transcrição fala a fala |
| `buscar_nas_transcricoes` | Busca de termos nas conversas |

Todas as ferramentas são somente leitura (`readOnlyHint: true`).

## Estrutura

```
.claude-plugin/marketplace.json      marketplace do Claude Code
.agents/plugins/marketplace.json     marketplace do Codex
plugins/metricx/
  .claude-plugin/plugin.json         manifesto Claude Code
  .mcp.json                          servidor MCP (formato Claude Code)
  plugin.json                        manifesto Codex / agent-plugins
  mcp.json                           servidor MCP (formato portável)
  skills/metricx-analise/SKILL.md    orientação de uso das ferramentas
  assets/icon.svg
```

Política de privacidade: https://api-metricx.baldussi.com.br/legal/privacidade · Termos de uso: https://api-metricx.baldussi.com.br/legal/termos · Suporte: **a definir pela Baldussi**.
