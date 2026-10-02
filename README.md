# Conecta.RUÁ para agentes de código

Plugins oficiais que conectam Codex, Claude Code e Cursor aos servidores MCP do Conecta.RUÁ.

## Formas de instalação

- **`conecta`**: plugin principal recomendado, com todos os domínios em uma única conexão MCP: `https://conecta.rua.com.br/mcp/conecta`.
- **`conecta-<domínio>`**: plugin individual, com somente o servidor escolhido, mantido para compatibilidade e instalações restritas a um domínio.

Use uma das formas. Instalar `conecta` junto com plugins individuais disponibiliza as mesmas tools por conexões diferentes no cliente.

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

A partir da versão **0.7.0**, o plugin principal `conecta` usa somente o endpoint unificado `/mcp/conecta`, incluindo Conhecimento IA. As definições das tools são descobertas pelo cliente conforme suas capacidades de busca e carregamento sob demanda. Os plugins individuais e endpoints especializados continuam disponíveis.

A nova organização por grupos e o guia sob demanda exigem o backend **ConectaServer 1.1.0** implantado no Conecta. Publicar ou atualizar este plugin não implanta o backend.

Ao migrar de uma versão anterior, atualize o plugin `conecta`, desative os plugins individuais que estiverem instalados e conclua o OAuth da conexão `conecta` quando solicitado. Abra uma nova tarefa para recarregar a configuração e o catálogo. O MCP publica o catálogo completo com paginação para clientes compatíveis; a busca e o carregamento sob demanda das tools dependem do cliente.

## Descoberta por domínio

O endpoint principal organiza o catálogo em dez grupos. Os domínios maiores também se dividem em subgrupos por finalidade. Cada tool recebe título e descrição que identificam seu grupo; os nomes operacionais continuam compatíveis. Uma conexão MCP reúne os grupos sem depender de namespaces adicionais na configuração do cliente.

| Domínio (`domain`) | Finalidade |
|---|---|
| `core` | Identidade, tenant, permissões, busca global, notificações, rascunhos e administração autorizada de créditos IA. |
| `ruacio` | Dashboards, relatórios, análises e artefatos do Ruácio. |
| `external-databases` | Catálogos, regras e consultas autorizadas em bancos externos. |
| `ai-knowledge` | Bases autorizadas, pesquisa, consulta e gestão de Conhecimento IA. |
| `scrum` | Projetos, sprints, tasks, board e conhecimento do Scrum. |
| `comercial` | Clientes e operações comerciais autorizadas. |
| `servicos` | Chamados, trâmites e conhecimento de serviços. |
| `contratos` | Consulta e gestão de contratos. |
| `crachas` | Operações de crachás. |
| `manual` | Pesquisa e consulta ao Manual do Usuário. |

Os subgrupos atuais são:

- **Scrum**: Tarefas; Colaboração em tarefas; Sprints; Tempo e timer; Board; Configurações; Projetos e equipe; Base de conhecimento; Relatórios e acompanhamento.
- **Comercial**: Leads; Metas; Cliente Conhecer; CRM / Oportunidades; CRM / Propostas; CRM / Atividades; CRM / Perfil e cadastros; CRM / Acompanhamento.
- **Contratos**: Consulta e gestão; Cadastros; Financeiro e aditivos; Reajustes em lote; Relatórios.
- **Bancos Externos**: Consultas SQL; Catálogo e estrutura; Regras, notas e contexto; Administração de conexões.
- **Serviços**: Perfil e cadastros; Atendimento e trâmites; Consultas e soluções.

Cada subgrupo tem atualmente menos de dez tools operacionais. Essa organização ajuda na descoberta e evolui conforme novas ferramentas são adicionadas. O guia do domínio retorna `groups` e as instruções originais completas para que o agente consulte o catálogo vigente.

Para iniciar uma tarefa:

1. Chame `current-user-context-tool` para identificar usuário, tenant, permissões e domínios autorizados.
2. Chame `get-conecta-domain-guide` com `domain` igual ao slug autorizado da tabela para ler as instruções completas desse domínio sob demanda.
3. Quando o cliente oferecer busca de ferramentas, procure e carregue as tools necessárias à tarefa. Consulte também os resources indicados no guia e preserve a paginação em leituras integrais.

A busca e o carregamento sob demanda pertencem ao cliente. O plugin configura somente a conexão HTTP: não adiciona namespaces nem opções da API como `defer_loading`. O servidor continua revalidando tenant, módulo, permissões e escopo em cada chamada, inclusive nas conexões individuais. A publicação do plugin não comprova descoberta ou execução autenticada no cliente; essa verificação depende de uma sessão OAuth ativa no cliente utilizado.

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
codex mcp login conecta
```

Abra uma nova tarefa depois de instalar ou atualizar o plugin para recarregar o catálogo.

## Claude Code

```text
/plugin marketplace add Rua-Start/conecta-mcp
/plugin install conecta@conecta-rua
/reload-plugins
```

Para uma instalação mínima, substitua `conecta` pelo nome do plugin individual. Em `/mcp`, conclua o login da conexão `conecta` que aparecer como `Needs authentication`. Para plugins individuais, autorize a conexão correspondente.

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
    "conecta": {
      "type": "http",
      "url": "https://conecta.rua.com.br/mcp/conecta"
    }
  }
}
```

Para usar somente um domínio, troque o nome e a URL conforme a tabela de plugins individuais.

## Estrutura multiplataforma

- `.agents/plugins/marketplace.json`: marketplace do Codex.
- `.claude-plugin/marketplace.json`: marketplace do Claude Code.
- `.cursor-plugin/marketplace.json`: marketplace do Cursor.
- `plugins/conecta`: plugin principal com uma única conexão MCP.
- `plugins/conecta-<domínio>`: pacotes individuais.
- `.mcp.json`: configuração usada por Codex e Claude Code.
- `mcp.json`: configuração usada pelo Cursor.

## Segurança

- Nenhuma credencial é versionada no plugin.
- OAuth usa PKCE e registro dinâmico de cliente.
- O servidor revalida tenant, módulo, permissões e escopo em cada tool.
- O MCP de Bancos de Dados Externos nunca recebe nem altera senha ou chave privada TLS.
