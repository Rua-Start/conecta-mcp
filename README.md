# Conecta.RUÁ para agentes de código

Plugin oficial que conecta Codex, Claude Code e Cursor ao servidor MCP unificado do Conecta.RUÁ.

## Módulos incluídos

- Core
- Scrum
- Comercial
- Serviços
- Crachás

Todos os clientes usam o mesmo endpoint:

```text
https://conecta.rua.com.br/mcp/conecta
```

O plugin não contém tokens nem credenciais. Cada cliente abre o OAuth do Conecta e recebe apenas as ferramentas permitidas para o usuário autenticado.

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
codex mcp login conecta
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

Abra `/mcp`, selecione o servidor do plugin Conecta e conclua o login no navegador quando aparecer `Needs authentication`.

## Cursor

No Cursor, abra **Settings → Plugins → Marketplaces**, importe o repositório:

```text
https://github.com/Rua-Start/conecta-mcp
```

Depois, instale **Conecta.RUÁ** e conclua o OAuth em **Settings → Tools & MCP** quando o servidor indicar que precisa de login.

Como alternativa de instalação direta do MCP, adicione esta configuração ao arquivo global `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "conecta": {
      "type": "http",
      "url": "https://conecta.rua.com.br/mcp/conecta"
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
- Os endpoints MCP especializados continuam disponíveis apenas para retrocompatibilidade.
