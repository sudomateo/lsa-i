# Conventions

This page describes the conventions used throughout this course. These conventions are meant to aid in the understanding of core topics.

## Italicized font

_Italicized font_ indicates emphasis for a particular word or phrase.

## Bold font

**Bold font** indicates key terms that are described the first time they are introduced.

## Monospace font

`Monospace font` indicates filenames, system commands, and other literal inline text.

## Keyboard keys

++ctrl+c++ are keys that should be pressed on the keyboard to perform an action.

## Code blocks

Code blocks are meant to simulate what you would see in your terminal. They show the command prompt, a command, and the output of any commands.

### Commands

Commands that start with `$` are meant to be run as a non-privileged user.

```
$ echo "Hello World, I am not root."
Hello World, I am not root.
```

Commands that start with `#` are meant to be run as the root user.

```
# echo "Hello World, I am root."
Hello World, I am root.
```

### Files

Code blocks that contain a header are meant to be the literal contents of one or more files. The following is an example of two files named `/tmp/myscript.sh` and `/tmp/myfile` with their respective contents.

``` bash tab="/tmp/myscript.sh"
#!/bin/bash
echo "Hello World"
```

``` bash tab="/tmp/myfile"
Hello world.
This is a plain text file.
Linux rules!
```

## Examples

The following shows how an example is presented in the course. Examples usually contain a code block that showcases a specific use case.

!!! example "Example"
    ```
    $ echo "This is an example of the echo command"
    This is an example of the echo command
    ```

## Questions

Questions are used to provide practice without giving away the answer. These are used in exercises and practice problems.

!!! question "Question"

    How can you print the text `Hello World` to the terminal?

    ??? success "Answer"
        ```
        $ echo "Hello World"
        Hello World
        ```

## Tables

Tables are used to show matrixes of related data.

| Variable | Description |
| -------- | ----------- |
| `$SHELL` | Displays the location of the current user's shell |
| `$PATH`  | Displays the locations the shell searches to find commands |

## Admonitions

Admonitions are block-styled content that is used to provide asides to the main text. They often include supplemental information regarding the surrounding text.

!!! note "Note"
    This is an note block. Notes provide more information that extends the surrounding text and details any gotchas.

!!! info "Info"
    This is an info block. Info blocks provide information that is needed to expand upon the surrounding text.

!!! tip "Tip"
    This is an tip block. Tips provide suggestions on ways to use the surrounding text in a real-world scenario.

!!! warning "Warning"
    This is a warning block. Warnings detail limitaions and unusual syntax regarding the surrounding text.

!!! danger "Danger"
    This is a danger block. Dangers detail bugs and other risks that could possibly render your system unusable.
