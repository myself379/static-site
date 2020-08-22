---
title: "My First Post"
date: 2020-08-22T10:56:26+08:00
draft: true
---

Toyed around with coc.nvim language server. This one of the best language server plug ins created for vim/neo-vim. It is a joy to bring IDE-like suggestions.


```json
{
    "languageserver": {
        "intelephense":  {
            "enable": true,
            "command": "intelephense",
            "args": ["--stdio"],
            "filetypes": ["php"],
            "initializationOptions": {
                "storagePath": "/tmp/intelephense"
            }
        },
        "settings": {
            "intelephense": {
                "files": {
                    "maxSize": 1000000,
                    "associations": ["*.php", "*.phtml"]
                },
                "completion": {
                    "insertUseDeclaration": true,
                    "fullyQualifyGlobalConstantsAndFunctions": false,
                    "triggerParameterHints": true,
                    "maxItems": 15
                },
                "format": {
                    "enable": true
                }
            }
        }
    } 
}
```
