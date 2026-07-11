# Conecta.RUÁ para Codex

Plugin do Codex que conecta ao servidor MCP unificado do Conecta.RUÁ.

## Módulos incluídos

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

Na primeira utilização, o Codex abrirá uma única autenticação OAuth do Conecta. Depois da autorização, Scrum, Comercial, Core, Serviços e Crachás ficam disponíveis na mesma conexão, sempre respeitando o usuário autenticado e suas permissões no sistema.

## Segurança

O plugin não contém tokens nem credenciais. A autenticação é feita diretamente em `https://conecta.rua.com.br`.
