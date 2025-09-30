<div align="center">
  <img src="bomiot/templates/dist/spa/icons/logo.png" alt="Bomiot logo" width="200" height="auto" />
  <h1>🚀 Bomiot</h1>
  <p><strong>One App you can do everything</strong></p>
  <p><em>Powerful Distributed Document Management Framework & Full-Stack Development Platform</em></p>

<!-- Badges -->
![License: APLv2](https://img.shields.io/github/license/Bomiot/Bomiot)
![Release Version (latest Version)](https://img.shields.io/github/v/release/Bomiot/Bomiot?color=orange&include_prereleases)
![i18n Support](https://img.shields.io/badge/i18n-Support-orange.svg)

![repo size](https://img.shields.io/github/repo-size/Bomiot/Bomiot)
![GitHub commit activity](https://img.shields.io/github/commit-activity/m/Bomiot/Bomiot)
![Contributors](https://img.shields.io/github/contributors/Bomiot/Bomiot?color=blue)

![GitHub Org's stars](https://img.shields.io/github/stars/Bomiot?style=social)
![GitHub Follows](https://img.shields.io/github/followers/Singosgu?style=social)
![GitHub Forks](https://img.shields.io/github/forks/Bomiot/Bomiot?style=social)
![GitHub Watch](https://img.shields.io/github/watchers/Bomiot/Bomiot?style=social)

![Python](https://img.shields.io/badge/Python-3.9+-yellowgreen)
![Django](https://img.shields.io/badge/Django-4.2+-yellowgreen)
![Quasar Cli](https://img.shields.io/badge/Quasar/cli-2.4.1+-yellowgreen)
![Vue](https://img.shields.io/badge/Vue-3.4.18+-yellowgreen)
![NodeJS](https://img.shields.io/badge/NodeJS-18.19.1+-yellowgreen)

[![YouTube](https://img.shields.io/youtube/channel/subscribers/UCPW1wciGMIEh7CYOdLnsloA?color=red&label=YouTube&logo=youtube&style=for-the-badge)](https://www.youtube.com/channel/UCPW1wciGMIEh7CYOdLnsloA)

[English](README.md) | [中文](README_CN.md)

</div>

---

## 🧭 Run this repository locally (macOS, Windows, Linux)

This section gives you a copy-paste runbook to get both the backend (Django/ASGI) and the frontend (Quasar/Vue) running immediately. It includes OS-specific commands and the expected outcome after each step.

Recommended versions:
- Python: 3.12.x (supported range is 3.9 – 3.13.0; Python 3.13.1+ can cause pin conflicts)
- Node: 18, 20, or 22 (Node 20 recommended)
- Package manager: Yarn (via Corepack) or npm

Before you start: open two terminals so you can run backend and frontend side by side.

### 1) Clone and enter the repo

```bash
git clone https://github.com/MarcosMasip/Bomiot-self-contained.git
cd Bomiot-self-contained
```

Expected outcome:
- Repository is cloned and you are in the project root.

### 2) Install Python 3.12 (if needed)

- macOS (Homebrew):

```bash
brew install python@3.12
python3.12 --version
```

- Linux (example for Debian/Ubuntu; adjust if needed):

```bash
sudo apt-get update
sudo apt-get install -y python3.12 python3.12-venv
python3.12 --version
```

- Windows (Microsoft Store or Python.org):
  - Install Python 3.12 from https://www.python.org/downloads/windows/
  - After install: `py -3.12 --version`

Expected outcome:
- The version command shows Python 3.12.x.

### 3) Create and activate a virtual environment

- macOS/Linux:

```bash
/opt/homebrew/bin/python3.12 -m venv .venv  # macOS Homebrew path; on Linux use: python3.12 -m venv .venv
source .venv/bin/activate
python --version
```

- Windows PowerShell:

```powershell
py -3.12 -m venv .venv
./.venv/Scripts/Activate.ps1
python --version
```

- Windows cmd.exe:

```bat
py -3.12 -m venv .venv
.\.venv\Scripts\activate.bat
python --version
```

Expected outcome:
- A `.venv/` folder is created.
- Your prompt shows the virtual environment active.
- `python --version` prints 3.12.x.

### 4) Upgrade pip tooling

```bash
pip install --upgrade pip wheel
```

Expected outcome:
- pip and wheel upgrade without errors.

### 5) Install backend dependencies (locked)

```bash
pip install -r requirements.txt
```

Expected outcome:
- Installs Django, uvicorn, and other pinned packages successfully with no conflicts.

### 6) Install this package as an editable CLI (no deps re-resolve)

```bash
pip install -e . --no-deps
bomiot -v
```

Expected outcome:
- Editable install succeeds; `bomiot` command becomes available.
- `bomiot -v` prints the bomiot version.

### 7) Initialize the workspace

```bash
bomiot init
```

Expected outcome:
- Creates `logs/` and `deploy/` directories (if missing).
- Generates an auth key (auth_key.py) if missing.
- Prints an ASCII banner.

### 8) Scaffold a new project (choose a name)

```bash
bomiot project my-project
```

Expected outcome:
- Creates `my-project/` with backend `media/`, `language/`, and frontend `templates/`.
- Writes/updates `setup.ini` with `[project] name = my-project`.
- Outputs: `Initialized project workspace my-project`.

Note: The root `.gitignore` already ignores `/my-project/` to keep your repo clean.

### 9) Apply database migrations

```bash
bomiot migrate
```

Expected outcome:
- Django applies migrations.
- SQLite DB created at `dbs/db.sqlite3`.
- Ends with lines like “Applying … OK”.

### 10) Create an admin user

```bash
bomiot initadmin
```

Expected outcome:
- If absent: creates admin/admin and prints credentials.
- If present: prints that admin already exists.

### 11) Start the backend server (keep it running)

```bash
bomiot run --host 127.0.0.1 --port 8000
```

Expected outcome:
- Uvicorn starts on http://127.0.0.1:8000
- Logs show “Application startup complete”.
- Useful endpoints (GET):
  - http://127.0.0.1:8000/test/
  - http://127.0.0.1:8000/fastapi/test/
  - http://127.0.0.1:8000/flask/test/
- Django admin: http://127.0.0.1:8000/admin/ (login admin/admin).

Leave this terminal running.

### 12) Open a second terminal for the frontend

Ensure Node and Yarn are available:

- macOS/Linux:

```bash
node -v || echo "Please install Node (https://nodejs.org)"
corepack enable
corepack prepare yarn@stable --activate
yarn -v
```

- Windows PowerShell:

```powershell
node -v
corepack enable
corepack prepare yarn@stable --activate
yarn -v
```

Expected outcome:
- Node prints v18/20/22+; Yarn prints a version (Corepack-managed is recommended).

### 13) Install frontend dependencies

```bash
cd my-project/templates
yarn install
```

Expected outcome:
- Installs node_modules.
- Quasar performs its prepare step.

### 14) Point axios to the backend (baseURL)

Option A — quick manual edit:
- Open `my-project/templates/src/boot/axios.js` and change:
  - Ensure the const exists: `const baseURL = 'http://127.0.0.1:8000'`
  - In the axios.create call, uncomment baseURL:
    - Change `// baseURL: baseURL` to `baseURL: baseURL`

Option B — command line (macOS/Linux):

```bash
sed -i '' 's#// baseURL: baseURL#baseURL: baseURL#' src/boot/axios.js  # macOS (BSD sed)
# Linux (GNU sed): sed -i 's#// baseURL: baseURL#baseURL: baseURL#' src/boot/axios.js
```

Option C — Windows PowerShell:

```powershell
(Get-Content src/boot/axios.js) -replace '// baseURL: baseURL','baseURL: baseURL' | Set-Content src/boot/axios.js
```

Expected outcome:
- Axios will call the backend at http://127.0.0.1:8000.

### 15) Run the frontend dev server

```bash
yarn dev
```

Expected outcome:
- Quasar dev server starts and opens your browser automatically (often http://localhost:9000).
- The UI loads; network calls go to http://127.0.0.1:8000 and should succeed.

### ✅ Verify
- Visit http://127.0.0.1:8000/test/ in your browser — you should see a simple JSON response.
- Visit http://127.0.0.1:8000/admin/ and log in with admin/admin.
- Use the frontend and confirm it can fetch data.

### 🛑 Shutdown / Closing procedures
- Frontend: press Ctrl+C in the terminal running `yarn dev`.
- Backend: press Ctrl+C in the terminal running `bomiot run` (wait for graceful shutdown log lines).
- Deactivate the virtual environment (optional):

```bash
deactivate
```

### 🧰 Troubleshooting
- Python 3.13.1 error when installing: This repo pins dependencies to `<=3.13.0`. Use Python 3.12.x to avoid conflicts.
- macOS “command not found: python3.12”: Install via Homebrew (`brew install python@3.12`) or use the system’s python3 if it’s 3.12.x.
- Windows execution policy prevents venv activation: In PowerShell (admin), run `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` once, then activate again.
- Quasar dev fails to open the browser: Copy the printed local URL (e.g., http://localhost:9000) and paste it into your browser manually.
- API calls failing from the frontend:
  - Ensure backend is running on 127.0.0.1:8000.
  - Ensure `src/boot/axios.js` has `baseURL: baseURL` uncommented.
  - Check the browser console/network tab for details.


## 📋 Table of Contents

- [🌟 Project Introduction](#-project-introduction)
- [✨ Core Features](#-core-features)
- [🚀 Quick Start](#-quick-start)
- [📦 Installation Guide](#-installation-guide)
- [🛠️ Command Line Tools](#️-command-line-tools)
- [🏗️ Project Structure](#️-project-structure)
- [🔧 Configuration](#-configuration)
- [🌐 Deployment Guide](#-deployment-guide)
- [📚 Scheduled Tasks](#-scheduled-tasks)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)
- [🔗 Related Links](#-related-links)

---

## 🌟 Project Introduction

Bomiot is a revolutionary distributed document management framework and full-stack development platform, with core components written in Rust, designed to solve modern development pain points. We believe that excellent open-source projects should not only have powerful technology stacks but also focus on developer experience and team collaboration efficiency, making it simple and easy to learn.

### 🎯 Design Philosophy

- **Learning Curve**: Backend supports Django, FastAPI, Flask; Frontend supports React, Angular, Vue, Django built-in Templates (official provides a Vue set)
- **Developer Friendly**: Seamless experience from 0 to 1, no complex configuration required
- **Team Collaboration**: Efficient development team interaction mechanisms
- **Modular Design**: Plugin-based architecture with extensible functionality
- **Easy Deployment**: pip installation, convenient for team deployment, supports Python 3.9+
- **Signal Mechanism**: Data management through signal mechanism, more convenient custom API support
- **Enterprise Ready**: Production-ready, supports large-scale deployment

---

## ✨ Core Features

### 🔧 Development Tools
- ✅ **Project Scaffolding**: One-click project and application creation
- ✅ **Plugin System**: Rich plugin ecosystem
- ✅ **Real-time File Monitoring**: Enhanced development efficiency

### 🕐 Task Management
- ✅ **Scheduled Tasks**: Powerful scheduling system
- ✅ **Task Monitoring**: Real-time task status tracking
- ✅ **Error Handling**: Intelligent exception handling mechanism
- ✅ **Log Management**: Complete logging system

### 🔐 Access Control
- ✅ **Fine-grained Permissions**: Role-based access control
- ✅ **JWT Authentication**: Secure identity authentication
- ✅ **API Permissions**: Interface-level permission management
- ✅ **Operation Audit**: Complete operation logs

### 🌍 Internationalization
- ✅ **Multi-language Support**: Built-in internationalization framework
- ✅ **Dynamic Language Switching**: Runtime language switching
- ✅ **Localization Configuration**: Regional settings

### 📊 System Monitoring
- ✅ **Performance Monitoring**: CPU, memory, disk monitoring
- ✅ **Process Management**: Real-time system process monitoring
- ✅ **Network Monitoring**: Network traffic statistics
- ✅ **Health Checks**: System health status detection

### 📚 Application Market
- ✅ **Application Sharing**: Application market pip installation, convenient and fast
- ✅ **Component Market**: Hot-pluggable components, dynamic import

---

## 🚀 Quick Start

### 1. Install Bomiot

```bash
# Install using pip
pip install bomiot

# Or install using poetry
poetry add bomiot
```

### 2. Initialize Workspace

```bash
# Initialize Bomiot workspace
bomiot init
```

### 3. Create Project

```bash
# Create new project
bomiot project my-project

# Create new application
bomiot new my-app
```

### 4. Database

```bash
# Initialize database
bomiot migrate

# If you created a new application, you can generate new database migration files
bomiot makemigrations
```

### 5. Create Administrator

```bash
# Initialize administrator
bomiot initadmin

# Reset administrator account password
bomiot initpwd
```

### 6. Start Service

```bash
# Start development server
bomiot run

# Or specify port
bomiot run --host 0.0.0.0 --port 8080
```

---

## 📦 Installation Guide

### System Requirements

- **Python**: 3.9 or higher
- **Node.js**: 18.19.1 or higher
- **Operating System**: Windows, macOS, Linux

### Modify Frontend

#### 1. Install Frontend Dependencies

```bash
# Enter frontend directory
cd my-project/templates

# Install dependencies
yarn install
```

#### 2. Open Development baseUrl

```bash
# Change axios.js
vim my-project/templates/src/boot/axios.js

```

```bash
# axios.js code snippet modification
 ...
const baseURL = 'http://127.0.0.1:8000' // Replace with your actual API URL

const api = axios.create({
  baseURL: baseURL ##Open this
})
 ...
```


#### 3. Frontend Development Debugging

```bash
# Ensure backend is already started
bomiot run
```

```bash
# Restart frontend
cd my-project/templates

&

quasar dev
```

---

## 🛠️ Command Line Tools

Bomiot provides powerful command line tools to make development and management simple and efficient.

### 📋 Command Overview

```bash
bomiot [command] [options]
```

### 🔧 Core Commands

#### Project Management

```bash
# Help command
bomiot -h

# View version number
bomiot -v

# Initialize workspace
bomiot init

# Create new project
bomiot project <project_name>

# Create new application
bomiot new <app_name>

# Create plugin
bomiot plugins <plugin_name>
```

#### Application Market

```bash
# Application market
bomiot market <project_name>

# Plugin installation, plugins are automatically hot-imported
pip install -y <plugin_name>

or

poetry add <plugin_name>
```

#### Database Management

```bash
# Create database migration
bomiot makemigrations

# Execute database migration
bomiot migrate

# Load initial data
bomiot loaddata <source>

# Export data
bomiot dumpdata [appname]
```

#### User Management

```bash
# Create administrator account
bomiot initadmin

# Reset administrator password
bomiot initpwd
```

#### Service Management

```bash
# Start server
bomiot run [options]

# Deploy project
bomiot deploy <project_name>
```

#### System Validation

```bash
# Initialize validation Keys
bomiot keys
```

### 🚀 Server Startup Options

```bash
bomiot run [options]

Options:
  --host, -b HOST                Server host address (default: 127.0.0.1)
  --port, -p PORT                Server port (default: 8000)
  --workers -w WORKERS           Number of worker processes (default: 1)
  --log-level LEVEL              Log level (critical/error/warning/info/debug/trace)
  --ssl-keyfile FILE             SSL key file
  --ssl-certfile FILE            SSL certificate file
  --proxy-headers                Enable proxy headers
  --http HTTP                    HTTP implementation (auto/h11/httptools)
  --loop LOOP                    Async loop (auto/asyncio/uvloop)
  --limit-concurrency            Maximum concurrent requests (default: 1000)
  --backlog                      Maximum waiting connections (default: 128)
  --timeout-keep-alive           HTTP keep-alive timeout (default: 5)
  --timeout-graceful-shutdown    Graceful shutdown timeout (default: 30)
```

### 📝 Usage Examples

```bash
# Basic startup
bomiot run

# Test api，method("GET")
"name": "django", "url": "http://127.0.0.1:8000/test/"
"name": "fastapi", "url": "http://127.0.0.1:8000/fastapi/test/"
"name": "flask", "url": "http://127.0.0.1:8000/flask/test/"

# Specify port and host
bomiot run --host 0.0.0.0 --port 8080

# Production environment configuration
bomiot run --host 0.0.0.0 --port 80 --workers 4 --log-level info

# SSL configuration
bomiot run --ssl-keyfile key.pem --ssl-certfile cert.pem
```

---

## 🏗️ Project Structure

```
my-project/                    # Project directory
├── fastapi_app/               # fastapi app
│   └── main.py                # Main file
├── flask_app/                 # flask app
│   └── main.py                # Main file
├── language/                  # Backend language files
│   ├── en-US.toml             # English translation file       
│   └── zh-CN.toml             # Chinese translation file
├── media/                     # Static files
│   ├── img/                   # Public images       
│   └── ***.md                 # Various md documents
├── static/                    # Static files
├── __version__.py             # my-project version
├── bomiotconf.ini             # Bomiot project identifier file
├── files.py                   # File signals
├── receiver.py                # Data API signals
├── server.py                  # Server signals
└── README.md                  # ReadME documentation
dbs/                           # Database files
logs/                          # System logs
setup.ini                      # Project configuration file
...
```

---

## 🔧 Configuration

### Environment Configuration

Bomiot uses configuration files to manage different environment settings:

```ini
# setup.ini
[project]
name = my-project

[database](requires keys validation)
# Supports multiple databases (sqlite, mysql, oracle, postgresql)
engine = sqlite
name = db_name
user = db_user
password = db_pwd
host = db_host
port = db_port

[local]
time_zone = UTC

[jwt]
user_jwt_time = 1000000

[throttle]
allocation_seconds = 1
throttle_seconds = 10

[request]
limit = 2

[file](requires keys validation)
file_size = 102400000
file_extension = py,png,jpg,jpeg,gif,bmp,webp,txt,md,html,htm,js,css,json,xml,csv,xlsx,xls,ppt,pptx,doc,docx,pdf
```

### Database Configuration

Supports multiple databases:

- **SQLite** (default)
- **MySQL** (requires keys validation)
- **PostgreSQL** (requires keys validation)
- **Oracle** (requires keys validation)

---

## 🌐 Deployment Guide

### Supervisor

```bash
# Generate deployment files
bomiot deploy my-project

# Point supervisord.conf to this file to complete daemon process deployment

```

## Scheduled Tasks

### Supported Scheduled Tasks

```python
ARGS_MAP = {
    'cron': ['year', 'month', 'day', 'week', 'day_of_week', 'hour', 'minute', 'second', 'start_date', 'end_date','timezone'],
    'interval': ['weeks', 'days', 'hours', 'minutes', 'seconds', 'start_date', 'end_date', 'timezone'],
    'date': ['run_date', 'timezone']
}
```

### Writing Scheduled Tasks

```python
from bomiot.server.core.signal import bomiot_signals

def my_scheduled_task(sender, **kwargs):
    print("Execute scheduled task")
    
# Send signal to bomiot anywhere, usually written in urls.py, refresh web page to take effect
bomiot_signals.send(sender=my_scheduled_task, msg={
    'models': 'JobList',
    'data': {
        'trigger': 'interval',
        'seconds': 60,
        'end_date': '2099-05-30',
        'description': 'Execute every 60 seconds, end on May 30, 2099'
    }
})
```

---

## 🤝 Contributing

We welcome all forms of contributions!

### Ways to Contribute

1. **Report Bugs**: [Create Issue](https://github.com/Bomiot/Bomiot/issues/new?template=bug_report.md)
2. **Feature Requests**: [Submit Feature Request](https://github.com/Bomiot/Bomiot/issues/new?template=feature_request.md)
3. **Code Contributions**: Fork the project and submit Pull Request
4. **Documentation Improvements**: Help improve documentation
5. **Community Support**: Answer other users' questions

### Ways to Contribute Code

```bash
# 1. Fork the project
# 2. Clone your Fork
git clone https://github.com/your-username/Bomiot.git

# 3. Create feature branch
git checkout -b feature/amazing-feature

# 4. Commit changes
git commit -m 'Add amazing feature'

# 5. Push to branch
git push origin feature/amazing-feature

# 6. Create Pull Request
```

### Code Standards

- Follow PEP 8 Python code standards
- Add appropriate comments and docstrings
- Write unit tests
- Ensure all tests pass

---

## 📄 License

This project is licensed under the [APLv2](LICENSE) License - see the [LICENSE](LICENSE) file for details.

---

## 🔗 Related Links

### 📺 Video Tutorials
- [YouTube Channel](https://www.youtube.com/channel/UCPW1wciGMIEh7CYOdLnsloA)

### 🐛 Issue Reporting
- [Report Bug](https://github.com/Bomiot/Bomiot/issues/new?template=bug_report.md)
- [Feature Request](https://github.com/Bomiot/Bomiot/issues/new?template=feature_request.md)

### 💬 Community
- [GitHub Discussions](https://github.com/Bomiot/Bomiot/discussions)
- [Issues](https://github.com/Bomiot/Bomiot/issues)

---

<div align="center">

**⭐ If this project helps you, please give us a Star!**

Made with ❤️ by [Bomiot Team](https://github.com/Bomiot)

</div>