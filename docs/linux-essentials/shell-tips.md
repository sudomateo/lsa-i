# Shell Tips and Tricks

There are some tips and tricks that you can use to save time when navigating the shell.

## Command Completion

Whenever you are typing something at the command prompt you can often press ++tab++ to autocomplete commands and arguments. This only works if whatever you are typing is valid. This is especially useful when you want to autocomplete file paths.

## Command History

The `history` command shows the last 500 commands that you've entered. Using the `history -c` command will clear this history buffer. If you want to rerun the last command in your history you can use the `!!` command. To run any other command you can run `!N` where `N` is the number of the command from the `history` command output. The command history for a user is located inside a file named `.bash_history` within the user's home directory. Another way to move back and forth between the history is to use the ++up++ and ++down++ arrow keys.

## Moving the Cursor

You can use the ++left++ and ++right++ arrow keys to move the cursor on the command prompt. A shortcut to move to the start of your command is ++ctrl+a++. To move to the end of the command, use ++ctrl+e++. To execute a command and reset your cursor, press ++enter++. Finally, the ++backspace++ key deletes the character before the cursor.
