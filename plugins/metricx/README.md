# MetricX

Plugin oficial do MetricX para Claude Code e Codex. Ele conecta o seu agente ao servidor MCP do MetricX
(`https://api-metricx.baldussi.com.br/mcp`) para consultar chamadas telefônicas, indicadores de atendimento, notas de
qualidade geradas por IA e transcrições das conversas, sempre em modo somente leitura e limitado às permissões do seu
usuário do MetricX (empresa, departamentos e ramais).

## O que o plugin envia e recebe

O plugin não roda código local: ele apenas registra o servidor MCP remoto e uma skill com orientações de uso. As
perguntas e consultas que o seu agente fizer são enviadas ao servidor do MetricX, que devolve somente dados que o seu
usuário já pode ver no MetricX. Nenhuma ferramenta altera dados. A ferramenta `perguntar_metricx` usa um provedor de IA
contratado pelo MetricX para gerar a consulta e redigir a resposta, com telefones mascarados.

## Autenticação

Na primeira conexão, o agente abre no navegador a página de login do MetricX (OAuth 2.1 com PKCE). Entre com o mesmo
e-mail e senha que você usa no MetricX. O módulo precisa estar habilitado para o seu usuário pelo administrador da
sua empresa. Conexões podem ser revogadas em Integrações → Agente MCP.

## Ferramentas

`descrever_dados`, `consultar_sql`, `perguntar_metricx`, `obter_indicadores`, `listar_chamadas`, `detalhar_chamada`,
`obter_transcricao` e `buscar_nas_transcricoes`. Documentação: https://api-metricx.baldussi.com.br/agente-mcp/documentacao
