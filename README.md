# xv releases

Release binaries and install scripts for **xv**, the crosstache secrets
manager (Azure Key Vault, AWS Secrets Manager, and local age-encrypted
storage). The source repository is private; this repository only carries
signed release artifacts and the install scripts, and is written by the
release pipeline — do not edit it by hand.

## Install

macOS / Linux:

    curl -sSL https://raw.githubusercontent.com/bziobnic/xv-releases/main/install.sh | bash

Windows (PowerShell):

    irm https://raw.githubusercontent.com/bziobnic/xv-releases/main/install.ps1 | iex

Already installed? `xv upgrade` checks this repository for new releases,
verifies the checksum and signature, and replaces the binary in place.
Installs at v0.44.0 or older looked for updates in the private source
repository and will fail; reinstall once with the install script above, and
`xv upgrade` will work normally from then on.

## Manual download and verification

Every release carries `xv-linux-x64.tar.gz`, `xv-macos-intel.tar.gz`,
`xv-macos-apple-silicon.tar.gz` and `xv-windows-x64.zip`, each with a
`.sha256` checksum and a `.minisig` signature. Verify with
[minisign](https://jedisct1.github.io/minisign/):

    minisign -Vm xv-linux-x64.tar.gz -P RWRuXFh34rB613dgsXyAMmtKvYK0SFwxq4i44dhGFXVTrhAQ7hJXf6Ym

## GitHub Action

```yaml
- uses: bziobnic/xv-releases@v1
  with: { version: v0.46.0, backend: azure, vault: myproj-prod-kv }
```
