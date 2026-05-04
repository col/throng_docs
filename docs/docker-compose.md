# Docker Compose

Throng runs each task in an isolated sandbox so that parallel work can't
interfere with itself. If your project includes a `docker-compose.yml`,
Throng will automatically bring it up alongside every dev session and shut it
down when the session ends.

This page explains how Throng manages those Compose projects and the small
changes you'll need to make so that multiple tasks can run side-by-side
without fighting over the same ports.

## How it works

When a dev session starts, Throng runs the equivalent of:

```bash
docker compose -p <unique-project-name> up -d
```

A unique project name per task means each session gets its own set of
containers, networks, and volumes — fully isolated from other tasks running
on your machine.

When Claude Code stops, Throng tears the environment down again with
`docker compose down`, so nothing is left running between sessions.

!!! note
    Throng only manages the Compose lifecycle. Your `docker-compose.yml`
    remains the source of truth for what services your project needs.

## Avoiding port conflicts

Because tasks may run in parallel, two sessions exposing the same host port
(say, Postgres on `5432`) would collide. To prevent that, Throng injects a
unique port for each declared service into the environment of the Compose
project it starts.

For this to work, your Compose file needs to read those values when binding
ports, and your application code needs to use the same values when
connecting.

### 1. Parameterize ports in `docker-compose.yml`

Use `${VAR:-default}` syntax so the file still works when you run it
directly outside of Throng:

```yaml
services:
  redis:
    image: redis:7-alpine
    ports:
      - "${REDIS_PORT:-6379}:6379"

  postgres:
    image: postgres:16
    ports:
      - "${POSTGRES_PORT:-5432}:5432"
```

The left-hand side is the host port — that's the one Throng overrides per
task. The right-hand side is the container port and stays fixed.

### 2. Use the same variables in your application

Your application connects to services on the host port, so it needs to read
the same environment variables. For example:

```python
import os

redis_port = int(os.environ.get("REDIS_PORT", 6379))
```

```javascript
const redisPort = Number(process.env.REDIS_PORT ?? 6379);
```

As long as your code and your Compose file agree on the variable name,
everything will line up — both in Throng (with injected ports) and in normal
local development (with the defaults).

## Lifecycle summary

| Event                          | What Throng does                          |
| ------------------------------ | ----------------------------------------- |
| Dev session starts             | `docker compose up -d` with a unique name |
| Claude Code is no longer running | `docker compose down`                   |

## Troubleshooting

- **Port still conflicts** — check that every `ports:` entry in your
  Compose file uses the `${VAR:-default}` form. A hard-coded host port will
  always collide across parallel tasks.
- **App can't reach a service** — make sure your application reads the same
  environment variable that the Compose file uses for the host port.
- **Containers from a previous session linger** — list them with
  `docker compose ls` and remove with
  `docker compose -p <project-name> down`.
