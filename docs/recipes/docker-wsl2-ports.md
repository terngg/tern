# Recipe: Docker & WSL2 port conflicts

When a local Node.js server fails with `EADDRINUSE: address already in use :::3000`, the process holding the port is not always obvious. Docker containers and WSL2 networking layers often own the port behind a proxy process (`wslhost.exe`, Docker Desktop helpers), so killing the wrong PID or ignoring containers leaves the conflict in place.

This recipe shows how to diagnose and clear those cases with `tern port`.

## 1. How `tern port` discovers listening PIDs

```bash
tern port 3000
```

Tern inspects the OS for a process in the **LISTEN** state on that TCP port and prints **PID**, **process name**, and (when available) **command**.

| Platform | Discovery tools (in order) |
| --- | --- |
| macOS / Linux | `lsof -i :PORT -sTCP:LISTEN`, then `ss -tulpn`, then `fuser PORT/tcp` |
| Windows | `netstat -ano -p tcp` for a `LISTENING` row, then `tasklist` for the process name |

If nothing is listening, Tern reports the port as free. Inspect mode is read-only; it does not terminate anything.

## 2. Ports held by Docker containers

Docker publishes container ports on the host. Tern may show a Docker-related process (or a proxy) as the holder. Prefer stopping the container over killing the proxy PID:

```bash
# See which container publishes the port
docker ps --format 'table {{.ID}}\t{{.Names}}\t{{.Ports}}' | grep 3000

# Stop that container
docker stop <container_id_or_name>

# Confirm the host port is free
tern port 3000
```

If you use Compose:

```bash
docker compose ps
docker compose stop <service>
```

Only after the container is stopped should you use `tern port 3000 --kill` if a leftover host process still holds the port.

## 3. WSL2 mirrored networking collisions

With WSL2, Windows and the Linux distro can both appear to bind the same port. Common symptoms:

- `tern port 3000` inside WSL shows a Node/Linux PID, but Windows still reports the port busy (or the reverse).
- The Windows side lists `wslhost.exe` or a Docker Desktop helper as the listener.

Suggested sequence:

1. Run `tern port 3000` **inside WSL** and note the Linux PID/name.
2. In **Windows** (PowerShell or CMD), run `tern port 3000` or `netstat -ano -p tcp` and note any `LISTENING` PID (often `wslhost.exe` or Docker).
3. Stop the real owner first:
   - App or dev server in WSL → stop it there, or `tern port 3000 --kill` inside WSL.
   - Docker → `docker stop` as above.
   - Stale WSL forwarding → exit the distro (`exit`) or, from Windows, `wsl --shutdown` (stops **all** WSL distros; save work first).
4. Re-check with `tern port 3000` on both sides.

Mirrored/localhost forwarding means freeing the port only in Windows or only in WSL is sometimes not enough; clear the side that still shows `LISTENING`.

## 4. Using `tern port --kill` safely

```bash
# Inspect first (always)
tern port 3000

# Terminate with interactive confirmation (default)
tern port 3000 --kill

# Skip the prompt (scripts / CI-style use)
tern port 3000 --kill --yes

# Stronger signal if a graceful stop fails
tern port 3000 --kill --force --yes
```

Behavior notes:

- Without `--kill`, Tern only reports the process.
- `--kill` asks for confirmation unless `--yes` is set.
- On Unix, default kill is `SIGTERM`; `--force` uses `SIGKILL`.
- On Windows, Tern uses `taskkill` (`/F` when `--force`).
- Do **not** kill system-critical PIDs, and prefer `docker stop` for container-published ports so the runtime can clean up cleanly.

If kill fails, Tern suggests `--force` or checking process ownership/permissions.

## Related commands

```bash
# Explain EADDRINUSE with local rules (no network)
tern why "EADDRINUSE: address already in use :::3000"

# Doctor may also flag configured project ports
tern doctor
```
