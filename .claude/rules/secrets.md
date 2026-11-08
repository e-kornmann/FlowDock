# Secrets

Never read, print, grep, copy or parse `.env` or any `*.local` file. That applies to the file tools, the shell and scripts alike. Once FlowDock has credentials (database passwords, API keys), they live there. `.claude/settings.json` denies the file tools; this rule covers everything else.

What such a file should contain belongs in a committed `.env.example` with placeholder values. Read that instead. When a script needs a value, run the script; it reads the file itself.

Never commit secrets. `.env` and `*.local` are git-ignored. Check `git status` before committing a new config file.
