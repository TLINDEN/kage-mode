# kage-mode

An emacs mode for the kage shader language

![Screenshot](https://github.com/TLINDEN/kage-mode/blob/main/.github/assets/screenshot.png)

The mode provides all the features of [go-mode](https://github.com/dominikh/go-mode.el).

Please note, that you can't use
[lsp-mode](https://github.com/emacs-lsp/lsp-mode) with kage-mode
though, because the go-backend doesn't support it.

# Install

Copy the file `kage-mode.el` into some directory in your `load-path`.

A Melpa package will be available in the future.

# Configuration

This is my configuration for kage-mode:

```lisp
(use-package kage-mode
  :ensure nil         ;; installed locally in site-lisp
  :defer nil
  :mode "\\.kage\\'"    ;; you must use a different suffix for kage files!
  :commands kage-gofmt-before-save

  :init
  (defun tvd-kage-install-hooks()
    ;; remove the lsp-mode stuff, since unsupported
    (remove-hook 'before-save-hook #'lsp-format-buffer t)
    (remove-hook 'before-save-hook #'lsp-organize-imports t)
    
    ;; use gofmt -s
    (add-hook 'before-save-hook #'kage-gofmt-before-save t t))

  :config
  (add-hook 'kage-mode-hook #'tvd-kage-install-hooks)
  
  ;; ignore warnings about no kage lsp backend
  (setq lsp-warn-no-matched-clients nil))
```
# Meta

Copyright (C) 2024, T.v.Dein tlinden AT cpan.org

This file is NOT part of Emacs.

This  program is  free  software; you  can  redistribute it  and/or
modify it  under the  terms of  the GNU  General Public  License as
published by the Free Software  Foundation; either version 3 of the
License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but
WITHOUT  ANY  WARRANTY;  without   even  the  implied  warranty  of
MERCHANTABILITY or FITNESS  FOR A PARTICULAR PURPOSE.   See the GNU
General Public License for more details.

You should have  received a copy of the GNU  General Public License
along  with  this program;  if  not,  write  to the  Free  Software
Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307
USA
