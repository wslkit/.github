<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/hawserhq/hawser/main/assets/hawser-mark-ondark.svg">
    <img alt="Hawser" src="https://raw.githubusercontent.com/hawserhq/hawser/main/assets/hawser-mark.svg" width="120" height="120">
  </picture>
</p>

<h1 align="center">Hawser</h1>

<p align="center"><strong>The upstream open source Docker Engine on Windows, via WSL2.</strong><br>
No licence fees. No Electron. No Kubernetes you did not ask for.</p>

<p align="center"><em><strong>hawser</strong> (n.) — the heavy line that moors a ship to the dock. It holds fast.</em></p>

---

Docker Desktop is a licensed product with a GUI you did not want and a
background footprint you cannot turn off. The engine underneath it is Apache-2.0
and has been all along.

Hawser runs **that engine** — real `dockerd`, built from source at pinned
upstream tags — in a dedicated WSL2 distro, and bridges it to `docker.exe` over
a named pipe at the speed you already expect. Install once and `docker ps` works
forever, on laptops and CI runners alike.

```powershell
hawser install                                  # engine, docker context, autostart
docker run --rm hello-world
```

## What it does that Docker Desktop's architecture cannot

- **Gives the RAM back.** `hawser config set idle-timeout 30m` stops a quiet
  engine and wakes it on your next `docker` command. An always-on engine has no
  such state to offer.
- **Reversible engine upgrades.** `hawser engine upgrade` and
  `hawser engine rollback` move between pinned engine versions with your images,
  containers and volumes untouched.
- **Snapshots of the whole engine.** Save and restore every image, container and
  volume as one named, checksummed archive — a runner's clean slate, or a
  checkpoint before something risky.
- **Local admission control.** Hawser already sits in the request path, so it
  can refuse `--privileged`, host namespaces, or images from registries this
  machine has ruled out — before the engine sees them.
- **An audit log of what actually happened.** Every image pull, container
  create/start/stop, exec and build that crossed the bridge.
- **Works behind the corporate proxy.** Host CA import, proxy configuration,
  VPN-aware MTU, and air-gapped installs from a verified bundle.

## Pinned, verified, reproducible

Nothing is ever fetched as "latest". The engine rootfs is built from source at
pinned upstream tags whose commit SHAs are verified during the build, on an
Alpine base pinned by digest. Every release carries a SHA-256, SLSA build
provenance, and a cosign keyless signature — and `hawser install` refuses a
rootfs that does not verify.

## The repositories

| | |
| --- | --- |
| [**hawser**](https://github.com/hawserhq/hawser) | the engine, the bridge, the supervisor, the CLI — one Go binary |
| [**hawser-vscode**](https://github.com/hawserhq/hawser-vscode) | engine status and control inside VS Code |
| [**setup-hawser**](https://github.com/hawserhq/setup-hawser) | one-line Hawser on a Windows CI runner |
| [**scoop-hawser**](https://github.com/hawserhq/scoop-hawser) | the Scoop bucket |
| [**wsldisk**](https://github.com/hawserhq/wsldisk) · [**wsldrive**](https://github.com/hawserhq/wsldrive) | WSL2 disk tooling |

## Status

**v0.3, pre-release.** Installable and working as a daily driver. Binaries are
not signed yet, so SmartScreen will warn — that work is tracked in the open.

📖 **[Documentation](https://hawserhq.github.io/hawser/)** ·
🐛 **[Issues](https://github.com/hawserhq/hawser/issues)** ·
📋 **[Roadmap](https://github.com/hawserhq/hawser/blob/main/ROADMAP.md)**

---

<sub>Apache-2.0. Docker and the Docker logo are trademarks of Docker, Inc.
Hawser is not affiliated with or endorsed by Docker, Inc.</sub>
