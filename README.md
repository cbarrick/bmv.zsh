bmv.zsh
=========================

```
Perform batch file operations using a text editor.

Usage:

    bmv [options] <files>

Options:

    -c, --command <command>
        Execute the given command with the old and new filenames as
        arguments. The default command is 'mv -v'.

    -d, --dry-run
        Print the commands which would be executed and exit.

    -v, --version
        Print the version and exit.

    -h, --help
        Print this help message and exit.

Error codes:

    1   The number of file names returned by the editor does not match the
        number of files being renamed.

    2   The editor failed.

    3   The command failed to process a file.
```

**bmv** is a simple shell utility for batch renaming files. Given some filenames, bmv opens a text editor with each name. The user then edits each line to the new file name. When the user closes the editor, the files are renamed. This makes renaming files using regular expressions simple.

The text editor used is determined by the `$VISUAL` environment variable. If it is unset, `$EDITOR` is used. And if *that* is unset, `vi` is used.

For example, to rename all `.txt` files in all subdirectories using Sublime Text:
```
VISUAL='subl -w' bmv **/*.txt
```

You probably want to set your default editor in `.zshrc`.


Installation
-------------------------

1. Clone this repository
    ```
    git clone https://github.com/cbarrick/bmv.zsh.git
    ```

2. Put the script on your fpath
    ```
    ln -s bmv.zsh/bmv /usr/share/zsh/site-functions/bmv
    ```

3. Load the script
    ```
    autoload bmv
    ```

You probably want to load the script in `.zshrc` to make it avaliable to all interactive shells.


Tips
-------------------------

- Use the `-c` option to let bmv work with your version control system:
    ```
    bmv -c 'git mv' **/*.py
    ```

- Most editors have powerful regular expression systems. Learn to use them for the  best experience.

- Editor commands need to wait until the names have been edited before returning. Sublime Text, Atom, and other graphical editors **do not** wait by default. To make Atom and Sublime Text wait, use their `-w` option.


The ISC License
-------------------------

Copyright (c) 2014 Chris Barrick <cbarrick1@gmail.com>

Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted, provided that the above copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
