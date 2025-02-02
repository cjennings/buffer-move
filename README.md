note
====

This fork of buffer-move is different from [lukhas/buffer-move](https://github.com/lukhas/buffer-move) ONLY in that it incorporates a PR by taughtz found [here](https://github.com/lukhas/buffer-move/pull/19).

From the commit message:

Using cl- functions requires Emacs 24.3 and the cl-lib package. Not having this was causing an issue were cl-flet was apparently not working correctly, which was causing error messages like:

    buf-move-right: Symbol’s value as variable is void: settings


installation
============

If you're using the straight package manager:

    (straight-use-package
     '(el-patch :type git :host github :repo "lukhas/buffer-move"
                :fork (:host github
                       :repo "cjennings/buffer")))

If you're using straight with use-package integration:

    (use-package buffer-move
      :straight (buffer-move :type git :host github :repo "lukhas/buffer-move"
                             :fork (:host github :repo "cjennings/buffer-move")))


buffer-move
===========

This file is for lazy people wanting to swap buffers without
typing C-x b on each window. This is useful when you have :

    +--------------+-------------+
    |              |             |
    |    #emacs    |    #gnus    |
    |              |             |
    +--------------+-------------+
    |                            |
    |           .emacs           |
    |                            |
    +----------------------------+

and you want to have :

    +--------------+-------------+
    |              |             |
    |    #gnus     |   .emacs    |
    |              |             |
    +--------------+-------------+
    |                            |
    |           #emacs           |
    |                            |
    +----------------------------+

With buffer-move, just go in #gnus, do buf-move-left, go to #emacs
(which now should be on top right) and do buf-move-down.

To use it, simply put a (require 'buffer-move) in your ~/.emacs and
define some keybindings. For example, i use :

    (global-set-key (kbd "<C-S-up>")     'buf-move-up)
    (global-set-key (kbd "<C-S-down>")   'buf-move-down)
    (global-set-key (kbd "<C-S-left>")   'buf-move-left)
    (global-set-key (kbd "<C-S-right>")  'buf-move-right)

By default the point will switch along with the moving buffer,
if you want the point to stay (as vim switches) you can set
`buffer-move-stay-after-swap` to a non-nil value like so:

    (setq buffer-move-stay-after-swap t)

Alternatively, you may let the current window switch back to the previous
buffer, instead of swapping the buffers of both windows. Set the
following customization variable to 'move to activate this behavior:

    (setq buffer-move-behavior 'move)
