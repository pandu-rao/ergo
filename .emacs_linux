;;; package --- Summary

;;; Commentary:

;;; Code:

(custom-set-variables
 ;; custom-set-variables was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 '(column-number-mode t)
 '(show-paren-mode t)
 '(tabbar-separator (quote (0.5))))

(custom-set-faces
 ;; custom-set-faces was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 '(highlight-indentation-face ((t (:inherit fringe :background "white"))))
 '(ledger-font-posting-date-face ((t (:foreground "dark violet")))))

;; disable startup messages
(setq initial-scratch-message nil)
(setq inhibit-startup-message t)
(fset 'yes-or-no-p 'y-or-n-p)

(setq visible-bell t)
(bar-cursor-mode t)
(setq line-number-mode t)
(delete-selection-mode t)
(tool-bar-mode -1)
; highlight matching parenthesis (useful when coding)
(require 'paren)

(require 'recentf)
(recentf-mode 1)
(setq recentf-max-menu-items 25)
(global-set-key "\C-x\ \C-r" 'recentf-open-files)

;; custom key binding functions
(defun up-one () (interactive) (scroll-up 1))
(defun down-one () (interactive) (scroll-down 1))

;; custom key bindings
(global-unset-key "\C-z")

(global-unset-key "\C-c\C-r")
(global-set-key "\C-c\C-d"         'delete-horizontal-space)

(global-set-key "\C-h"             'delete-backward-char)
(global-set-key "\M-h"             'backward-kill-word)

(global-set-key "\M-s"             'occur)
(global-set-key "\M-o"             'other-window)

(global-set-key [(shift control l)]    'this-line-to-top-of-window)
(global-set-key [(shift control n)]    'up-one)
(global-set-key [(shift control p)]    'down-one)

;; {{ ergo keypad mapping provides navigation/cut-paste
(global-set-key [(kp-7)]               'beginning-of-line)
(global-set-key [(shift kp-7)]         'beginning-of-line-mark)
(global-set-key [(control kp-home)]    'beginning-of-buffer)
(global-set-key [(shift control kp-7)] 'beginning-of-buffer-mark)

(global-set-key [(kp-8)]               'previous-line)
(global-set-key [(shift kp-8)]         'previous-line-mark)

(global-set-key [(kp-9)]               'scroll-down)
(global-set-key [(shift kp-9)]         'scroll-down-mark)

(global-set-key [(kp-4)]               'backward-char)
(global-set-key [(shift kp-4)]         'backward-char-mark)
(global-set-key [(control kp-left)]    'backward-word)
(global-set-key [(shift control kp-4)] 'backward-word-mark)

(global-set-key [(kp-6)]               'forward-char)
(global-set-key [(shift kp-6)]         'forward-char-mark)
(global-set-key [(control kp-right)]   'forward-word)
(global-set-key [(shift control kp-6)] 'forward-word-mark)

(global-set-key [(kp-1)]               'end-of-line)
(global-set-key [(shift kp-1)]         'end-of-line-mark)
(global-set-key [(control kp-end)]     'end-of-buffer)
(global-set-key [(shift control kp-1)] 'end-of-buffer-mark)

(global-set-key [(kp-2)]               'next-line)
(global-set-key [(shift kp-2)]         'next-line-mark)

(global-set-key [(kp-3)]               'scroll-up)
(global-set-key [(shift kp-3)]         'scroll-up-mark)

(global-set-key [(kp-0)]               'overwrite-mode)
(global-set-key [(shift kp-0)]         'yank)
(global-set-key [(control kp-insert)]  'copy-region-as-kill)

(global-set-key [(kp-decimal)]         'forward-delete-char)
(global-set-key [(shift kp-decimal)]   'kill-region)

(global-set-key [(control kp-divide)]  'undo)

(global-set-key [delete]               'delete-char)
(global-set-key [kp-delete]            'delete-char)
;; }} ergo keypad mapping provides navigation/cut-paste

(setq frame-title-format "%b : %f")

(set-face-foreground 'mode-line              "White")
(set-face-background 'mode-line              "#808080")
(set-face-foreground 'font-lock-string-face  "#2F67FF")
(set-face-foreground 'font-lock-warning-face "Red")
(set-face-background 'region                 "DarkBlue")
(set-face-foreground 'region                 "White")

(add-hook 'before-save-hook 'whitespace-cleanup)

(defun python-insert-breakpoint ()
  "Insert the text 'import pdb; pdb.set_trace()'"
  (interactive)
  (insert "import pdb; pdb.set_trace()")
  (newline)
  )

(global-set-key [f9] 'python-insert-breakpoint)

(defun python-remove-breakpoint ()
  "Remove the text 'import pdb; pdb.set_trace()'"
  (interactive)
  (let ((x (line-number-at-pos))
        (cur (point)))
    (search-forward-regexp "^[ ]*import pdb; pdb.set_trace()")
    (if (= x (line-number-at-pos))
        (let ()
          (move-beginning-of-line 1)
          (kill-line 1)
          (move-beginning-of-line 1))
      (goto-char cur))))

(global-set-key [(shift f9)] 'python-remove-breakpoint)

; Insert the date, the time, and the date and time at point. Insert
; the date 31 days hence at point (eventually...). Useful for keeping
; records. These are based on Glickstein.

(defvar insert-time-format "%T"
  "*Format for \\[insert-time] (c.f. 'format-time-string' for how to format).")

(defvar insert-date-format "%Y-%m-%d %a"
  "*Format for \\[insert-date] (c.f. 'format-time-string' for how to format).")

(defun insert-time ()
  "Insert the current time according to the variable \"insert-time-format\"."
  (interactive "*")
  (insert (format-time-string insert-time-format
          (current-time))))

(defun insert-date ()
  "Insert the current date according to the variable \"insert-date-format\"."
  (interactive "*")
  (insert "[")
  (insert (format-time-string insert-date-format
          (current-time)))
  (insert "]"))

(defun insert-time-and-date ()
  "Insert the current date according to the variable
  \"insert-date-format\", then a space, then the current time
  according to the variable \"insert-time-format\"."
  (interactive "*")
  (progn
    (insert "[")
    (insert (format-time-string insert-date-format
          (current-time)))
    (insert " ")
    (insert-time)
    (insert "]")))

(global-set-key [f3] 'insert-date)
(global-set-key [f4] 'insert-time)
(global-set-key [f5] 'insert-time-and-date)

;; configure tabs
(setq-default indent-tabs-mode nil)
(setq-default tab-width 4)
(setq cua-auto-tabify-rectangles nil)

;; emacs packages using package-install
(require 'package)
(add-to-list 'package-archives '("melpa" . "http://melpa.org/packages/") t)
(add-to-list 'package-archives '("marmalade" . "https://marmalade-repo.org/packages/"))
(package-initialize)

;; hide *buffers*
(when (require 'tabbar nil t)
  (setq tabbar-buffer-groups-function
        (lambda () (list "All Buffers")))
  (setq tabbar-buffer-list-function
        (lambda ()
          (remove-if
           (lambda(buffer)
             (find (aref (buffer-name buffer) 0) " *"))
           (buffer-list))))
  (tabbar-mode t))

;; tabbar color
(set-face-attribute
 'tabbar-default nil
 :background "gray20"
 :foreground "gray20"
 :box '(:line-width 1 :color "gray20" :style nil))
(set-face-attribute
 'tabbar-unselected nil
 :background "gray30"
 :foreground "white"
 :box '(:line-width 5 :color "gray30" :style nil))
(set-face-attribute
 'tabbar-selected nil
 :background "gray75"
 :foreground "black"
 :box '(:line-width 5 :color "gray75" :style nil))
(set-face-attribute
 'tabbar-highlight nil
 :background "white"
 :foreground "black"
 :underline nil
 :box '(:line-width 5 :color "white" :style nil))
(set-face-attribute
 'tabbar-button nil
 :box '(:line-width 1 :color "gray20" :style nil))
(set-face-attribute
 'tabbar-separator nil
 :background "gray20"
 :height 0.6)

;; Change padding of the tabs
;; we also need to set separator to avoid overlapping tabs by highlighted tabs

;; adding spaces
(defun tabbar-buffer-tab-label (tab)
  "Return a label for TAB.
That is, a string used to represent it on the tab bar."
  (let ((label  (if tabbar--buffer-show-groups
                    (format "[%s]  " (tabbar-tab-tabset tab))
                  (format "%s  " (tabbar-tab-value tab)))))
    ;; Unless the tab bar auto scrolls to keep the selected tab
    ;; visible, shorten the tab label to keep as many tabs as possible
    ;; in the visible area of the tab bar.
    (if tabbar-auto-scroll-flag
        label
      (tabbar-shorten
       label (max 1 (/ (window-width)
                       (length (tabbar-view
                                (tabbar-current-tabset)))))))))

;; keep tabs alphabetically sorted
(defun tabbar-add-tab (tabset object &optional append_ignored)
  "Add to TABSET a tab with value OBJECT if there isn't one there yet.
If the tab is added, it is added at the beginning of the tab list,
unless the optional argument APPEND is non-nil, in which case it is
added at the end."
  (let ((tabs (tabbar-tabs tabset)))
    (if (tabbar-get-tab object tabset)
        tabs
      (let ((tab (tabbar-make-tab object tabset)))
        (tabbar-set-template tabset nil)
        (set tabset (sort (cons tab tabs)
                          (lambda (a b) (string< (buffer-name (car a)) (buffer-name (car b))))))))))

(global-set-key [(ctrl tab)] 'tabbar-forward-tab)
(global-set-key [C-S-iso-lefttab] 'tabbar-backward-tab)

;; http://www.emacswiki.org/emacs/LineNumbers
(global-linum-mode 1)

;; customize org-mode
(add-hook 'org-mode-hook
          '(lambda ()
             (linum-mode 0)
             (define-key org-mode-map [(meta h)] nil)
             (define-key org-mode-map [(control tab)] nil)))


; http://www.emacswiki.org/emacs/InteractivelyDoThings
(require 'ido)
(ido-mode t)

;; http://www.emacswiki.org/emacs/uniquify
(require 'uniquify)

;; Turn off prompts for emacsclient that ask
;; buffer has a running process. kill it?
(setq kill-buffer-query-functions
      (remove 'process-kill-buffer-query-function
              kill-buffer-query-functions))

(delete-selection-mode t)

;; elpy
;; python code navigator
(require 'package)
(add-to-list 'package-archives
             '("elpy" . "https://jorgenschaefer.github.io/packages/"))

;; M-x package-refresh-contents to download a fresh copy of archive
(package-initialize)

;; for some reason enabling this turns off ability to browse source
;; (add-hook 'python-mode-hook (highlight-indentation-mode 0))

;; ledger mode
(autoload 'ledger-mode "ledger-mode" "A major mode for Ledger" t)
(add-to-list 'load-path
             (expand-file-name "/path/to/ledger/source/lisp/"))
(add-to-list 'auto-mode-alist '("\\.ledger$" . ledger-mode))

;; customize ledger-mode
(add-hook 'ledger-mode-hook
          '(lambda ()
             (define-key ledger-mode-map [(control tab)] nil)))

;; lisp
;; (setq inferior-lisp-program "sbcl")
;; (load (expand-file-name "~/stuff/lab/lisp/quicklisp/slime-helper.el"))


;; customize c mode
(setq-default c-default-style "linux")
(setq-default c-basic-offset 4)

;; treat _ as a word character
;; enable for all programming modes
(add-hook 'prog-mode-hook 'superword-mode)

;;; .emacs ends here
