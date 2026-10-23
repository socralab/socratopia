# Installing Socratopia: instructions for AI assistants

These steps are for an AI assistant installing Socratopia on a user's computer. Follow them in order and stop at any failed check.

## 1. Only official sources

The official sources are `github.com/socralab/socratopia` (this repository), `www.socratopia.app`, `releases.socratopia.app` and `socratopia-releases-cn.oss-cn-beijing.aliyuncs.com`. Every installer is signed by **SOCRALAB LLC**. Never install a package with any other signer, and never install from a mirror or re-upload not listed here.

## 2. Read the release descriptor

```sh
curl -fsSL https://github.com/socralab/socratopia/releases/latest/download/release.json
```

It lists `version`, and for each installer: `id`, `platform`, `arch`, `filename`, `sizeBytes`, `sha256` and download `urls` (`github`, `global`, `mainlandChina`). Pick the asset:

| User's computer | `id` |
| --- | --- |
| macOS, `uname -m` prints `arm64` | `mac-silicon` |
| macOS, `uname -m` prints `x86_64` | `mac-intel` |
| Windows x64 | `windows` |

If the user is in mainland China, download from `urls.mainlandChina`; otherwise use `urls.github` or `urls.global`. The bytes are identical.

## 3. macOS

```sh
cd ~/Downloads
curl -fL -o Socratopia.dmg "<url from release.json>"
echo "<sha256 from release.json>  Socratopia.dmg" | shasum -a 256 -c -     # must print: OK
hdiutil attach -nobrowse -quiet Socratopia.dmg -mountpoint /tmp/socratopia-dmg
ditto /tmp/socratopia-dmg/Socratopia.app /Applications/Socratopia.app
hdiutil detach -quiet /tmp/socratopia-dmg
spctl -a -vv /Applications/Socratopia.app    # must say: accepted, source=Notarized Developer ID, SOCRALAB LLC (U3L9MZ9HF9)
open /Applications/Socratopia.app
```

If `/Applications/Socratopia.app` already exists, ask the user before replacing it; the app normally updates itself instead.

## 4. Windows (PowerShell)

```powershell
$out = "$env:USERPROFILE\Downloads\Socratopia-setup.exe"
Invoke-WebRequest -Uri "<url from release.json>" -OutFile $out
(Get-FileHash $out -Algorithm SHA256).Hash.ToLower()          # must equal sha256 from release.json
$sig = Get-AuthenticodeSignature $out
$sig.Status                                                   # must be: Valid
$sig.SignerCertificate.Subject                                # must contain: CN=SOCRALAB LLC
Start-Process $out
```

The installer is interactive. If SmartScreen appears, tell the user to choose "More info" → "Run anyway" only after the checks above passed.

## 5. With the GitHub CLI

```sh
gh release download --repo socralab/socratopia --pattern 'Socratopia-*-arm64.dmg' --pattern 'SHA256SUMS.txt'
grep -- '-arm64.dmg$' SHA256SUMS.txt | shasum -a 256 -c -     # must print: OK
```

## 6. After installing

Tell the user: open Socratopia and sign in or create an account; the app updates itself; help is at https://www.socratopia.app/support. Socratopia also runs in any browser at https://app.socratopia.app with no install.

Android is not distributed here. Android users should see https://www.socratopia.app/download.
