# Redirections

When working on command lines, it is useful to send output of a command to file or read input from a file or send output of one command to the next command.

## Output redirection

```
$echo "Hello"
Hello
```
will display the string Hello on the terminal.

```
$echo "Hello" > greetings.txt
```
Will redirect the output of the echo command to the file "greetings.txt".

```
$echo "Bye World!" >> greetings.txt
```
Will APPEND the output of the echo command to the file "greetings.txt"


## Input Redirection

```
$ sort < numbers.txt
```
Will read the contents from the file "numbers.txt" and sort them. By default, sort will sort the lines alphabetically.

`sort -n < numbers.txt` will sort the lines numerically.

## Error Redirection

```
$ cat commands.sh
cp src
cd /some/path/that/does/not/exist
ls
$ sh commands.sh 2> errors.log
```
This will execute the `cp src` command and spits out the error that the destination is not specified. Then it executes the `cd` command and spits out the error that the path does not exist. Then it executes the command `ls` and prints out the contents of the directory. When we don't want errors on our screen (stdout), then we might want to redirect the errors to a file. In this case, the file is errors.log. The operator "2>" will redirect errors.


## Pipe
With pipes, the output of one command is sent to the next command as an input.
```
$ cat some-big-file | more
```
This will provide contents of the file "some-big-file" as an input to the command "more". more is a pager utility. The more command breaks the output into individual screens and waits for you to press the space bar before continuing on to the next screen. Pressing the enter key will advance the output one line.

```
$ cat numbers.txt | sort | uniq
```
This will find out all the unique numbers from the file "numbers.txt". Note that, the file must contain numbers on separate lines.


# Miscellaneous commands and options

```
$echo -e "Hello\nCruel World!"
Hello
Cruel World!
```
Will process the escape sequence \n and convert that to a newline. 


`sh filename.sh` will process all the commands in the file filename.sh line by line.

`cp src target` will copy the contents from file src and pastes them into the file target (Creates file target if doesn't already exist and overwrites if already exists)


`mkdir test && cd test` Makes the directory test and enters into that directory. && is used to execute multiple commands one after the other.


`curl <Website URL>` This command will display the content of the URL on your terminal
`curl -o file <Website URL>` This command will save the content of the URL into `file`
`curl -I <Website URL>` This command will display the HTTP header of the website.

# Devil is in the details

For any program on UNIX-based systems, three files are automatically opened when the program starts execution. These files are stdin(Standard input), stdout (Standard Output) and stderr (Standard errors). stdin is usually the keyboard. Any program that interacts with users, expects that users will type something as an input. stdout and stderr are usually the screen/monitor. One can choose to redirect these to files. In UNIX based systems, everything is a file. Sockets are files. directories are files. You can see the type of file with `ls -l`. See the first letter of each line. If it is 'd', then it is a directory. If it is '-', then it is a regular file. 
```
$ls -l
drwxr-xr-x  2 unmeshjoshi  staff   68 Dec  4 15:37 test-dir
-rw-r--r--  1 unmeshjoshi  staff   12 Oct 16 12:57 test.txt
```

Also note that the extension of file doesn't matter in UNIX based systems. The content of the file decides the file format. E.g. In Windows OS, executable files are generally with .exe extension. In UNIX-based systems (Linux, MAC), it is not the case. People use extension of convenience. E.g. .out, .dmg and .sh
