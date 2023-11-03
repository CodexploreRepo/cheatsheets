# VSCode

## Shortcut

- Command Palette: `CMD + SHIFT + P`
- Select Multiple Lines: `Option + CMD + Down Key` &#8594; ESC to exit the multiple lines

## Setup

- Code path:  Open the Command Palette (Cmd+Shift+P) and type 'shell command' to find the **Shell Command: Install 'code' command in PATH command**.
- Extensions:
  - Theme: search **"GitHub Theme"**
    - Change theme: Command Palette &#8594; type "Theme"
  - Icon Them: **"Material icon theme"**
  - Python: Python, Pylance (upports type hinting features that can be helpful for working with Pydantic models and FastAPI), Jupyter, Flake8, Black, iSort
  - Install Vscode using `.vsix` file, a package format used for Visual Studio Code (VS Code) extensions.
    - You can download the `.vsix` file from the VS Code Extension Official Website &#8594; Go to VS Code &#8594; Extension Tab &#8594; Choose "Install from VSIX" and browse to the downloaded `.vsix` file
- Settings: UI & JSON

  - UI:

    - Tab Size: 2 (YAML = 2 spaces)
    - Rulers: Need to modify in JSON [80, 88]
    - Search for **"python type checking mode"** and set it to `basic` for basic type checking. `Pylance` will now show diagnostics and warnings to catch simple type-related errors. Alternatively, you can set it to `strict` to enforce more advanced type checking rules.
    - Search for **"Python inlay type hints"**, and enable inlay hints for **Variable Types** and **Function Return Types**:

  - JSON: `CMD + SHIFT + P` &#8594; "Open User Settings" &#8594; [settings.json](../docs/assests/settings.json)

```json
{
  // Default Code Formatter: Prettier
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  // Python Code Formatter Settings
  "[python]": {
    "editor.defaultFormatter": "ms-python.black-formatter",
    "editor.codeActionsOnSave": {
      "source.organizeImports": true // isort
    }
  },
  "black-formatter.args": ["--line-length=80"], // black
  "isort.args": ["--profile", "black"] // isort
}
```

## Create Virtual Venv

- Create `requirements.txt`
- Create a virtual environment by opening the Command Palette (⇧⌘P) and running the Python: Create Environment command.
- When asked for the environment type, select Venv
- Then select the latest version of Python available on your machine:

## Debuger

- Reference:
  - [Configure and run the debugger](https://code.visualstudio.com/docs/python/python-tutorial#_configure-and-run-the-debugger)

### Start Debugger

- Run the code by starting up the debugger (F5).
  - For Fast API: From the dropdown menu, select the FastAPI configuration option from the list

### Breakpoint

- Add a breakpoint
- Run the code &#8594; the code will stop at the breakpoint
- Select the statement that you want to check the output &#8594; right-click on the editor and select **Evaluate in Debug Console** &#8594; the output of the selected statement will be printed in **Debug Console**

## Code Refactor

- Change the function name: Right Click &#8594; **“Find All References”** &#8594; **"Rename Symbol"**
- **Peek**: can view the definition & modify the function

## Debug

## Error

### VS Code Extension

- Error while installing VS Code extension: `"[error] end of central directory record signature not found,end of central directory record signature not found: Error: end of central directory record signature not found,end of central directory record signature not found"`
  - Root Cause: there might be an error, some part of the installation file while downloading the extension and store in cache extension folders
  - Solution: by deleting the following cache extension/data folders from this link https://github.com/PowerShell/vscode-powershell/issues/4474
    - `C:\Users\UserName\AppData\Roaming\Code\CachedExtensionVSIXs`
    - `C:\Users\UserName\AppData\Roaming\Code\CachedData`
