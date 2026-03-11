# Bagunserver2

Minecraft 1.21.1 NeoForge server running via [itzg/docker-minecraft-server](https://github.com/itzg/docker-minecraft-server).

Mods are managed in two ways: Modrinth mods are declared in `mods.txt` and auto-downloaded on startup; manual JARs can be dropped into the `mods/` folder.

## Requirements

- [Docker](https://docs.docker.com/get-docker/) with the Compose plugin

## Running

```bash
# Start the server (detached)
docker compose up -d

# Follow logs
docker compose logs -f

# Stop the server
docker compose down
```

## Managing Mods

### Modrinth mods

Edit `mods.txt` and add the mod's Modrinth slug — the part after `/mod/` in the URL (e.g. `modrinth.com/mod/ferrite-core` → `ferrite-core`):

```
# mods.txt
ferrite-core
create
jei
```

Restart the server to apply changes. Mods removed from the list are deleted automatically.

### Manual JARs

For mods not available on Modrinth (private mods, paid mods, custom builds), drop the `.jar` file into the `mods/` folder and restart. The server picks them up automatically.
This has not yet been tested if it actually works, so maybe something will break.

## Server Commands

```bash
docker compose exec mc rcon-cli <command>

# attach
docker compose exec mc rcon-cli

# Examples
docker compose exec mc rcon-cli op YourUsername
docker compose exec mc rcon-cli whitelist add Player
docker compose exec mc rcon-cli list
```

## Configuration

Key settings in `docker-compose.yml`:

| Variable | Default | Description |
|---|---|---|
| `MEMORY` | `4G` | Heap size allocated to the JVM |
| `MAX_PLAYERS` | `20` | Player slot limit |
| `DIFFICULTY` | `normal` | Game difficulty |
| `ONLINE_MODE` | `true` | Set to `false` for offline/LAN |
| `OPS` | _(unset)_ | Comma-separated op usernames |
| `WHITELIST` | _(unset)_ | Comma-separated whitelisted usernames |

World data and server files are persisted in the `data/` directory.
