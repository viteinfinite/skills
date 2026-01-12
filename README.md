# Claude Plugin Marketplace (viteinfinite)

A small marketplace for installing the skills in this repository as Claude plugins.

## Marketplace

Marketplace name: `viteinfinite-claude-marketplace`

## Plugins

- `commit-style-enforcer`: Generates properly formatted commit messages
- `documentation-updater`: Keeps project documentation accurate after changes

## Install

Add the marketplace from GitHub:

```shell
/plugin marketplace add viteinfinite/claude-plugin-marketplace
```

Install a plugin:

```shell
/plugin install commit-style-enforcer@viteinfinite-claude-marketplace
```

## Local testing

```shell
/plugin marketplace add ./
/plugin install documentation-updater@viteinfinite-claude-marketplace
```
