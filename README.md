# claude-fpe
A CLI wrapper for Claude Code that encrypts secrets before they leave your machine through proxy-middleware.
# The problem

Claude Code reads your files, including .env files, config files, and anything else in your project. Every token it reads gets sent to Anthropic's servers as part of your session context. That includes database passwords, API keys, and internal hostnames you probably didn't think about. Or most times, like myself as an example, people often give Claude sensitive information such as API keys and we tell Claude to put these keys in
How it works
When you run `claude-fpe` A local proxy starts on your machine, and Claude Code is launched pointing at it. Every request is intercepted before it reaches Anthropic, and sensitive values are transformed using format-preserving encryption... meaning your credentials are replaced with fake values that look structurally identical, so Claude Code can still reason about your code. The real values never leave your machine, but the shape, semantic meaning, and structure of these values will still allow Claude to infer what is going on.

When the session ends, the encryption key is discarded. Reconstruction after that point is impossible by design.
MIT
