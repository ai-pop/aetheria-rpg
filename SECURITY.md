# Security

## Reporting a vulnerability

Do not publish API keys, access tokens, private prompts, save files containing personal information, or unredacted diagnostics in a public issue.

For ordinary bugs, use the issue tracker after removing secrets. For a vulnerability that should not be public, use GitHub's private vulnerability reporting feature when available.

## Local secrets

Aetheria stores provider keys locally under:

```text
%APPDATA%\Godot\app_userdata\Aetheria\secrets.json
```

The file is not part of a game save or diagnostic bundle. Keep it private.

## Release integrity

Each GitHub Release publishes a SHA-256 checksum. Compare it with the downloaded archive before sharing or running a build from an untrusted mirror.
