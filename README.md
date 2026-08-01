# hanzo.vim

[![Vim](https://img.shields.io/badge/VIM-%2311AB00.svg?style=for-the-badge&logo=vim&logoColor=white)](https://www.vim.org/) [![Neovim](https://img.shields.io/badge/NeoVim-%2357A143.svg?&style=for-the-badge&logo=neovim&logoColor=white)](https://neovim.io/)

An AI plugin for Vim and Neovim: generate and edit text in a buffer, explain or refactor a
selection, and run a code cell against a Jupyter kernel — all through `:Hanzo*` commands
without leaving the editor.

Requires Vim 8.0+ or Neovim 0.8+, and Python 3.10+.

## Install

Clone into your plugin path. `packload`, Vim:

```bash
git clone --depth 1 https://github.com/hanzoai/hanzo.vim \
  ~/.vim/pack/git-plugins/start/hanzo.vim
```

Neovim:

```bash
git clone --depth 1 https://github.com/hanzoai/hanzo.vim \
  ~/.local/share/nvim/site/pack/git-plugins/start/hanzo.vim
```

Windows:

```bash
git clone --depth 1 https://github.com/hanzoai/hanzo.vim \
  ~/vimfiles/pack/git-plugins/start/hanzo.vim
```

With [vim-plug](https://github.com/junegunn/vim-plug):

```vim
Plug 'hanzoai/hanzo.vim'
```

Then, so `:help` works:

```vim
packloadall | silent! helptags ALL
```

## First use

Set the model and the endpoint you want to talk to, then start the bridge:

```vim
let g:hanzo_model = 'zen5-coder'
let g:hanzo_provider = 'hanzo'
```

```vim
:HanzoStart          " start the bridge process
:HanzoStatus         " check it came up
:Hanzo write a test for this function
```

Commands, all of them defined in `plugin/hanzo.vim`:

| Command | What it does |
| --- | --- |
| `:Hanzo [prompt]` | Generate into the buffer |
| `:HanzoComplete` | Complete at the cursor |
| `:HanzoExplain` | Explain the selection |
| `:HanzoFix` | Fix the selection |
| `:HanzoTests` | Write tests for the selection |
| `:HanzoDocs` | Write docs for the selection |
| `:HanzoReview` | Review the selection |
| `:HanzoModel <id>` · `:HanzoModels` | Set or list the model |
| `:HanzoMode <mode>` | Switch mode |
| `:HanzoEval <expr>` · `:HanzoEvalLine` · `:HanzoEvalSelection` · `:HanzoRepl <kernel>` | Evaluate through a Jupyter kernel |
| `:HanzoStart` · `:HanzoStop` · `:HanzoStatus` · `:HanzoVersion` | Manage the bridge |

Configuration variables: `g:hanzo_model`, `g:hanzo_provider`, `g:hanzo_port`,
`g:hanzo_mode`, `g:hanzo_auto_start`, `g:hanzo_diagnostics`, `g:hanzo_debug`,
`g:hanzo_set_default_keybinds`.

> The defaults compiled into `plugin/hanzo.vim` today still point at a local endpoint and
> a non-Hanzo model id. Set `g:hanzo_model` and `g:hanzo_provider` yourself until that is
> fixed; `zen5-coder` and `enso` are the ids to reach for. The full catalog is
> `curl https://catalog.hanzo.ai/v1/models`.

## Optional integrations

Detected automatically if you have them:

- [nui.nvim](https://github.com/MunifTanjim/nui.nvim) — Neovim UI
- [significant.nvim](https://github.com/ElPiloto/significant.nvim) — animated signs
- [ALE](https://github.com/dense-analysis/ale) — fixing problems in generated code

## Docs

`:help neural` in the editor, [`doc/`](doc/) and [`docs/`](docs/) in the repository, and
[`LLM.md`](LLM.md) for the code layout. The bridge itself is
[`python3/bridge.py`](python3/bridge.py).

## Lineage

A fork of [dense-analysis/neural](https://github.com/dense-analysis/neural). The `:Neural`
commands and the buffer-editing machinery come from there and still work; the `:Hanzo*`
commands, the bridge and the REPL integration are ours. Upstream's licence is preserved in
[LICENSE.md](LICENSE.md), and this fork is not affiliated with or endorsed by that project.
