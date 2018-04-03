# General configuration
```
set nocompatible

```

# Tab widths
```
:set tabstop=4      ; Make tab appear 4 characters wide
:set shiftwidth=4   ; Size of indents
:set expandtab      ; Expand TABs to spaces
```
For the modline: `vim :set ts=4 sw=4 sts=4 et :`

# Grepping multiple files
```{vim}

```

# Tags
```{vim}
# Install on OSX: brew install ctags
:! ctags -R
```


# Makefiles
```
:make    ; run make
:copen   ; open a mini window with a list of error
         ; hit Enter to jump to error
C-]      ; follow tag under cursor
```
