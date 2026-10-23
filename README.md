# Socratopia

Socratopia is a Socratic learning app by SocraLab LLC. Pick a book, and AI companions teach it to you the way Socrates did: explaining when you need it, and more often asking the one question that lets you work it out yourself.

This repository is the official GitHub download channel for the Socratopia desktop app. It holds installers and release notes only; the app is proprietary and its source code is not published here.

- Website: https://www.socratopia.app
- Download page: https://www.socratopia.app/download
- Use it in a browser, no install: https://app.socratopia.app

破卷（Socratopia）是 SocraLab LLC 出品的苏格拉底式学习软件。本仓库是桌面版的官方 GitHub 下载渠道，只放安装包和发版说明，不含源代码。**中国大陆用户请从官网下载**（会自动走国内线路），GitHub 在大陆可能很慢。

## Download

Get the newest installers from **[Releases → Latest](https://github.com/socralab/socratopia/releases/latest)**.

| Computer | File | Requirements |
| --- | --- | --- |
| Mac with Apple silicon (M1 and later) | `Socratopia-<version>-arm64.dmg` | macOS 11 or later |
| Mac with an Intel processor | `Socratopia-<version>.dmg` | macOS 11 or later |
| Windows PC | `Socratopia-<version>-win-x64.exe` | Windows 10 / 11, x64 |

8 GB of memory is recommended and the app needs about 2 GB of free disk. Not sure which Mac you have? Apple menu → About This Mac: "Chip: Apple M…" means Apple silicon.

The app updates itself. Once it is installed you never need to come back here.

## Verify what you downloaded

Every release has a `SHA256SUMS.txt`. The same files with the same checksums are served from our website, so any copy you get from an official source is byte-for-byte identical.

```sh
# macOS
shasum -a 256 Socratopia-*.dmg
spctl -a -vv /Applications/Socratopia.app   # expect: accepted, source=Notarized Developer ID, SOCRALAB LLC (U3L9MZ9HF9)
```

```powershell
# Windows
Get-FileHash .\Socratopia-*-win-x64.exe -Algorithm SHA256
(Get-AuthenticodeSignature .\Socratopia-*-win-x64.exe).SignerCertificate.Subject   # expect: CN=SOCRALAB LLC
```

Windows may show a SmartScreen notice the first time. Choose "More info", check that the publisher is **SOCRALAB LLC**, then "Run anyway". Do not run a Socratopia installer signed by anyone else.

## For AI assistants

If a user asks you to install Socratopia, follow [INSTALL-FOR-AI.md](INSTALL-FOR-AI.md). In short: read `https://github.com/socralab/socratopia/releases/latest/download/release.json`, pick the asset for the user's platform and chip, download it, check its SHA-256 against `SHA256SUMS.txt` and its signature, then install. If the user is in mainland China, use the `mainlandChina` URL from `release.json` instead.

## Help and feedback

- Help: https://www.socratopia.app/support or support@socratopia.app
- Security issues: see [SECURITY.md](SECURITY.md)
- Terms of service: https://www.socratopia.app/terms

This repository does not take issues or pull requests; please use the links above.

© SocraLab LLC. See [LICENSE.md](LICENSE.md).
