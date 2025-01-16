# Linux Shell Implementation

This project is a custom implementation of a simple Linux shell, designed to support basic shell operations such as command execution, input/output redirection, pipes, and wildcard expansion. The shell can be run in both interactive and batch modes.

## Features

- **Interactive Mode**: Accepts commands from the user and executes them in real time.
- **Batch Mode**: Executes commands from a specified input file.
- **Command Execution**: Executes Linux commands using `execvp()`.
- **Piping**: Supports commands with pipes (e.g., `ls | grep file`).
- **Redirection**: Handles input (`<`) and output (`>`) redirection.
- **Wildcard Expansion**: Expands commands with wildcard characters (`*`).
- **Custom Built-in Commands**:
  - `cd`: Change directory.
  - `pwd`: Print current working directory.
  - `which`: Locate a command in system paths.
- **Conditional Execution**:
  - `then`: Executes only if the previous command succeeded.
  - `else`: Executes only if the previous command failed.

## Code Structure

### Files and Libraries

- **Header Files**:
  - `<fcntl.h>`: File control options.
  - `<glob.h>`: For wildcard expansion.
  - `<stdio.h>`, `<stdlib.h>`, `<string.h>`: Standard C libraries.
  - `<sys/stat.h>`, `<sys/types.h>`, `<sys/wait.h>`: System calls and process control.
  - `<unistd.h>`: POSIX API.

### Key Functions

- `interactive_mode()`: Runs the shell interactively.
- `batch_mode(const char *filename)`: Executes commands from a file.
- `parse_and_execute(char *command, int saved_stdin, int saved_stdout)`: Parses commands and decides how to execute them.
- `executeCommand(char *argv[])`: Executes single commands.
- `execute_pipe_command(char *args1[], char *args2[])`: Executes commands connected with a pipe.
- `expand_wildcards(char *arg, char **argv, int *argc)`: Expands wildcard characters in arguments.
- `execute_redirection(char *file, char *args[], int key, int stdin, int stdout)`: Handles input/output redirection.
- `pipe_and_redirect(char *args[], char *input_file, char *output_file, char *args_pipe[])`: Handles pipes combined with redirection.

### Main Program Flow

1. **Startup**: Detects whether to run in interactive or batch mode.
2. **Command Parsing**: Splits user input into tokens and identifies pipes, redirections, or wildcards.
3. **Command Execution**:
   - Executes regular commands or built-in commands (`cd`, `pwd`, etc.).
   - Handles pipes and redirections as necessary.
4. **Exit**: Shell exits when the `exit` command is issued.

## Usage

### Compilation

Compile the program using `gcc`:
```bash
gcc -o myShell myShell.c
```
### Running the Shell

#### Interactive Mode: Run the shell without arguments
```bash
./myShell
```
#### Batch Mode: Provide a file containing commands
```bash
./myShell <batch_file>
```
#### Example Commands

#### Execute a single command
```bash
ls -l
```
#### Execute a piped command
```bash
ls | grep file
```
#### Redirect input and output
```bash
sort < input.txt > output.txt
```
#### Change directory
```bash
cd /path/to/directory
```
#### Print current directory
```bash
pwd
```
#### Locate a command
```bash
which gcc
```
#### Exit the Shell
```bash
mysh> exit
```
