
# UV Setup for Python Project Management on Windows

This guide explains how to set up a Python project using `uv`, a versatile package and project manager, on Windows. It covers installation, managing virtual environments, adding dependencies, troubleshooting common issues, and running scripts.

## Prerequisites
- Windows operating system
- PowerShell (used as the terminal)

## Step 1: Install UV
1. **Install `uv` using the official installer:**
   ```powershell
   powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
   ```
2. **Verify the installation:**
   ```powershell
   uv --version
   ```
   This should display the installed version of `uv`.

## Step 2: Create a New Project
1. **Create a project directory and initialize it:**
   ```powershell
   mkdir my_project
   cd my_project
   uv init my_project
   ```
   This creates a `pyproject.toml` file in the project folder.

## Step 3: Manage the Virtual Environment
1. **Create a virtual environment:**
   ```powershell
   uv venv
   ```
   This command will create a `.venv` folder with a new virtual environment.

2. **Activate the virtual environment:**
   ```powershell
   .venv\Scripts\Activate
   ```

## Step 4: Add Dependencies
1. **Add a package (e.g., `requests`):**
   ```powershell
   uv add requests
   ```
   If you get an error like "No `pyproject.toml` found," make sure you are in the correct project directory where the `pyproject.toml` file exists.

### Troubleshooting Dependency Installation Issues
- If you encounter a DNS error or are unable to download packages, try these steps:
  1. **Check your internet connection** to ensure you are online.
  2. **Use a different DNS server** (like Google DNS):
     - Open Control Panel > Network and Sharing Center > Change adapter settings.
     - Right-click on your active network connection and select **Properties**.
     - Select **Internet Protocol Version 4 (TCP/IPv4)** and click **Properties**.
     - Set the DNS server to:
       - Preferred DNS server: `8.8.8.8`
       - Alternate DNS server: `8.8.4.4`
  3. **Configure proxy settings** if you are behind a proxy:
     ```powershell
     $env:HTTP_PROXY="http://your-proxy-server:port"
     $env:HTTPS_PROXY="https://your-proxy-server:port"
     ```
  4. **Manually download the package** and install from the local file:
     ```powershell
     uv add "C:\path\to\downloaded\requests-2.32.3-py3-none-any.whl"
     ```

## Step 5: Lock Dependencies
- Lock the project dependencies to ensure consistent installations:
  ```powershell
  uv lock
  ```

## Step 6: Create a Script
1. **Create a new folder for scripts and add a Python script:**
   ```powershell
   mkdir scripts
   cd scripts
   # You can use any text editor to create a new Python script file named `main.py`.
   # For example, using Notepad:
   notepad main.py
   ```
2. **Add the following code to `main.py`:**
   ```python
   import requests

   response = requests.get("https://api.github.com")
   print(response.json())
   ```

## Step 7: Run the Script
1. **Execute the script using `uv`:**
   ```powershell
   cd ..
   uv run .\scripts\main.py
   ```

## Step 8: Install and Use Command-Line Tools
1. **Install a CLI tool, such as `black` (a code formatter):**
   ```powershell
   uv tool install black
   ```
   If you see a warning about `C:\Users\<username>\.local\bin` not being on your `PATH`, update the `PATH` variable:
   ```powershell
   $env:PATH = "C:\Users\<username>\.local\bin;$env:PATH"
   ```

2. **Format a script using `black`:**
   ```powershell
   uvx black .\scripts\main.py
   ```

## Step 9: Linting and Formatting Python Files

1. **Format all Python files using `black`:**
   ```powershell
   uvx black . --check
   uvx black .
   uvx ruff check .

## Troubleshooting Common Issues
1. **Issue:** Command not found (`touch`, `vim`).
   - **Solution:** Use built-in Windows alternatives like `notepad` for text editing.

2. **Issue:** Cannot move or rename directories because they are in use.
   - **Solution:** Make sure all files in the directory are closed in any editor or program before attempting to rename.

## Summary of Commands
1. **Initialize a project:** `uv init my_project`
2. **Create a virtual environment:** `uv venv`
3. **Activate the virtual environment:** `.venv\Scripts\Activate`
4. **Add dependencies:** `uv add requests`
5. **Lock dependencies:** `uv lock`
6. **Create a script folder and add a Python script.**
7. **Run the script:** `uv run .\scripts\main.py`
8. **Install and run tools:** `uv tool install black`, `uvx black .\scripts\main.py`

By following this guide, you should be able to set up a Python project using `uv` on a Windows environment, manage dependencies, and work with virtual environments effectively.
