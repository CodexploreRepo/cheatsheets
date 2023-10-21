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
  - Python: Python, Pylance, Jupyter, Flake8, Black, iSort
- Settings: UI & JSON

  - UI:
    - Tab Size: 2 (YAML = 2 spaces)
    - Rulers: Need to modify in JSON [80, 88]
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

## Code Refactor

- Change the function name: Right Click &#8594; **“Find All References”** &#8594; **"Rename Symbol"**
- **Peek**: can view the definition & modify the function
