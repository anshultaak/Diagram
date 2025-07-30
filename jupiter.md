Here’s a complete documentation-style summary of our conversation — from setting up Jupyter Notebook as a service on Ubuntu, addressing build errors, to disabling download/export options:

---

# 📘 Secure JupyterLab Setup on Ubuntu Server

### 🔧 1. Setup Jupyter Notebook as a Service

**Step 1: Create a virtual environment**

```bash
python3 -m venv /opt/jupyterenv
source /opt/jupyterenv/bin/activate
```

**Step 2: Install JupyterLab**

```bash
pip install jupyterlab
```

**Step 3: Generate config and set password**

```bash
jupyter lab --generate-config
jupyter lab password
```

**Step 4: Create a systemd service**
File: `/etc/systemd/system/jupyter.service`

```ini
[Unit]
Description=Jupyter Lab
After=network.target

[Service]
Type=simple
PIDFile=/run/jupyter.pid
ExecStart=/opt/jupyterenv/bin/jupyter lab --config=/home/ubuntu/.jupyter/jupyter_lab_config.py
User=ubuntu
Group=ubuntu
WorkingDirectory=/home/ubuntu
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

**Step 5: Enable and start the service**

```bash
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl enable jupyter
sudo systemctl start jupyter
```

---

### 🛠️ 2. Troubleshooting Build Issues

You encountered this error:

```
Please install nodejs >=20.0.0 before continuing.
```

**Solution: Upgrade Node.js**

```bash
sudo apt-get remove nodejs
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Then retry the build:

```bash
/opt/jupyterenv/bin/jupyter lab build --dev-build=False --minimize=False
```

---

### 🚫 3. Prevent Users from Downloading Data

#### ⚠️ Problem:

Users can still download/export notebooks using the **“File > Save and Export Notebook As”** menu.

#### ✅ Objective:

Disable all notebook export/download options via UI.

---

### 🔒 4. Disabling Export via Lab Extension

**Disable the notebook export option in UI:**

```bash
/opt/jupyterenv/bin/jupyter labextension disable @jupyterlab/notebook-extension:export
```

**Rebuild JupyterLab after disabling:**

```bash
/opt/jupyterenv/bin/jupyter lab build --dev-build=False --minimize=False
```

Make sure nodejs ≥ v20 is installed before doing this.

---

### 🔄 5. Restart the Jupyter Service

```bash
sudo systemctl restart jupyter
```

---

### 🧱 Optional: Harden the JupyterLab Instance

* Use **firewall rules** or **reverse proxy (e.g., NGINX)** to restrict access.
* Disable terminal and file browser if needed via:

  ```bash
  jupyter labextension disable @jupyterlab/terminal-extension
  jupyter labextension disable @jupyterlab/filebrowser-extension
  ```

You can list all extensions with:

```bash
jupyter labextension list
```

---

Let me know if you want this exported as a `.md` or `.txt` file — I can generate and share it.
