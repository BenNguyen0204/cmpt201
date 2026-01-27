# Cheat sheet

## Linux tutorial

### Basic command
- Terminal = window where you type commands
- Shell = program that runs your commands (bash is common)
- `pwd`: Print Working Directory: Tells you what your current working directory is.
- List files:
```bash
ls
ls -l     # long format
ls -a     # include hidden files
ls -la    # both
```
- Change directory:
```bash
cd folder
cd ..     # parent
cd ~      # home
cd -      # previous directory
cd /      # root
```
- Absolute vs Relative Paths
    - Absolute path starts with /. Example: /home/user/stuff
    - Relative path does NOT start with /. Example: stuff/
    - Special: . current directory, .. parent directory, ~ home directory
- Linux is Case Sensitive: File.txt ≠ file.txt
- `file filename` - shows file type
- `man`= manual pages
```bash
man ls
man cd
man chmod
man -k copy # if you don’t know exact command name
```

### File manipulation
- `mkdir`: Make Directory - ie. Create a directory.
- `rmdir`: Remove Directory - ie. Delete a directory.
- `touch`: Create a blank file.
- `cp`: copy a file
- `mv`: move a file or renaming it
- `rm`: delete a file and `rm -r myFolder/`: delete a folder

## Text editor
- `nvim file.text`
    - `i`: insert mode
    - `esc`: normal mode
    - `:w` save
    - `:q` quit
    - `:wq` save and quit
    - `:q!` quit no save
    - `h j k l`, `gg` (top), `G` (bottom), `0` (line start), `$` (line end)
    - `dd`: delete line
    - `yy`: copy line
    - `p`: paste
    - `u`: undo and `U`: undo all changes to the current line
    - `/word`: search, then `n`: next and `N`: previous
- `cat <file>`: view files
- `less <file>`: view larger files
- `echo hello` or `echo "I like ramen"`
- `name=Ben` then `echo $name`

### Wildcard
- Wildcards match filenames: `ls *.txt` -> return matching files with .txt
```bash
ls *        # everything in folder
ls *.c      # all files ending in .c
ls ab* b*   # starts with "ab" and "b"
rm *.o      # remove all .o files
cp *.c src/ # copy all .c files into src/
```
### Permissions
- `ls -l filename` or `ls -ld dirname`: output example: -rwxr-xr--
    - 1st char: `-` normal file and `d` is directory
    - Next 9 chars: user(owner) - group - others
    - r = read file contents, w = modify file, x = execute file (run it)
    - r = 4, w = 2, x = 1 
        - then 7 = rwx, 6 = rw-, 5 = r-x, 4 = r--, 0 = ---
        - `chmod 644 file`
    - u user, g group, o others, a all
 ```bash
chmod u+x script.sh     # add execute to user
chmod a+x script.sh     # add execute to everyone
chmod go-w file.txt     # remove write from group+others
chmod u=rw file.txt     # set exact perms for user
```

### Filter
- A filter = command that reads input (stdin), processes it, outputs result (stdout).
- `head [-number of lines to print] [path]`: by default print first 10 lines
- `tail [-number of lines to print] [path]`: by default print last 10 lines 
- `sort [-options] [path]`: by default it will sort alphabetically
- `nl [-options] [path]`: number lines
- `wc [-options] [path]`: word count as well as characters and lines: 12 36 195: l w c
- `cut [-options] [path]`:
    - `cut -f 1 -d ' ' mysampledata.txt` first col
    - `cut -f 1,2 -d ' ' mysampledata.txt` first 2 col
        - `-d ' '`: fields are seperate by a space
- `sed <expression> [path]`: Stream Editor, search and replace on our data.
    - `sed 's/oranges/bananas/g'`- s for substitude and replace oranges with bananas
- `uniq [options] [path]`: remove duplicate lines from the data.
    - `uniq mysampledata.txt`
- `tac [path]`: print last line first, the opposite of `cat [path]`

### Grep and Regular Expressions
- `egrep [command line options] <pattern> [path]`: search a given set of data and print every line which contains a given pattern
    - `egrep 'mellon' mysampledata.txt`
- Regular expression:
    - . = any 1 char
    - ? = matches 0 or 1 times only.
    - * = matches 0 or more times.
    - + = matches 1 or more times.
    - {n} = previous matches exactly n times.
    - {n,m} = matches at least n times and not more than m times.
    - [agd] = one of a/g/d
    - [^agd] = NOT a/g/d
    - [c-f] = range c–f
    - ( ) = group
    - | = OR
    - ^ = start of line
    - $ = end of line
- `egrep '[aeiou]{2,}' mysampledata.txt`: identify any line with two or more vowels in a row
- `egrep '2.+' mysampledata.txt`: any line with a 2 on it
- `egrep '2$' mysampledata.txt`: number 2 as the last character on the line.
- `egrep 'or|is|go' mysampledata.txt`:  each line which contains either 'is' or 'go' or 'or'.

### Piping and redirection
- `ls > myoutput`: save the output of ls into the file myoutput.
- `wc -l barry.txt > myoutput`: content of myoutput will be clear, then the new output will be saved to it
    - `echo "hi" > file.txt`: Write text into a file (overwrite)
- `ls >> myoutput`: append instead of clear
    - `echo "another line" >> file.txt`: Add text to a file (append)
- `wc -l < myoutput` prints `8` while `wc -l myoutput` prints `8 myoutput`
- `ls -l video.mpg blah.foo 2> errors.txt`: redirecting error messages whenm trying to access video.mpg and blah.foo to a file named errors.txt
- `ls | head -3` or `ls | head -3 | tail -1`: piping: Send the output from one program as input to another program.

### Process Management!
- `top`: what is currently happening on the system like task manager
- `ps aux`: processes running in your current terminal session
- `kill [signal] <PID>`
- `jobs`: display a list of current jobs running in the background
- Foreground job: Normal way you run commands. Terminal waits until it finishes
    - Ex `sleep 5` you don’t get the prompt back until 5 seconds pass
- Background job: Add **&** at the end. Terminal gives your prompt back immediately
    - Ex: `sleep 5 &`
- `fg <job number>` - Bring a background job back to foreground
- `ctrl + z` - Pause the current foreground process and move it into the background.

## Bash script
- A bash script = a file of terminal commands you can run once to automate repeated tasks.
```bash
#!/bin/bash
echo Hello, who am I talking to?
read varname
echo It\'s nice to meet you $varname
pwd
ls
```
- `chmod +x myscript.sh` to allow running
- `./myscript.sh` chmod needed or `bash myscript.sh` no chmod needed

- **Variables**: A temporary store for information (data)
    - Ex: `name=Ryan`, `age = 20`
    - Put **$** in front to read it: `echo "$name"`
    - Special variables:
        - $0 = script name
        - $1–$9 = arg #1 to #9
        - $# = number of args
        - $@ = all args (list)
        - $? = last command’s exit code
        - $$ = current script PID
        - $USER = your username
        - $HOSTNAME = machine name
        - $SECONDS = seconds since script started
        - $RANDOM = random number
        - $LINENO = current line number in script
    - `export var1` will allow var1 to be accessed by the child script, say `./script2.sh`

- **Input**: 
    - `read`
        - `-p` specify a prompt
        - `-s` make the input silent
```bash
#!/bin/bash
# Ask the user for login details
read -p 'Username: ' uservar
read -sp 'Password: ' passvar
echo
echo Thankyou $uservar we now have your login details
```
    - Reading from STDIN
        - STDIN - /dev/stdin
        - STDOUT - /dev/stdout
        - STDERR - /dev/stderr
```bash
#!/bin/bash
# A basic summary of my sales report
echo Here is a summary of the sales data:
echo ====================================
echo
cat /dev/stdin | cut -d' ' -f 2,3 | sort
```

- **Arithmetic!**
    - Operator: - `+, -, \*, /, ++, --, %`	addition, subtraction, multiply, divide, add 1, min 1, modulus
    - `let <arithmetic expression>`. Ex: `let a=5+4`
    - `expr item1 operator item2`. Ex: `expr 5 + 4`
    - `$(( expression ))`: Double Parentheses. Ex: `a=$(( 4 + 5 ))`
    - `${#variable}`: Length of a Variable

- **If Statements!**
```bash
#if_example.sh
#!/bin/bash
if [ $1 -gt 100 ]
    then
        echo Hey that\'s a large number.
        pwd
fi
date
```
- `./if_example.sh 15` will print date and  `./if_example.sh 150` will print `Hey that\'s a large number.`

![alt text](Test.png)

- If else
```bash
if [ <some test> ]
then
    <commands>
else
    <other commands>
fi
```

- If Elif Else
```bash
if [ <some test> ]
then
    <commands>
elif [ <some test> ]
then
    <different commands>
else
    <other commands>
fi
```
- Boolean operation: And - &&. Or - ||
```bash
or.sh
#!/bin/bash
# or example
if [ $USER == 'bob' ] || [ $USER == 'andy' ]
then
    ls -alh
else
    ls
fi
```
- Case:
```bash
case <variable> in
<pattern 1>)
    <commands>
    ;;
<pattern 2>)
    <other commands>
    ;;
esac
```
- **Loops!**
- While loops
```bash
while [ <some test> ]
do
    <commands>
done
```

- Until loops
```bash
until [ <some test> ]
do
    <commands>
done
```

- For loops
```bash
for var in <list>
do
    <commands>
done
```

- Ranges
```bash
for value in {10..0..2}
do
    echo $value
done
echo All done
```
