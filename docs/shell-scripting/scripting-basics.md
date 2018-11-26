# Scripting Basics

## Syntax

Shell scripts are a great way to automate many repetitive tasks. These shell scripts are nothing more than a file with a list of shell commands to execute from top to bottom. In fact, the only difference between a shell script file and a normal text file is that the very first line contains a special syntax, called the "shhbang" or "hashbang", that tells the shell which interpreter to use to run the commands. The "shhbang" is a line beginning with `#!` that lists the location of the interpreter to use.

To see the "shhbang" in a shell script, create a file named `example.sh` with the following contents.

```
#!/bin/bash
echo "This is a simple shell script"
```

Notice how the very first line contains the line `#!/bin/bash`. This tells the shell to use the `/bin/bash` program as the interpreter for all of the commands listed in the script. In this case, only the `echo` command is listed.

Once you have your first line all set up with the interpreter, the rest of the lines in your script can be any legal shell command you would type at the command prompt. Also, any lines that begin with `#` are comments and are ignored during runtime.

Once you have your `example.sh` file saved, you must give it execute permissions using `chmod +x example.sh`. This will allow a user to execute the file as a script.

To run your script, enter the absolute or relative path to your script on the command line and hit ++enter++. For example, enter `./example.sh` and hit ++enter++ to see what happens.

!!! example "Example: Showing shell scripts."

    A script named `example01.sh`

    ```
    $ cat example01.sh
    #!/bin/bash
    echo "The current date is:"
    date

    $ ./example01.sh
    The current date is:
    Sat Nov 24 23:14:08 EST 2018
    ```

## Variables and Arguments

Now that we understand the syntax for a shell script, let's dive into shell scripting variables and arguments. If you're coming from another programming or scripting language, it's good to know that the bash shell does not have a concept of variable types. That means there's no such thing as booleans, strings, integers, or floats for shell scripting variables. Every variable is stored as a string is the bash shell.

To create a variable, use the following syntax.

```
myvar="Hello"
```

To now use the contents of that variable, use the following syntax.

```
echo "${myvar}"
```

Variables are also create from the script arguments. Arguments are variables that are passed in on the command line. These arguments use special variable names that we'll cover in a moment. In order to run a script with arguments, you can use the following syntax.

```
./myscript.sh arg1 arg2 argN
```

!!! example "Example: Showing variables in shell scripts."

    Printing a variable.

    ```
    $ cat example02.sh
    #!/bin/bash
    myvar="hello"
    echo "The variable is: ${myvar}"

    $ ./example02.sh
    The variable is: hello
    ```


This will pass in the arguments to the script and store them in special variables. Here's a table of the special variables in shell scripts and a description of what they hold.

| Variables | Description                                   |
| --------- | --------------------------------------------- |
| `${0}`    | The name of the shell script.                 |
| `${1}`    | The value of the first argument.              |
| `${2}`    | The value of the second argument.             |
| `${N}`    | The value of the Nth argument.                |
| `${?}`    | The return code of the last executed command. |
| `${*}`    | A space-delimited string of all arguments.    |
| `${@}`    | A newline-delimited string of all arguments.  |
| `${#}`    | The number of arguments.                      |


!!! example "Example: Showing variables and arguments in shell scripts."

    Printing the arguments for a script.

    ```
    $ cat example03.sh
    #!/bin/bash
    echo "The first argument is ${1}"
    echo "The second argument is ${1}"

    $ ./example03.sh Hello World
    The first argument is Hello
    The second argument is World
    ```
    
    Showing special variables for a script.

    ```
    $ cat example04.sh
    #!/bin/bash
    date
    echo "The return code of the date command was ${?}"
    datetypo 
    echo "The return code of the datetypo command was ${?}"

    $ ./example04.sh
    Sat Nov 24 23:43:18 EST 2018
    The return code of the date command was 0
    ./test.sh: line 4: datetypo: command not found
    The return code of the datetypo command was 127
    ```
    
    Showing more special variables for a script.

    ```
    $ cat example05.sh
    #!/bin/bash
    echo "The number of arguments is ${#}"
    echo "The space-delimited string of arguments is ${*}"
    echo "The newline-delimited string of arguments is ${@}"

    $ ./example05.sh one two three
    The number of arguments is 3
    The space-delimited string of arguments is one two three
    The newline-delimited string of arguments is one two three
    ```

!!! info "For an explanation on the difference between `${*}` and `${@}` check out the [bash reference guide](https://www.gnu.org/software/bash/manual/bashref.html#Special-Parameters)."

## Conditionals and Loops

Conditionals and Loops help us control the execution flow of the script. It's common to conditionally execute something based on some other condition. It's also common to loop over items and perform an action on each item. Shell scripting allows us to do both of these concepts using `if`, `case`, and `for`.

### `if`

The `if` statement executes if a condition is true. All `if` statements in a shell script must be enclosed with `fi` (if spelled backwards).

You can use tests or comparision in `if` statements to determine what condition to test before either executing or skipping the `if` statement. Some common conditional expression are detailed in the [bash reference guide](https://www.gnu.org/software/bash/manual/bashref.html#Bash-Conditional-Expressions).

The syntax for an `if` statement is as follows.

```
if [ "${myvar}" == "hello" ]; then
  echo "${myvar} is equal to hello"
fi
```

!!! example "Example: Showing `if` usage."
    
    Testing if the first argument is equal to `hello`.

    ```
    $ cat example06.sh
    #!/bin/bash
    myvar="hello"
    if [ "${myvar}" == "hello" ]; then
      echo "${myvar} is equal to hello"
    fi

    $ ./example06.sh
    hello is equal to hello
    ```

    Testing if a file exists and is a directory.

    ```
    $ cat example07.sh
    #!/bin/bash
    if [ -d "/tmp" ]; then
      echo "The /tmp directory exists"
    fi

    $ ./example07.sh
    The /tmp directory exists
    ```

You can also combine the `if` statement with an optional `elif` or `else`. The `elif` condition allows you to sequentially test multiple if statements without writing an entire new block of code. The `else` condition allows you to execute code if the `if` or `elif` before it does not execute. An `if` statement will stop executing once it either hits a true condition or if it runs through the entire block without hitting a condition.

!!! example "Example: Showing `if`, `elif`, and `else` usage."
    
    Performing multiple tests.

    ```
    $ cat example08.sh
    #!/bin/bash
    if [ "${#}" -eq 0 ]; then
      echo "There are no arguments"
    elif [ "${#}" -eq 1 ]; then
      echo "There is one argument"
    else
      echo "There is more than one argument"
    fi

    $ ./example08.sh
    There are no arguments
    $ ./example08.sh one
    There is one argument
    $ ./example08.sh one two
    There is more than one argument
    ```

### `case`

The `case` statement is just a shorthand syntax for multiple `if` statements. The `case` statement must be closed with `esac` (case spelled backwards).

!!! example "Example: Showing `case` usage."
    
    ```
    $ cat example09.sh
    #!/bin/bash
    case ${#} in
      0)
        echo "There are no arguments"
        ;;
      1)
        echo "There is one argument"
        ;;
      *)
        echo "There is more than one argument"
        ;;
    esac

    $ ./example09.sh
    There are no arguments
    $ ./example09.sh one
    There is one argument
    $ ./example09.sh one two
    There is more than one argument
    ```

### `for`

The `for` statement is a way to loop over items in iterations. It's useful for looping over files or arguments.

!!! example "Example: Showing `for` usage."
    
    ```
    $ cat example10.sh
    #!/bin/bash
    for arg in ${@};
    do
      echo "The current arg is ${arg}"
    done

    $ ./example10.sh
    $ ./example10.sh one
    The current arg is one
    $ ./example10.sh one two
    The current arg is one
    The current arg is two
    ```

## Functions

Functions are a way to create repeatable and reusable code. Functions can run blocks of code over and over again. They also take arguments!


!!! example "Example: Showing function usage."
    
    ```
    $ cat example11.sh
    #!/bin/bash
    myfunction () {
      echo "This is a function"
      if [ ${#} -ne 0 ]; then
        echo "You passed these arguments to this function: ${*}"
      fi
      echo
    }
    myfunction
    myfunction myarg1

    $ ./example11.sh
    This is function
    
    This is function
    You passed these arguments to this function: myarg1
    ```

## Return Codes

When a command is executed in a shell it returns a code, often called the exit code or return code. This return code can range from `0-255` where `0` indicates a successful run of the command and anything non-zero (`1-255`) indicates a failure. This can be useful in shell scripts to conditionally execute some code if another command executed successfully.

If you want your script to return a return code upon exiting you can use the `exit` command. The `exit` command will stop execution of the shell script and exit, returning the specified exit code. The default return code is `0` unless one is specified. For example, `exit` returns the exit code of `0` while `exit 1` returns the exit code of `1`. Remember you can return any code from `0-255`.

!!! example "Example: Showing the usage of return codes."
    
    ```
    $ cat example12.sh
    #!/bin/bash
    date
    if [ "${?}" -eq 0 ]; then
      echo "The date command completed successfully"
      exit 0
    else
      exit 1
    fi

    $ ./example12.sh
    Sat Nov 24 23:43:18 EST 2018
    The date command completed successfully

    $ echo ${?}
    0
    ```
