# Conecta.RUÁ para agentes de código

Plugin oficial que conecta Codex, Claude Code e Cursor aos servidores MCP especializados do Conecta.RUÁ.

## Módulos incluídos

- Core
- Scrum
- Comercial
- Serviços
- Contratos
- Crachás
- Manual

Todos os clientes recebem um servidor MCP por domínio:

```text
/mcp/core
/mcp/scrum
/mcp/comercial
/mcp/servicos
/mcp/contratos
/mcp/crachas
/mcp/manual
```

O plugin não contém tokens nem credenciais. Cada cliente abre o OAuth do Conecta por servidor e recebe apenas as ferramentas permitidas para o usuário autenticado. Autorize os servidores em sequência; o Cursor limita o catálogo a cerca de 50 tools por servidor, então o plugin não usa o endpoint agregado `/mcp/conecta`.

## Codex

Adicione o marketplace:

```bash
codex plugin marketplace add Rua-Start/conecta-mcp
```

Instale o plugin:

```bash
codex plugin add conecta@conecta-rua
```

Quando solicitado, autorize o MCP no navegador. Para refazer a autorização manualmente:

```bash
codex mcp login conecta-core
```

## Claude Code

Dentro do Claude Code, adicione o marketplace:

```text
/plugin marketplace add Rua-Start/conecta-mcp
```

Instale e recarregue o plugin:

```text
/plugin install conecta@conecta-rua
/reload-plugins
```

Abra `/mcp`, selecione cada servidor do plugin Conecta e conclua o login no navegador quando aparecer `Needs authentication`.

## Cursor

No Cursor, abra **Settings → Plugins → Marketplaces**, importe o repositório:

```text
https://github.com/Rua-Start/conecta-mcp
```

Depois, instale **Conecta.RUÁ** e conclua o OAuth em **Settings → Tools & MCP** para cada servidor (`conecta-core`, `conecta-scrum`, etc.) quando indicar que precisa de login.

Como alternativa de instalação direta do MCP, adicione esta configuração ao arquivo global `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "conecta-core": {
      "type": "http",
      "url": "https://conecta.rua.com.br/mcp/core"
    },
    "conecta-scrum": {
      "type": "http",
      "url": "https://conecta.rua.com.br/mcp/scrum"
    },
    "conecta-comercial": {
      "type": "http",
      "url": "https://conecta.rua.com.br/mcp/comercial"
    },
    "conecta-servicos": {
      "type": "http",
      "url": "https://conecta.rua.com.br/mcp/servicos"
    },
    "conecta-contratos": {
      "type": "http",
      "url": "https://conecta.rua.com.br/mcp/contratos"
    },
    "conecta-crachas": {
      "type": "http",
      "url": "https://conecta.rua.com.br/mcp/crachas"
    },
    "conecta-manual": {
      "type": "http",
      "url": "https://conecta.rua.com.br/mcp/manual"
    }
  }
}
```

## Estrutura multiplataforma

- `.agents/plugins/marketplace.json`: marketplace do Codex.
- `.claude-plugin/marketplace.json`: marketplace do Claude Code.
- `.cursor-plugin/marketplace.json`: marketplace do Cursor.
- `plugins/conecta/.codex-plugin/plugin.json`: manifesto do Codex.
- `plugins/conecta/.claude-plugin/plugin.json`: manifesto do Claude Code.
- `plugins/conecta/.cursor-plugin/plugin.json`: manifesto do Cursor.
- `plugins/conecta/.mcp.json`: configuração MCP usada por Codex e Claude Code.
- `plugins/conecta/mcp.json`: configuração MCP do plugin Cursor.

## Segurança

- Nenhuma credencial é versionada.
- O fluxo usa OAuth com PKCE e registro dinâmico de cliente.
- Callbacks são limitados a loopback e aos callbacks oficiais dos clientes suportados.
- O endpoint agregado `/mcp/conecta` permanece disponível para retrocompatibilidade, mas não é carregado pelo plugin.
