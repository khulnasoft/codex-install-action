# codex-install-action

This action downloads the codex CLI and installs the Nix packages defined in your `codex.json`.

[![version](https://img.shields.io/github/v/release/khulnasoft/codex-install-action?color=green&label=version&sort=semver)](https://github.com/khulnasoft/codex-install-action/releases) [![tests](https://github.com/khulnasoft/codex-install-action/actions/workflows/test.yaml/badge.svg)](https://github.com/khulnasoft/codex-install-action/actions/workflows/test.yaml?branch=main)

## Example Workflow

```
name: Testing with codex

on: push

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Install codex
        uses: khulnasoft/codex-install-action@main

      - name: Run arbitrary commands
        run: codex run -- echo "done!"

      - name: Run a script called test
        run: codex run test
```

## Configure Action

### Action Inputs

| Input argument           | description                                                                           | default               |
| ------------------------ | ------------------------------------------------------------------------------------- | --------------------- |
| project-path             | Path to the folder that contains a valid `codex.json`                                | repo's root directory |
| enable-cache             | Cache the entire Nix store in github based on your `codex.json`                      | false                 |
| refresh-cli              | Specify whether the CLI should be redownloaded                                        | false                 |
| codex-version           | Specify codex CLI version you want to pin to. Only supports >0.2.2                   | latest                |
| sha256-checksum          | Specify an explicit checksum for the codex binary                                    |                       |
| disable-nix-access-token | Disable configuration of nix access-tokens with the GitHub token used in the workflow | false                 |
| skip-nix-installation    | Skip the installation of nix                                                          | false                 |

### Example Configuration

Here's an example job with all inputs:

```
- name: Install codex
  uses: khulnasoft/codex-install-action@main
  with:
    project-path: 'path-to-folder'
    enable-cache: 'true'
    refresh-cli: 'false'
    codex-version: 0.10.4
    disable-nix-access-token: 'false'
    sha256-checksum: f5907e5782f6e1f5a7ca32c8ae2a0a81618549314bab237174a46fb216f43809
```
