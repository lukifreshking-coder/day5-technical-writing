# Part A: User Manual Procedure

## Create a Python virtual environment and install a package on Windows

### Purpose

This procedure explains how a beginner can create an isolated Python environment, activate it in Windows PowerShell, and install the `requests` package. A virtual environment keeps a project's Python packages separate from other projects.

### Intended audience

First-semester computing students who can use Windows and open VS Code but have not created a Python virtual environment before.

### Prerequisites

Before starting, make sure you have:

- A computer running Windows 10 or Windows 11.
- Python 3 installed and available from PowerShell.
- Visual Studio Code installed.
- The Python extension installed in VS Code (recommended).
- A stable internet connection to download the package.
- Basic permission to create folders in your user directory.

### Procedure

**Step 1 — Open PowerShell in VS Code.**  
Action: Open VS Code, select **Terminal → New Terminal**, and choose PowerShell if prompted.  
Expected result: A PowerShell terminal appears at the bottom of VS Code.

**Step 2 — Check that Python is available.**  
Action: Run `py --version`.  
Expected result: PowerShell displays a Python version, such as `Python 3.13.x`.

**Step 3 — Create a project folder.**  
Action: Run `mkdir python-venv-practice`.  
Expected result: A folder named `python-venv-practice` is created in the terminal's current directory.

**Step 4 — Move into the project folder.**  
Action: Run `cd python-venv-practice`.  
Expected result: The PowerShell prompt shows that the current directory ends in `python-venv-practice`.

**Step 5 — Create the virtual environment.**  
Action: Run `py -m venv .venv`.  
Expected result: A `.venv` folder appears in the project directory and contains the environment files.

**Step 6 — Activate the virtual environment.**  
Action: Run `.\.venv\Scripts\Activate.ps1`.  
Expected result: The PowerShell prompt begins with `(.venv)`.

**Step 7 — Install the package.**  
Action: Run `python -m pip install requests`.  
Expected result: pip reports that `requests` and its dependencies were installed successfully, or that the package is already installed in this environment.

**Step 8 — Verify the package installation.**  
Action: Run `python -m pip show requests`.  
Expected result: The output displays package details, including its name, version, and installation location.

**Step 9 — Create a Python test file.**  
Action: In VS Code Explorer, create a file named `test_requests.py` in the project folder.  
Expected result: The new file appears in the Explorer panel.

**Step 10 — Add a simple import test.**  
Action: Enter `import requests` followed by `print(requests.__version__)` in `test_requests.py`, then save the file.  
Expected result: The file is saved with two lines of Python code.

**Step 11 — Run the test file.**  
Action: Run `python test_requests.py` in the terminal.  
Expected result: The terminal prints the installed `requests` version without an import error.

### Screenshot description

Include a screenshot of VS Code with the PowerShell terminal visible. The terminal should show the `(.venv)` prefix and the output from `python -m pip show requests`. The screenshot should make it clear that the package is installed in the virtual environment. Hide any personal information you do not want to share.

### Troubleshooting: PowerShell blocks activation

**Symptom:** PowerShell reports that running scripts is disabled when you try to activate the environment.

**Solution:** In the same PowerShell terminal, run:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

If prompted, confirm the change, then run:

```powershell
.\.venv\Scripts\Activate.ps1
```

**Why this helps:** The policy change applies only to the current PowerShell process and does not permanently change the machine-wide execution policy. If your school or organization manages this setting, follow its IT guidance instead.

**If `py` is not recognized:** Python may not be installed or its launcher may not be available. Install Python from the official Python website, enable the option to add Python to PATH if offered, reopen VS Code, and try `py --version` again.

### Completion checklist

- [ ] Python version displayed successfully.
- [ ] The `.venv` folder was created.
- [ ] The terminal prompt showed `(.venv)`.
- [ ] The `requests` package was installed and verified.
- [ ] The test file ran without an import error.
- [ ] The required screenshot was captured, if actual screenshots are required.
