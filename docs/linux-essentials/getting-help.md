# Getting Help

## The `help` Command

If you're ever unsure how to use a command, there are a few ways to get help. If you need help with internal shell commands, you can use the `help` command.

!!! example "Example: Using `help`."

    ```
    $ help
    GNU bash, version 4.2.46(2)-release (x86_64-redhat-linux-gnu)
    These shell commands are defined internally.  Type `help' to see this list.
    Type `help name' to find out more about the function `name'.
    Use `info bash' to find out more about the shell in general.
    Use `man -k' or `info' to find out more about commands not in this list.

    A star (*) next to a name means that the command is disabled.

    job_spec [&]                                        history [-c] [-d offset] [n] or history -anrw [f>
    (( expression ))                                    if COMMANDS; then COMMANDS; [ elif COMMANDS; the>
    . filename [arguments]                              jobs [-lnprs] [jobspec ...] or jobs -x command [>
    :                                                   kill [-s sigspec | -n signum | -sigspec] pid | j>
    [ arg... ]                                          let arg [arg ...]
    [[ expression ]]                                    local [option] name[=value] ...
    alias [-p] [name[=value] ... ]                      logout [n]
    bg [job_spec ...]                                   mapfile [-n count] [-O origin] [-s count] [-t] [>
    bind [-lpvsPVS] [-m keymap] [-f filename] [-q nam>  popd [-n] [+N | -N]
    break [n]                                           printf [-v var] format [arguments]
    builtin [shell-builtin [arg ...]]                   pushd [-n] [+N | -N | dir]
    caller [expr]                                       pwd [-LP]
    case WORD in [PATTERN [| PATTERN]...) COMMANDS ;;>  read [-ers] [-a array] [-d delim] [-i text] [-n >
    cd [-L|[-P [-e]]] [dir]                             readarray [-n count] [-O origin] [-s count] [-t]>
    command [-pVv] command [arg ...]                    readonly [-aAf] [name[=value] ...] or readonly ->
    compgen [-abcdefgjksuv] [-o option]  [-A action] >  return [n]
    complete [-abcdefgjksuv] [-pr] [-DE] [-o option] >  select NAME [in WORDS ... ;] do COMMANDS; done
    compopt [-o|+o option] [-DE] [name ...]             set [-abefhkmnptuvxBCHP] [-o option-name] [--] [>
    continue [n]                                        shift [n]
    coproc [NAME] command [redirections]                shopt [-pqsu] [-o] [optname ...]
    declare [-aAfFgilrtux] [-p] [name[=value] ...]      source filename [arguments]
    dirs [-clpv] [+N] [-N]                              suspend [-f]
    disown [-h] [-ar] [jobspec ...]                     test [expr]
    echo [-neE] [arg ...]                               time [-p] pipeline
    enable [-a] [-dnps] [-f filename] [name ...]        times
    eval [arg ...]                                      trap [-lp] [[arg] signal_spec ...]
    exec [-cl] [-a name] [command [arguments ...]] [r>  true
    exit [n]                                            type [-afptP] name [name ...]
    export [-fn] [name[=value] ...] or export -p        typeset [-aAfFgilrtux] [-p] name[=value] ...
    false                                               ulimit [-SHacdefilmnpqrstuvx] [limit]
    fc [-e ename] [-lnr] [first] [last] or fc -s [pat>  umask [-p] [-S] [mode]
    fg [job_spec]                                       unalias [-a] name [name ...]
    for NAME [in WORDS ... ] ; do COMMANDS; done        unset [-f] [-v] [name ...]
    for (( exp1; exp2; exp3 )); do COMMANDS; done       until COMMANDS; do COMMANDS; done
    function name { COMMANDS ; } or name () { COMMAND>  variables - Names and meanings of some shell var>
    getopts optstring name [arg]                        wait [id]
    hash [-lr] [-p pathname] [-dt] [name ...]           while COMMANDS; do COMMANDS; done
    help [-dms] [pattern ...]                           { COMMANDS ; }
    ```

## The `--help` Option

If you don't understand a command, the very first thing you should try is passing it the `--help` option. This usually prints command usage and common options of the command.

!!! example "Example: Using `--help`."

    ```
    $ cat --help
    Usage: cat [OPTION]... [FILE]...
    Concatenate FILE(s), or standard input, to standard output.

    -A, --show-all           equivalent to -vET
    -b, --number-nonblank    number nonempty output lines, overrides -n
    -e                       equivalent to -vE
    -E, --show-ends          display $ at end of each line
    -n, --number             number all output lines
    -s, --squeeze-blank      suppress repeated empty output lines
    -t                       equivalent to -vT
    -T, --show-tabs          display TAB characters as ^I
    -u                       (ignored)
    -v, --show-nonprinting   use ^ and M- notation, except for LFD and TAB
        --help     display this help and exit
        --version  output version information and exit

    With no FILE, or when FILE is -, read standard input.

    Examples:
    cat f - g  Output f's contents, then standard input, then g's contents.
    cat        Copy standard input to standard output.

    GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
    For complete documentation, run: info coreutils 'cat invocation'
    ```

## Manual Pages

If the `help` command and the `--help` option don't give you what you need, you can read the manual pages using the `man` command. The manual pages give an overview of the command and common usage. The `man` command actually uses the `less` pager to view the documentation.

!!! example "Example: Using `man`."

    ```
    $ man cat
    ```

