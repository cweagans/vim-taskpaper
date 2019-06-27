# vim-taskpaper

## Introduction

From the TaskPaper website (<http://hogbaysoftware.com/projects/taskpaper>):

"TaskPaper is a simple to-do list application that helps you stay
organized. Unlike competing applications, TaskPaper is based on plain text
files which offer you paper-like simplicity and ease of use." 

TaskPaper is a to-do list application for Mac OS X based on the "Getting
Things Done" approach of David Allen (<http://www.davidco.com/>). It supports
the GTD notions of projects, tasks and contexts.

This package contains a syntax file and a file-type plugin for the simple
format used by the TaskPaper application. It is intended for Mac users who
want to edit their TaskPaper lists in Vim from time to time (for example, in
a SSH session, or on a non-Mac system) and for anyone who is looking for a
simple to-do list format.

## Installation

Assuming you're using [vim-plug](https://github.com/junegunn/vim-plug):

```
Plug 'cweagans/vim-taskpaper'
```

If you're using the [Vigor](https://github.com/vim-vigor) neovim distribution,
you can also install the [language-taskpaper](https://github.com/vim-vigor/language-taskpaper)
layer.

## Features

Vim can complete context names after the '@' using the keyword completion
commands (e.g. Ctrl-X Ctrl-N).

The plugin defines some new mappings:

    <Leader>td     Mark task as done
    <Leader>tx     Mark task as cancelled
    <Leader>tt     Mark task as today
    <Leader>tD     Archive @done items
    <Leader>tX     Show tasks marked as cancelled
    <Leader>tT     Show tasks marked as today
    <Leader>t/     Search for items including keyword
    <Leader>ts     Search for items including tag
    <Leader>tp     Fold all projects
    <Leader>t.     Fold all notes
    <Leader>tP     Focus on the current project
    <Leader>tj     Go to next project
    <Leader>tk     Go to previous project
    <Leader>tg     Go to specified project
    <Leader>tm     Move task to specified project

Marking a task as done will add the "@done" context tag to the end of the
task, and it will be greyed out by the syntax file.

To show all tasks with a particular context tag, type `\ts` and a tag name to
search.  If you use the `\ts` command over the desired context tag, the tag
name is set as default value.  This will fold all the irrelevant tasks leaving
only the tasks in the current context visible.

To fold all top-level projects leaving only the headings visible use the `\tp`
command. Standard fold commands can be used to open (`zo`) and close (`zc`)
individual projects.

To show all projects and tasks use the `zR` command. This disables folding so
that the entire file is expanded.

To go to next or previous project use the `\tj` command or `\tk` command.  To
go to a project you specify use the `\tg` command.  You can complete project
names with <Tab> on prompt.

## Options

The plugin supports a number of configuration variables, which can be set in
your .vimrc file.

To change the default date format string used when marking a task complete,
define the `task_paper_date_format` variable. The format matches your system's
`strftime()` function.

For example, to include the date and time in ISO8601 format:

    let g:task_paper_date_format = "%Y-%m-%dT%H:%M:%S%z"

To change the default archive project name, define the
`task_paper_archive_project` variable.  The default value is "Archive".

    let g:task_paper_archive_project = "Archive"

By default, when you move a task, the cursor will follow that task to its new
location.  To make the cursor stay in it's current location, change the
`task_paper_follow_move` variable.

    let g:task_paper_follow_move = 0

If you want to hide done tasks when searching you can change the
`task_paper_search_hide_done` variable.

    let g:task_paper_search_hide_done = 1

To set a custom style (colour, bold, etc.) for tags task_paper_styles variable,
which is a dictionary.

    let g:task_paper_styles={'wait': 'ctermfg=Blue guifg=Blue', 'FAIL':
'ctermbg=Red guibg=Red'}

See |highlight-args| for a full description of the syntax.

Customize
==========

You can create your own shortcut for tagging.  To define your own shortcut,
write settings in ~/.vim/ftplugin/taskpaper.vim or ~/.vimrc.  If you use the
.vimrc file, define settings like:

    function! s:taskpaper_setup()
    " Your settings
    nnoremap <buffer> <silent> <Leader>tn
    \    :<C-u>call taskpaper#toggle_tag('next', '')<CR>
    endfunction

    augroup vimrc-taskpaper
    autocmd!
    autocmd FileType taskpaper call s:taskpaper_setup()
    augroup END

To add a tag without argument:

    nnoremap <buffer> <silent> <Leader>tn
    \    :<C-u>call taskpaper#add_tag('next', '')<CR>

To delete a tag:

    nnoremap <buffer> <silent> <Leader>tN
    \    :<C-u>call taskpaper#delete_tag('next', '')<CR>

To toggle a tag:

    nnoremap <buffer> <silent> <Leader>tn
    \    :<C-u>call taskpaper#toggle_tag('next', '')<CR>

To add a tag with an argument:

    nnoremap <buffer> <silent> <Leader>tq
    \    :<C-u>call taskpaper#add_tag('priority')<CR>

You can specify the priority value on prompt.

To delete the priority tag with any argument:

    nnoremap <buffer> <silent> <Leader>tQ
    \    :<C-u>call taskpaper#delete_tag('priority', '')<CR>

To delete only the level 1 of priority tag:

    nnoremap <buffer> <silent> <Leader>tQ
    \    :<C-u>call taskpaper#delete_tag('priority', '1')<CR>

To toggle a tag with an argument:

    nnoremap <buffer> <silent> <Leader>tq
    \    :<C-u>call taskpaper#toggle_tag('priority')<CR>

To update a tag (not delete if the tag exists):

    nnoremap <buffer> <silent> <Leader>tq
    \    :<C-u>call taskpaper#update_tag('priority')<CR>

## Acknowledgements

* The [original plugin](https://github.com/davidoc/taskpaper.vim) was written by David O'Callaghan <david.ocallaghan@cs.tcd.ie>
* This fork has been improved by contributions from many forks of the original repository
