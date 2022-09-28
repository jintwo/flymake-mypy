# flymake-mypy

This module provides new-style (read: not [legacy "Proc"](https://www.gnu.org/software/emacs/manual/html_mono/flymake.html#The-legacy-Proc-backend)) Flymake support for Python static type checking using [mypy](http://mypy-lang.org/).

## Installation

### Manual

Clone this repository and add the following to your config

```emacs-lisp
(add-to-list 'load-path "/path/to/flymake-mypy")

(require 'flymake-mypy)
(add-hook 'python-mode-hook #'flymake-mypy-enable)
```

### Straight

```emacs-lisp
(use-package flymake-mypy
  :straight (flymake-mypy
             :type git
             :host github
             :repo "com4/flymake-mypy")
  :hook (python-mode . flymake-mypy-enable))
```

## Usage with Eglot
Eglot mode clobbers the flymake checkers. If you would like to stack this and the default style checker with your LSP's checker you can modify and use the following snippet

```emacs-lisp
(defun my/flymake-eglot-fix ()
    "Add flymake checkers after Eglot replaces the checkers."
    (when (derived-mode-p 'python-mode)
      ;; re-enable the default python.el checker
      (add-hook 'flymake-diagnostic-functions 'python-flymake nil t)
      (flymake-mypy-enable)))

(add-hook 'eglot-managed-mode-hook 'my/flymake-eglot-fix)
```
