## About


This is the official PHP indentation plug-in for VIm (version 1.39 is bundled with VIm 7.4).

Please, visit [the homepage](https://www.2072productions.com/to/phpindent.txt) of the PHP indentation script to see all the details about its features and capabilities.

### Options

Just type `:help php-indent` inside VIm.

### Optional updated Syntax script

Feel free to use [my updated version](https://github.com/2072/vim-syntax-for-PHP) of the official VIm syntax
script for PHP which fixes a few issues and add support for some of the newest PHP
features (see the [change log](https://github.com/2072/vim-syntax-for-PHP/commits/master) for the details).

## Install


### Vundle
 1. Install and configure the [Vundle](https://github.com/gmarik/vundle) plug-in manager, [follow the instructions here](https://github.com/gmarik/vundle#quick-start)
 2. Add the following line to your `.vimrc`:

         Plugin '2072/PHP-Indenting-for-VIm'
 3. Source your `.vimrc` with `:so %` or otherwise reload your VIm
 4. Run the `:BundleInstall` command

### Pathogen
 1. Install the [pathogen.vim](https://github.com/tpope/vim-pathogen) plug-in, [follow the instructions here](https://github.com/tpope/vim-pathogen#installation)
 2. Clone the repository under your `~/.vim/bundle/` directory:

         cd ~/.vim/bundle
         git clone https://github.com/2072/PHP-Indenting-for-VIm.git

### Debugging
This script uses a lot of heuristics to do its job, when debugging you need to do 2 things:
- Comment out the `finish` here (search for 'XXX'):

```viml
" Only define the functions once per Vim session.
if exists("*GetPhpIndent")
    call ResetPhpOptions()
    finish " XXX -- comment this line for easy dev
endif
```

Doing this allows you to easily reload the indent script after a modification by just reloading your test `.php` file.

- Enable the step debug printing by executing the command: `:%s /" DEBUG \zec//g`.
This will cause the script to pause at key steps, look for the number printed and search it in the indent script.
You can add more debug call, the convention is to use the current line number as the hint + any other relevant useful information.
You can disable them again with `:%s /^\s*\zs\zecall DebugPrintReturn/" DEBUG /g`.

Then try to indent the line causing issues and follow what is happening to find out which part of the script is causing the issue.
You can disable the print function interruptions by hitting the `<Del>` key of your keyboard.

Note that the indent script switches to an "optimized mode" when you indent several lines in a row so there can be bugs that only happen in this optimized mode.
This mode is automatic on the 3rd consecutive line indentation, just indent a line above the line you last indented to switch back to the default mode.

If you make a modification, make sure to run the command `:setlocal debug=msg` to enable vim debug messages.

