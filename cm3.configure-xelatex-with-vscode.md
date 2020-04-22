# CM3. Configure xeLatex with vscode

## 1. Before configure

### 1-1. windows

#### 1-1-1. Copy your fonts files\(TTF\) to C:\Windows\Fonts

```text
cd  C:\Windows\Fonts
cp ~/Downloads/*.ttf C:\Windows\Fonts
```

Very! very! important, else XeLatex cannot recognize fonts.

Note:

**`Please do no use Windows font Manager`**

## 2. Paste following setting append "settings.json" in vscde

```text
 "latex-workshop.latex.tools": [
        {
            "name": "xelatex",
            "command": "xelatex",
            "args": [
                "%DOCFILE%"
            ]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "xelatex",
            "tools": [
                "xelatex"
            ]
        },
        {
            "name": "xe->bib->xe->xe",
            "tools": [
                "xelatex",
                "bibtex",
                "xelatex",
                "xelatex"
            ]
        }
    ]
```
