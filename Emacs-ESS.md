Installation
```
# MacOS
brew install emacs --with-cocoa
brew install brewsci/science/ess
```

Configuration
```
## ~/.emacs
;; Loading ESS
(require 'ess-site)
(ess-toggle-underscore nil)

(show-paren-mode 1)
(setq show-paren-delay 0)

  (fset 'my-complete-file-name
        (make-hippie-expand-function '(try-complete-file-name-partially
                                       try-complete-file-name)))
  (global-set-key "\M-/" 'my-complete-file-name)
```

Basic commands. Syntax: `~ab~` means `C-a C-b`
```
~xf~    Open file
~xs~    Save file
~x~o    Switch to other window
~x~b    Switch buffer
~x~0    Close current window

M-/     Text completion

~b/e~   Beginning/End of line
~s/r~   Forward/backward search
~w~     Cut text
~y~     Paste text

~ce~    Evaluate line/region
~cn~    Evaluate line
~cb~    Evaluate buffer
```
