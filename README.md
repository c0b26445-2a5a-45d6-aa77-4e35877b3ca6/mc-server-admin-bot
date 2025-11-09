# mc-server-admin-bot

A Discord bot for administering a Minecraft server from Discord – starting with whitelist approvals and expanding to permissions and other server controls (e.g. `/op`, restarts, status).

---

## Features

> **Current status:** early development / planning phase.

Planned features:

- [ ] Request-based whitelist management
  - [ ] Users can request to be whitelisted via a Discord command ([Issue #2](https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot/issues/2))
  - [ ] UUID lookup & validation via `playerdb.co` ([Issue #3](https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot/issues/3))
  - [ ] Requester confirmation of the found player ([Issue #3](https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot/issues/3))
  - [ ] Approver review (approve / deny with optional reason) ([Issue #4](https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot/issues/4))
  - [ ] Feedback messages to the requester ([Issue #6](https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot/issues/6))

- [ ] Temporary vs permanent whitelist ([Issue #5](https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot/issues/5))
  - [ ] Temporary add (runtime only)
  - [ ] Permanent add (update server config / compose + handle restart)

- [ ] Server admin actions (future) ([Issue #8](https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot/issues/8))
  - [ ] Grant/remove operator (`/op` / `/deop`)
  - [ ] Server status (online/players)
  - [ ] Safe restart / maintenance commands

- [ ] Role-/permission-based access control in Discord ([Issue #6](https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot/issues/6))

---

## Architecture Overview

High-level components (planned):

- **Discord Bot**
  - Handles commands, interactions, and permissions in Discord
  - Communicates with the backend for whitelist / admin actions

- **Minecraft Backend**
  - Executes server commands via Docker or RCON
  - Manages whitelist and (later) other admin actions

- **Configuration**
  - Environment-specific settings (Dev vs Prod)
  - Discord tokens, RCON credentials, server addresses, etc.

---

## Environments

Planned environments:

- **Local Development**
  - Test Discord server & test bot
  - Local test Minecraft server (via Docker)
  - Safe sandbox for trying new features

- **Production**
  - Real Discord server & bot
  - Real Minecraft server (Docker)
  - Uses stricter permissions and more cautious defaults

Configuration will be separated by environment (e.g. different `.env` files or config sections).

---

## Requirements

> Exact stack and versions TBD.

- Programming language: **TBD** (e.g. Node.js / Python / other)
- Discord bot framework: **TBD**
- Minecraft server:
  - Dockerized Minecraft server
  - RCON access or Docker command access
- Access to `playerdb.co` API for UUID lookup

---

## Setup (High-Level)

> This is a conceptual overview. Details will be added as the implementation progresses.

1. **Clone the repository**

   ```bash
   git clone https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot.git
   cd mc-server-admin-bot
   ```

2. **Create and configure a Discord application & bot**

- Create a Discord application in the Developer Portal
- Add a bot user and copy its token
- Invite the bot to your test Discord server with the required permissions

3. **Prepare Minecraft server access**

- Ensure your Minecraft server is running in Docker or is reachable via RCON
- Configure RCON / Docker access credentials

4. **Configure environment variables**

- Create a development config (e.g. `.env.development` or similar)
- Add:
  - Discord bot token
  - Minecraft server host/port
  - RCON/Docker credentials
  - Any other required settings

5. **Run the bot in development mode**

   - (Details TBD when implementation is in place.)

## Development Workflow

This project uses a simple Git workflow:

- `main` branch
  - Always intended to be in a deployable / working state
  - Mirrors what can safely run on the production server
- Feature branches
  - Named like `feature/whitelist-flow`, `feature/op-command`, etc.
  - Used for developing new features and experiments
  - Merged into `main` once tested and stable

Example flow:

1. **Update `main`:**

   ```bash
   git switch main
   git pull origin main
   ```

2. **Create a feature branch:**

   ```bash
   git clone https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot.git
   cd mc-server-admin-bot
   git switch -c feature/whitelist-flow
   ```

3. **Develop & test locally**

4. **Commit and push:**

   ```bash
   git commit -S -m "feat: add basic whitelist request command"
   git push -u origin feature/whitelist-flow
   ```

5. **Merge back into `main` when stable**

## Versioning

This project is intended to follow Semantic Versioning (`MAJOR.MINOR.PATCH`), starting with pre-1.0 versions:

- `0.x.y` – development phase, APIs and behavior may change
- Tag examples (future):
- `v0.1.0` – first working bot skeleton
- `v0.2.0` – whitelist request & approval flow
- `v0.3.0` – operator (`/op`) management

Tags will be created on commits that represent stable, deployable versions.

## Commit Message Conventions

This project uses simple, structured commit messages inspired by "Conventional Commits".
The idea is to make the Git history easier to read and understand.

Common prefixes:

- `feat:` – a new feature  
  - Example: `feat: add whitelist request command`

- `fix:` – a bug fix  
  - Example: `fix: handle invalid UUID response`

- `docs:` – documentation changes only (README, comments, etc.)  
  - Example: `docs: document whitelist approval flow`

- `test:` – adding or updating tests  
  - Example: `test: add tests for whitelist approval`

- `refactor:` – code changes that do not change behavior (cleanup, re-structuring)  
  - Example: `refactor: split whitelist logic into separate module`

- `chore:` – maintenance tasks, setup, config, tooling, etc.  
  - Example: `chore: initialize project structure`

These prefixes are mainly for humans:
they help to quickly see *what kind* of change a commit introduces.

> *The goal is not to be perfect, but to keep the history understandable for myself (and any future contributors).*


## Roadmap (Draft)

- [ ] Define technology stack (language, Discord library, etc.)
- [ ] Implement basic bot connection & health check command ([Issue #1](https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot/issues/1))
- [ ] Implement end-to-end whitelist request & approval flow ([Issue #2](https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot/issues/2))
- [ ] Implement UUID lookup and check ([Issue #3](https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot/issues/3))
- [ ] Implement temp vs permanent whitelist handling ([Issue #5](https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot/issues/5))
- [ ] Add admin commands (`/op`, `/deop`, status) ([Issue #8](https://github.com/c0b26445-2a5a-45d6-aa77-4e35877b3ca6/mc-server-admin-bot/issues/8))
- [ ] Improve configuration and logging
- [ ] Document deployment steps for production

## License
> TODO: Choose a license (e.g. MIT, Apache-2.0) and add it here.
