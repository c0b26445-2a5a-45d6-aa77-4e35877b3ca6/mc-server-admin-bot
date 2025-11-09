# Discord Bot (mc-server-admin-bot)

This folder contains the Discord-facing part of the project.

Responsibilities:
- Connect to Discord as a bot user
- Handle commands and events
- Check Discord roles/permissions
- Translate user actions into backend actions (whitelist, admin commands, etc.)

This bot does **not** directly talk to Minecraft:
that logic will live in the `mc_backend/` folder.

## Discord Bot Setup (Planned)

1. **Create a Discord application & bot user**
   - Use the Discord Developer Portal.
   - Add a bot user and copy its token.
   - Invite the bot to a development Discord server.

2. **Configure environment variables**
   - Store the bot token in an environment variable (e.g. `DISCORD_BOT_TOKEN_DEV`).
   - Do **not** commit tokens to Git.
   - Use a `.env` file locally that is ignored by Git.

3. **Select a language and Discord library**
   - Example options:
     - Python + a Discord library
     - Node.js + a Discord library
   - Once decided, set up the project structure inside `bot/`.

4. **Implement a basic bot skeleton**
   - First goal: connect to Discord and respond to a simple test command.
   - This will likely become version `v0.1.0` later.
