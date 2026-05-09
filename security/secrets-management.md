# Secrets Management

## Purpose

Secrets management protects credentials, API keys, tokens, passwords, and private configuration used by the ALZO AI System.

## Secret Management Rules

- Do not commit secrets to the repository.
- Store local secrets in ignored `.env` files or approved secret stores.
- Use placeholder values in documentation.
- Rotate credentials when access changes or exposure is suspected.
- Separate development, staging, and production secrets.

## API Key Protection

API keys should be scoped, monitored, rotated, and disabled when no longer required.

## Local Security Rules

Local machines should use private environment files, locked accounts, updated tools, and non-production credentials.

## Backup Security

Secrets should not be included in plain-text backups unless the backup is encrypted and access-controlled.
