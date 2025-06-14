```json
{
  // editor
  "editor.fontSize": 17,
  "editor.fontFamily": "Fira Code Fira Mono, Operator Mono, monospace",
  "editor.fontLigatures": true,
  "editor.wordWrap": "on",
  "editor.minimap.enabled": false,
  "editor.renderWhitespace": "all",
  "editor.tabSize": 2,
  "editor.insertSpaces": true,
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000,
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.guides.bracketPairs": true,
  "editor.tokenColorCustomizations": {
    "textMateRules": [
      {
        "scope": "comment",
        "settings": {
          "fontStyle": "italic"
        }
      }
    ]
  },
  
  // cursor

  "editor.cursorSmoothCaretAnimation": true,
  "editor.cursorBlinking": "expand",
  "[javascript]": {
    "editor.formatOnSave": false,
    "editor.defaultFormatter": null
  },
  "[javascriptreact]": {
    "editor.formatOnSave": false,
    "editor.defaultFormatter": null
  },
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.fixAll.tslint": true,
    "source.organizeImports": true
  },
  "eslint.alwaysShowStatus": true,

  //terminal
  "terminal.integrated.fontSize": 17,
  "terminal.integrated.fontWeight": "normal",
  "terminal.integrated.fontFamily": "Fira Code, Operator Mono, monospace",,
  "terminal.integrated.cursorStyle": "line",
  "terminal.integrated.cursorWidth": 2,
  "terminal.integrated.cursorBlinking": true,
  "workbench.colorTheme": "GitHub Dark Default",

  // terminal customization
  "workbench.colorCustomizations": {
    "terminal.background": "#000000",
    "terminal.foreground": "#ABB2BF",
    "terminalCursor.background": "#fff",
    "terminalCursor.foreground": "#FFFFFF",
    "terminal.ansiBlack": "#282C34",
    "terminal.ansiRed": "#E06C75",
    "terminal.ansiGreen": "#98C379",
    "terminal.ansiYellow": "#E5C07B",
    "terminal.ansiBlue": "#61AFEF",
    "terminal.ansiMagenta": "#C678DD",
    "terminal.ansiCyan": "#56B6C2",
    "terminal.ansiWhite": "#ABB2BF",
    "terminal.ansiBrightBlack": "#5C6370",
    "terminal.ansiBrightRed": "#E06C75",
    "terminal.ansiBrightGreen": "#98C379",
    "terminal.ansiBrightYellow": "#E5C07B",
    "terminal.ansiBrightBlue": "#61AFEF",
    "terminal.ansiBrightMagenta": "#C678DD",
    "terminal.ansiBrightCyan": "#56B6C2",
    "terminal.ansiBrightWhite": "#E6E6E6"
  },
  "terminal.integrated.defaultProfile.windows": "Git Bash"
}
```