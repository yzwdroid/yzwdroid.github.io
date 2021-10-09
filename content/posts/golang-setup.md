 ---
title: Go development with VSCode and vim 
date: 2019-11-18
---

## Gofmt
Go takes a strong stance on code formatting. The gofmt tool rewrites code into the standard format.

```
gofmt filenames
```

## Golint

Linter is a tool that analyzes source code to flag programming errors, bugs, stylistic errors, and suspicious constructs.
Using Linter provides many benefits.
- Find bugs
- Speed up code review
- Manage code quality


```
go get -u golang.org/x/lint/golint
golint filenames
```

## VSCode setup

Install the Go extension maintained by Go Team at Google(previously maintained by Microsoft).

You should immediately see a prompt in the bottom-right corner of your screen titled Analysis Tools Missing. This extension relies on a suite of command-line tools, which must be installed separately. Accept the prompt, or use the Go: Install/Update Tools command.

Also, see the tutorial [https://code.visualstudio.com/docs/languages/go](https://code.visualstudio.com/docs/languages/go)

## vim setup

Install the vim-go plugin
`Plug 'fatih/vim-go', { 'do': ':GoUpdateBinaries' }`

The official toturial [https://github.com/fatih/vim-go/wiki](https://github.com/fatih/vim-go/wiki)

Here are some settings from my vimrc file
```bash
augroup go
  autocmd!

  autocmd FileType go nmap <silent> <Leader>v <Plug>(go-def-vertical)
  autocmd FileType go nmap <silent> <Leader>s <Plug>(go-def-split)
  autocmd FileType go nmap <silent> <Leader>d <Plug>(go-def-tab)

  autocmd FileType go nmap <silent> <Leader>x <Plug>(go-doc-vertical)

  autocmd FileType go nmap <silent> <Leader>i <Plug>(go-info)
  autocmd FileType go nmap <silent> <Leader>l <Plug>(go-metalinter)

  autocmd FileType go nmap <silent> <leader>b :<C-u>call <SID>build_go_files()<CR>
  autocmd FileType go nmap <silent> <leader>t  <Plug>(go-test)
  autocmd FileType go nmap <silent> <leader>r  <Plug>(go-run)
  autocmd FileType go nmap <silent> <leader>e  <Plug>(go-install)

  autocmd FileType go nmap <silent> <Leader>c <Plug>(go-coverage-toggle)


  autocmd Filetype go command! -bang A call go#alternate#Switch(<bang>0, 'edit')
  autocmd Filetype go command! -bang AV call go#alternate#Switch(<bang>0, 'vsplit')
  autocmd Filetype go command! -bang AS call go#alternate#Switch(<bang>0, 'split')
  autocmd Filetype go command! -bang AT call go#alternate#Switch(<bang>0, 'tabe')
augroup END
```

