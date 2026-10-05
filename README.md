# A real Claude Code CLI session

I do all my work in Claude Code CLI — terminal only, no IDE. This is the best example I have of what that actually looks like end to end.

[`SESSION.md`](./SESSION.md) is a lightly cleaned export of a real session, working on [MigrateProof](https://github.com/Nivish-21/migrateproof) (finds the API changes your test suite would silently fail to catch).

The story: my laptop kept overheating, over and over, no matter what I killed. Turned out to be a genuine fork bomb — MigrateProof's own `scan` command runs `npm test` against its target directory, and when run against its own repo, its own test suite calls `scan` again, which runs `npm test` again, recursing without end. Killing the processes never helped, they just respawned faster than I could kill them.

What's in the transcript:
- Diagnosis from real `ps` / `docker` output, not guesswork
- A genuine third-party bug caught along the way: `@types/dockerode`'s `VolumeInspectInfo` type is missing a `CreatedAt` field the real Docker daemon actually returns, caught by verifying against the live daemon instead of trusting the types
- A mistake made and owned mid-session (a `docker container prune -f` took out an unrelated container of mine), checked for data loss, then fixed properly
- Two separate guards shipped as two separate real commits
- Measured result: 106s → 6s, 18 Docker containers → 0, 156/156 tests passing

Nothing in this transcript is edited for content. Long raw command output is truncated (marked `...[truncated]`), and a database connection string, a personal email, and a private session link were removed. Everything else — the reasoning, every command, every diff — is exactly what happened.
