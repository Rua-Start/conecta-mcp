# Conecta.RUÁ para Codex

Plugin do Codex que conecta aos servidores MCP do Conecta.RUÁ.

## Servidores incluídos

- Scrum
- Comercial
- Core
- Serviços
- Crachás

## Instalação

Adicione este repositório como marketplace:

```bash
codex plugin marketplace add Rua-Start/conecta-mcp
```

Depois, instale o plugin:

```bash
codex plugin add conecta@conecta-rua
```

Na primeira utilização, o Codex abrirá a autenticação OAuth do Conecta. As ferramentas disponíveis respeitam o usuário autenticado e suas permissões no sistema.

## Segurança

O plugin não contém tokens nem credenciais. A autenticação é feita diretamente em `https://conecta.rua.com.br`.
