# Discord Bot Design

## Commands (initial ideas)

- `/whitelist request <username-or-uuid>`
  - User requests access to the server.
  - Bot looks up UUID via playerdb.co.
  - Bot shows result to requester and asks for confirmation.

- Approver actions:
  - Approve temporary
  - Approve permanent
  - Deny (with optional reason)

- (Future) Admin commands:
  - `/mc op <username>`
  - `/mc deop <username>`
  - `/mc status`

## Roles and Permissions

- Requesters:
  - Anyone in a specific Discord server/channel/role can request whitelist.

- Approvers:
  - Users with a specific role (e.g. `Server Approver`) can approve/deny.

- Admins:
  - Smaller group with full control (e.g. `/op`, restarts etc.).

## High-Level Flow (Whitelist Request)

1. Requester uses `/whitelist request <username-or-uuid>`.
2. Bot calls playerdb.co and shows the found player data.
3. Requester confirms or cancels.
4. If confirmed, a pending request is created for approvers.
5. Approvers approve (temp or permanent) or deny (optional reason).
6. Bot sends the decision and result back to the requester.
7. Backend updates the Minecraft server accordingly.
