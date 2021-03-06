    This plugin adds four main commands in normal mode

cs: To change the surroundings.
ds: To delete the surroundings.
ys: To add surroundings.
S: To surround the currently selected text.
The following are some commands that I usually use. However, you can check the documentation for more:

cs”’: Change the surrounding from double quotes to single quotes.
ds”: Delete the closest double-quotes surroundings.
ysiw<b>: Surround the current word with <b> tag (iw means inner word.)

Plug 'terryma/vim-multiple-cursors'

This plugin adds three main commands in normal mode

<ALT-n>: Start multi cursor mode, select the current word, or select the next occurrence.
<ALT-x>: deselect the current occurrence and go to the next one.
<ALT-p>: deselect the current occurrence and go to the previous one.
C-c/Esc: to exit the mode

___

Usage
This plugin adds three main commands in normal mode

cx + motion: Select the first bloc to swap or select the second, and perform the swap.
cxx : Similar to cx but for the current line.
X: Similar to cx but for the select text.
cxc: Cancel pending exchange.

Plug 'tommcdo/vim-exchange'

___

Plug ‘michaeljsmith/vim-indent-object’

This plugin adds three text objects:

ii: Indent level.
ai: Indent level plus one line above
aI: Indent level plus one line above and below.

gcii: Comment all the instructions inside the same indent level.
cxii: Exchange an indent level.
dai: To delete an if statement and all its instructions.

Plug 'vim-scripts/argtextobj.vim'
___
Plug 'vim-scripts/ReplaceWithRegister'
__
Plug 'machakann/vim-highlightedyank'
let g:highlightedyank_highlight_duration = DURATION_IN_MILLISECONDS

___

nnoremap <c-t> :action ActivateTerminalToolWindow<CR>
nnoremap <leader>t :action Terminal.OpenInTerminal<CR>

set ideajoin
set idearefactormode=keep
vnoremap < <gv
vnoremap > >gv
nnoremap [[ :action MethodUp<CR>
nnoremap ]] :action MethodDown<CR>
nnoremap zc :action CollapseRegion<CR>
nnoremap zo :action ExpandRegion<CR>
nnoremap <leader>zc :action CollapseAllRegions<CR>
nnoremap <leader>zo :action ExpandAllRegions<CR>
nnoremap <leader>c :action CommentByLineComment<CR>
nnoremap <leader>r :action Refactorings.QuickListPopupAction<CR>
nnoremap <Leader>=  :action ReformatCode<CR>
nnoremap <leader>o :action OptimizeImports<CR>
nnoremap <c-r> :action RecentFiles<CR>
nnoremap <leader>l :action RecentLocations<CR>
nnoremap <leader>h  :action LocalHistory.ShowHistory<CR>
nnoremap ge :action GotoNextError<CR>
nnoremap gE :action GotoPreviousError<CR>

___

set incsearch
nnoremap <c-/> :action FindInPath<CR>
nnoremap <c-a> :action GotoAction<CR>
nnoremap <c-f> :action GotoFile<CR>
nnoremap <leader>u :action FindUsages<CR>
nnoremap <leader>s :action GotoRelated<CR>
nnoremap <leader>h :action CallHierarchy<CR>
nnoremap <leader>b :action ShowNavBar<CR>
nnoremap <c-s> :action FileStructurePopup<CR>
nnoremap <c-o> :action GotoSymbol<CR>
nnoremap gc :action GotoClass<CR>
nnoremap gi :action GotoImplementation<CR>
nnoremap gd :action GotToDeclaration<CR>
nnoremap gp :action GotToSuperMethod<CR>
nnoremap gt :action GotoTest<CR>
nnoremap gb :action Back<CR>
nnoremap gf :action Forward<CR>

___

nnoremap ,r :action ContextRun<CR>
nnoremap ,c :action RunClass<CR>
nnoremap ,f :action ChooseRunConfiguration<CR>
nnoremap ,t :action ActivateRunToolWindow<CR>
nnoremap ,u :action Rerun<CR>
nnoremap ,f :action RerunFailedTests<CR>

___


Unquote a word that's enclosed in single quotes  
`di'hPl2x`

- `di'` - Delete the word enclosed by single quotes.
- `hP` - Move the cursor left one place (on top of the opening quote) and put the just deleted text before the quote.
- `l` - Move the cursor right one place (on top of the opening quote).
- `2x` - Delete the two quotes.
