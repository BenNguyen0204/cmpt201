# Cheat sheet

## Linux tutorial
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
