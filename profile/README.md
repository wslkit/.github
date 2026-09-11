<h1 align="center">wslkit</h1>

<p align="center"><strong>Native Windows tools for WSL2.</strong><br>
Small, single-binary, no admin rights, no Electron.</p>

---

WSL2 is the best Linux on Windows there has ever been, and the tooling around
it is thin. These fill gaps that shipped tools leave: running containers
without a licensed desktop app, reclaiming disk a VHDX will not give back,
seeing where the space actually went.

Each is a native Windows binary that does one thing, with a `--json` mode so it
composes into scripts and CI.

## Projects

### [skrog](https://github.com/wslkit/skrog) — Docker Engine on Windows

The upstream open source Docker Engine, in a dedicated WSL2 distro, bridged to
`docker.exe` over a named pipe. No licence fees, no Electron, no Kubernetes you
did not ask for.

```powershell
irm https://wslkit.github.io/skrog/install.ps1 | iex
skrog install
docker run --rm hello-world
```

It does things Docker Desktop's architecture cannot: **idle-stop** gives the
RAM back and wakes on the next `docker` command; **reversible engine upgrades**
move between pinned versions with your images intact; **snapshots** save and
restore the whole engine as one checksummed archive; **admission control**
refuses `--privileged` or untrusted registries before the engine sees them; and
an **audit log** records what actually crossed the bridge. Built for corporate
networks too — host CA import, proxies, VPN-aware MTU, air-gapped installs.

📖 [Documentation](https://wslkit.github.io/skrog/) ·
🔌 [VS Code extension](https://github.com/wslkit/skrog-vscode) ·
🏗️ [CI action](https://github.com/wslkit/setup-skrog)

### [wsldisk](https://github.com/wslkit/wsldisk) — reclaim WSL2 disk space

Compact, move and inspect WSL2 virtual disks from one native CLI. No admin
rights, no PowerShell incantations, no Hyper-V.

### [wsldrive](https://github.com/wslkit/wsldrive) — WSL2 drive tooling

---

## Pinned, verified, reproducible

Nothing is fetched as "latest". Releases carry a SHA-256, SLSA build
provenance and a cosign keyless signature, so a download ties back to the
workflow, the repository and the commit that produced it.

<sub>Apache-2.0. Not affiliated with Microsoft or Docker, Inc. "WSL" and
"Windows Subsystem for Linux" are trademarks of Microsoft; these are
independent tools that work with it.</sub>
