# Conecta.RUÁ para agentes de código

Plugins oficiais que conectam Codex, Claude Code e Cursor aos servidores MCP do Conecta.RUÁ.

## Formas de instalação

- **`conecta`**: pacote completo recomendado, com todos os dez servidores especializados.
- **`conecta-<domínio>`**: pacote mínimo, com somente o servidor escolhido.

Use uma das formas. Instalar `conecta` junto com um plugin individual duplica o mesmo servidor e suas tools no cliente.

| Plugin individual | Servidor MCP externo |
|---|---|
| `conecta-core` | `https://conecta.rua.com.br/mcp/core` |
| `conecta-ruacio` | `https://conecta.rua.com.br/mcp/ruacio` |
| `conecta-external-databases` | `https://conecta.rua.com.br/mcp/external-databases` |
| `conecta-ai-knowledge` | `https://conecta.rua.com.br/mcp/ai-knowledge` |
| `conecta-scrum` | `https://conecta.rua.com.br/mcp/scrum` |
| `conecta-comercial` | `https://conecta.rua.com.br/mcp/comercial` |
| `conecta-servicos` | `https://conecta.rua.com.br/mcp/servicos` |
| `conecta-contratos` | `https://conecta.rua.com.br/mcp/contratos` |
| `conecta-crachas` | `https://conecta.rua.com.br/mcp/crachas` |
| `conecta-manual` | `https://conecta.rua.com.br/mcp/manual` |

As mesmas tools estão disponíveis no chat interno do Conecta conforme tenant, módulo, permissões e escopo do usuário. Externamente, cada endpoint usa OAuth e aplica as mesmas regras de autorização no servidor.

O endpoint agregado `https://conecta.rua.com.br/mcp/conecta` continua disponível para integrações que desejem uma única conexão. O plugin completo usa os dez endpoints especializados para evitar truncamento de catálogos em clientes com paginação limitada.

## Codex

Adicione o marketplace:

```bash
codex plugin marketplace add Rua-Start/conecta-mcp
```

Instale o pacote completo:

```bash
codex plugin add conecta@conecta-rua
```

Ou instale apenas um domínio:

```bash
codex plugin add conecta-external-databases@conecta-rua
```

Quando solicitado, conclua o OAuth no navegador. Para refazer a autorização de um servidor:

```bash
codex mcp login conecta-external-databases
```

Abra uma nova tarefa depois de instalar ou atualizar o plugin para recarregar o catálogo.

## Claude Code

```text
/plugin marketplace add Rua-Start/conecta-mcp
/plugin install conecta@conecta-rua
/reload-plugins
```

Para uma instalação mínima, substitua `conecta` pelo nome do plugin individual. Em `/mcp`, conclua o login dos servidores instalados que aparecerem como `Needs authentication`.

## Cursor

Em **Settings → Plugins → Marketplaces**, importe:

```text
https://github.com/Rua-Start/conecta-mcp
```

Instale **Conecta.RUÁ** para todos os domínios ou somente o plugin individual desejado. Conclua o OAuth em **Settings → Tools & MCP**.

## Configuração MCP direta

Qualquer cliente compatível pode usar um endpoint sem instalar o marketplace:

```json
{
  "mcpServers": {
    "conecta-external-databases": {
      "type": "http",
      "url": "https://conecta.rua.com.br/mcp/external-databases"
    }
  }
}
```

Troque o nome e a URL conforme a tabela. Para uma única conexão agregada, use `conecta` e `/mcp/conecta`.

## Estrutura multiplataforma

- `.agents/plugins/marketplace.json`: marketplace do Codex.
- `.claude-plugin/marketplace.json`: marketplace do Claude Code.
- `.cursor-plugin/marketplace.json`: marketplace do Cursor.
- `plugins/conecta`: pacote completo.
- `plugins/conecta-<domínio>`: pacotes individuais.
- `.mcp.json`: configuração usada por Codex e Claude Code.
- `mcp.json`: configuração usada pelo Cursor.

## Segurança

- Nenhuma credencial é versionada no plugin.
- OAuth usa PKCE e registro dinâmico de cliente.
- O servidor revalida tenant, módulo, permissões e escopo em cada tool.
- O MCP de Bancos de Dados Externos nunca recebe nem altera senha ou chave privada TLS.
