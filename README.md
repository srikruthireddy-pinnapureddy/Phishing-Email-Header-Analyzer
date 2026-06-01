# ThePhish — Phishing Email Header Analyzer

ThePhish is a lightweight Flask web app that helps analysts inspect forwarded phishing emails, extract observables (URLs, domains, IPs, attachments), and orchestrate analysis via TheHive and Cortex.

**Quick summary**
- Web UI served by Flask + Flask-SocketIO
- Integrates with TheHive (cases) and Cortex (analyzers)
- Fetches emails via IMAP (expects forwarded EML attachments)

**Repository layout (key folders)**
- `app/` — application source, configs and static assets
- `docker/` — optional Docker Compose templates for a full stack

## Requirements
- Python 3.11 (system or venv)
- pip
- Network access to your TheHive/Cortex/MISP instances (if used)

Windows note: `requirements.txt` has been adjusted for Windows compatibility (prebuilt wheels): `greenlet`, `eventlet`, `dnspython`, and `python-magic-bin` are used to avoid native build issues.

## Quick start (local)
1. From repository root, create and activate a virtual environment (recommended):

```bash
python -m venv .venv
```

On PowerShell use:

```powershell
.\.venv\Scripts\Activate.ps1
```

2. Install dependencies:

```bash
python -m pip install -r app/requirements.txt
```

3. Edit `app/configuration.json` with IMAP and TheHive/Cortex/MISP connection details.
4. Start the application:

```bash
python app/thephish_app.py
```

The UI will be available at: http://127.0.0.1:8080

## Docker (optional)
The `docker/` folder contains a Compose template for spinning up TheHive/Cortex and thephish together for testing. See `docker/README.md` and adapt the files before use.

## Configuration
- `app/configuration.json` — IMAP, TheHive, Cortex, MISP and case defaults
- `app/analyzers_level_conf.json` — mapping to tune analyzer levels
- `app/whitelist.json` — whitelist rules applied during analysis

Important: Do not commit real credentials. Replace secrets with environment variables or a secrets manager for production.

## Running tests / smoke checks
- After start, the homepage `/` should return HTTP 200.
- The `/list` endpoint returns the list of unread emails (requires IMAP configured).

## Security & privacy
- Remove or redact credentials from `app/configuration.json` before committing.
- The app interacts with third-party services — ensure API keys and access are restricted appropriately.

## Contributing
- Fixes and improvements are welcome. Please follow standard GitHub workflows: fork, branch, PR.

## License
This project is published under the existing LICENSE file in the repository.
