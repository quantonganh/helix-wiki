# Vim

Helix's editing model is strongly inspired from vim and kakoune, and a notable difference from vim (and the most striking similarity to kakoune) is that Helix follows the `selection → action` model. This means that whatever you are going to act on (a word, a paragraph, a line, etc) is selected first and the action itself (delete, change, yank, etc) comes second. A cursor is simply a single width selection.

# Kakoune

Kakoune's strength is in being a first class citizen of the shell environment it runs in, and really defines very little about the editor with all the functionality helix provides being possible through shell integrations and external sidecar processes like kak-lsp and kak-tree. The downside of this approach is that you need to configure and maintain a number of plugins in varying languages in order to acheive all the functionality Helix includes. Helix prefers instead to include common functionality as part of the core editor.

Besides approach to core features, Helix's editing model, while derived from Kakoune, differs in some important ways:

* *Avoids use of held modifiers.* A consequence of this preference is that the pattern of using shift to extend selections with a given movement is replaced with the use of a new mode toggled with `v`. Kakoune's view mode is then moved to `z` to make room.
* *Avoids use of alt.* Alt is often in an awkward place on the keyboard, making for strenuous key combinations. Kakoune uses alt to mean the reversal of direction, but Helix restores the use of shift for this purpose, bringing it more in line with the vim lineage.
* Helix was created after Kakoune decided to change the meaning of the `x` key, so Helix's `x` still exhibits conditional behavior (extend to line bounds, or else add a line below to selection). A decision hasn't been made on if this will remain the case.