# Downloads

| File | Version | SHA-256 |
| --- | --- | --- |
| [freeagentcoder-0.4.0.vsix](freeagentcoder-0.4.0.vsix) | 0.4.0 | `46b7a86188820f5cfe78516c6a3bf01dff9e17e30568bfe5e273fea01c626d81` |

## Install from the file

1. Download the `.vsix` file.
2. In VS Code, open the Command Palette (`Ctrl+Shift+P`) and run **Extensions: Install from VSIX…**
3. Pick the file.

Installing from the Marketplace instead gets you automatic updates.

## Check the file

PowerShell:

```powershell
Get-FileHash freeagentcoder-0.4.0.vsix -Algorithm SHA256
```

macOS or Linux:

```bash
shasum -a 256 freeagentcoder-0.4.0.vsix
```

The result should match the SHA-256 above.
