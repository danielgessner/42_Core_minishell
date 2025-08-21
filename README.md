# 🐚 minishell - Crafting Your Own Unix Shell

<div align="center">

[![42 School](https://img.shields.io/badge/42-School-000000?style=for-the-badge&logo=42&logoColor=white)](https://42.fr/)
[![C](https://img.shields.io/badge/C-A8B9CC?style=for-the-badge&logo=c&logoColor=white)](https://en.wikipedia.org/wiki/C_(programming_language))
[![Readline](https://img.shields.io/badge/Readline-Library-4EAA25?style=for-the-badge)](https://tiswww.case.edu/php/chet/readline/rltop.html)
[![Norminette](https://img.shields.io/badge/Norminette-✅_Passing-success?style=for-the-badge)](https://github.com/42School/norminette)
[![Grade](https://img.shields.io/badge/Grade-125%2F100-brightgreen?style=for-the-badge)]()

*"The shell is not just a program - it's the conductor orchestrating the symphony of Unix"*

</div>

---

## 🎯 Project Overview

**minishell** is where 42 students dive deep into the heart of Unix systems programming, creating their own command-line interpreter from scratch. This project is the ultimate test of understanding how shells work under the hood - from parsing complex command lines to managing processes, signals, and the environment. It's not just about recreating bash; it's about mastering the fundamental concepts that power every Unix system.

> *"To understand Unix, you must first understand the shell. To understand the shell, you must build one yourself."*

## 🚀 The Shell Philosophy

At its core, a shell is a **command interpreter** - a bridge between human intent and machine execution. It transforms your typed commands into running processes, manages their lifecycle, and orchestrates their communication.

### 🔧 What Makes a Shell?

A shell is the **interface** between you and the operating system:

```bash
minishell$ echo "Hello World" | grep "World" > output.txt
```

This simple command involves:
- **Lexical analysis** - Breaking input into tokens
- **Syntax parsing** - Understanding command structure  
- **Variable expansion** - Processing environment variables
- **Process creation** - Forking and executing programs
- **I/O redirection** - Managing file descriptors
- **Pipeline management** - Connecting process streams

---

## 🏗️ Technical Architecture

### 🧠 Core Processing Pipeline

```
Input → Lexer → Parser → Expander → Executor → Output
  ↓       ↓        ↓         ↓         ↓        ↓
 "cmd"   Tokens   AST    Variables  Process   Result
```

### 🗂️ Project Structure

```
minishell/
├── 📁 includes/           # Header files
│   ├── shell.h           # Main shell definitions  
│   ├── parse.h           # Parsing structures
│   └── execute.h         # Execution engine
├── 📁 parsing/            # Input processing
│   ├── main.c            # Main entry point
│   ├── lexer.c           # Tokenization
│   ├── parser.c          # Syntax analysis
│   ├── expansion.c       # Variable expansion
│   ├── heredoc.c         # Here document handling
│   ├── signal.c          # Signal management
│   └── wildcard.c        # Pattern matching
├── 📁 execution/          # Command execution
│   ├── execute.c         # Main executor
│   ├── builtins.c        # Built-in commands
│   ├── pipex.c           # Pipeline management
│   ├── env.c             # Environment handling
│   └── redirects.c       # I/O redirection
└── 📁 libft/             # Custom C library
```

### 🎭 System Components

| Module | Purpose | Responsibility |
|--------|---------|----------------|
| **Lexical Analyzer** | Tokenization | Break input into meaningful tokens |
| **Parser** | Syntax Analysis | Build abstract syntax tree |
| **Expander** | Variable Processing | Handle `$VAR`, quotes, wildcards |
| **Executor** | Process Management | Fork, exec, wait, signal handling |
| **Built-ins** | Internal Commands | echo, cd, pwd, export, unset, env, exit |

---

## 🎪 Feature Showcase

### ⚡ Command Parsing & Execution
```bash
minishell$ ls -la | grep "minishell" | wc -l
1

minishell$ echo "Testing redirection" > test.txt && cat test.txt
Testing redirection

minishell$ export MY_VAR="Hello" && echo "$MY_VAR World"
Hello World
```

### 🔄 Pipeline Management
```bash
# Complex pipeline with multiple commands
minishell$ cat /etc/passwd | grep "root" | cut -d: -f1 | sort

# Pipeline with built-ins and external commands
minishell$ echo "apple\nbanana\napple" | sort | uniq -c
```

### 📂 I/O Redirection
```bash
# Input redirection
minishell$ wc -l < /etc/passwd

# Output redirection
minishell$ ls -la > directory_listing.txt

# Append redirection
minishell$ echo "New line" >> log.txt

# Here document
minishell$ cat << EOF
> This is a
> multi-line input
> EOF
```

### 🌟 Variable Expansion
```bash
# Environment variables
minishell$ echo "User: $USER, Home: $HOME"

# Custom variables
minishell$ export GREETING="Hello" TARGET="42"
minishell$ echo "$GREETING, $TARGET!"

# Exit status
minishell$ ls /nonexistent; echo "Exit code: $?"
```

### 🎯 Wildcard Expansion
```bash
# File pattern matching
minishell$ echo *.c
main.c lexer.c parser.c execute.c

# Directory traversal
minishell$ ls src/*.h
src/shell.h src/parse.h src/execute.h
```

---

## 🔧 Built-in Commands Arsenal

### 🎨 Command Reference

| Command | Description | Example Usage |
|---------|-------------|---------------|
| `echo` | Display text with optional `-n` flag | `echo "Hello World"` |
| `cd` | Change working directory | `cd /path/to/directory` |
| `pwd` | Print current working directory | `pwd` |
| `export` | Set environment variables | `export PATH=/bin:$PATH` |
| `unset` | Remove environment variables | `unset MY_VAR` |
| `env` | Display all environment variables | `env` |
| `exit` | Exit shell with optional status code | `exit 42` |

### ⚡ Built-in Examples

#### Echo Mastery
```bash
# Basic echo
minishell$ echo "Hello, World!"
Hello, World!

# Echo without newline
minishell$ echo -n "No newline"; echo " - continued"
No newline - continued

# Variable expansion in echo
minishell$ export NAME="minishell"
minishell$ echo "Welcome to $NAME!"
Welcome to minishell!
```

#### Directory Navigation
```bash
# Absolute path
minishell$ cd /usr/local/bin && pwd
/usr/local/bin

# Relative path  
minishell$ cd ../.. && pwd
/usr

# Home directory
minishell$ cd ~ && pwd
/Users/username
```

#### Environment Management
```bash
# Set multiple variables
minishell$ export DEBUG=1 VERBOSE=true LOG_LEVEL=info

# View specific variable
minishell$ echo "Debug mode: $DEBUG"

# Remove variable
minishell$ unset DEBUG && echo "Debug: $DEBUG"
Debug: 
```

---

## 🚀 Quick Start

### ⚡ Installation & Build

```bash
# Clone the shell mastery
git clone <repository-url>
cd minishell

# Build the project
make

# Launch your shell
./minishell
```

### 🎮 First Commands

```bash
# Welcome to your shell!
minishell$ echo "My first shell command!"
My first shell command!

# Test pipeline functionality
minishell$ echo "testing pipes" | cat | wc -w
2

# Environment variable magic
minishell$ export SHELL_NAME="minishell" && echo "Current shell: $SHELL_NAME"
Current shell: minishell

# File redirection test
minishell$ echo "Hello from minishell" > greeting.txt && cat greeting.txt
Hello from minishell
```

---

## 🧪 Comprehensive Testing

### 🎯 Basic Functionality Tests

```bash
# Test command execution
minishell$ ls
minishell$ pwd
minishell$ whoami

# Test built-ins
minishell$ echo "Testing echo"
minishell$ cd /tmp && pwd
minishell$ export TEST=123 && echo $TEST

# Test pipelines
minishell$ echo "apple\nbanana\napple" | sort | uniq
```

### 🔧 Advanced Feature Tests

```bash
# Complex pipelines
minishell$ cat /etc/passwd | grep "root" | cut -d: -f1

# Multiple redirections
minishell$ echo "line1" > test.txt && echo "line2" >> test.txt && cat test.txt

# Here documents
minishell$ cat << END
> First line
> Second line  
> END

# Variable expansion edge cases
minishell$ export VAR="test" && echo "$VAR" '$VAR' "literal $VAR"
```

### 🛡️ Error Handling Tests

```bash
# Command not found
minishell$ nonexistent_command
minishell: nonexistent_command: command not found

# Invalid syntax
minishell$ echo "unclosed quote
minishell$ | invalid pipe start

# Permission denied
minishell$ cat /etc/shadow
cat: /etc/shadow: Permission denied

# Signal handling (Ctrl+C)
minishell$ sleep 10
^C
minishell$ 
```

### 🧮 Memory & Performance Tests

```bash
# Memory leak testing with valgrind
valgrind --leak-check=full --show-leak-kinds=all ./minishell

# Stress testing with complex commands
minishell$ for i in {1..100}; do echo "test $i" | wc -w; done

# Large pipeline testing
minishell$ cat large_file.txt | sort | uniq | grep pattern | wc -l
```

---

## 🌟 Implementation Deep Dive

### 🧩 Lexical Analysis Engine

#### Token Classification
```c
typedef enum t_token_type {
    TOKEN_WORD,              // Command arguments
    TOKEN_PIPE,              // |
    TOKEN_REDIRECT_IN,       // <
    TOKEN_REDIRECT_OUT,      // >
    TOKEN_REDIRECT_APPEND,   // >>
    TOKEN_HEREDOC,           // <<
    TOKEN_EOF                // End of input
} t_token_type;
```

#### Tokenization Process
```c
// Core tokenization function
t_token *lexer_next_token(char **input) {
    skip_whitespace(input);
    
    if (**input == '|')
        return create_token(TOKEN_PIPE, "|");
    else if (**input == '<')
        return handle_redirect_in(input);
    else if (**input == '>')
        return handle_redirect_out(input);
    else
        return handle_word_token(input);
}
```

### 🎭 Parser Architecture

#### Command Node Structure
```c
typedef struct s_cmd_node {
    int                 cmd_type;    // Simple, pipe, background
    char                **cmd;       // Command and arguments
    t_file_list         *files;     // Redirections
    struct s_cmd_node   *next;      // Next command in pipeline
} t_cmd_node;
```

#### Syntax Tree Building
```c
// Parse command pipeline
t_cmd_list *parse_pipeline(t_token **tokens) {
    t_cmd_list *commands = init_cmd_list();
    
    while (*tokens && (*tokens)->type != TOKEN_EOF) {
        t_cmd_node *cmd = parse_simple_command(tokens);
        add_cmd_to_list(commands, cmd);
        
        if (*tokens && (*tokens)->type == TOKEN_PIPE) {
            advance_token(tokens);
            continue;
        }
        break;
    }
    
    return commands;
}
```

### 🔄 Execution Engine

#### Process Management
```c
// Execute pipeline of commands
int execute_pipeline(t_cmd_list *commands, char ***envp) {
    t_pipe_info pipes;
    int cmd_count = commands->size;
    
    // Create pipes for communication
    setup_pipes(&pipes, cmd_count);
    
    // Execute each command in the pipeline
    for (int i = 0; i < cmd_count; i++) {
        pid_t pid = fork();
        
        if (pid == 0) {
            // Child process
            setup_child_pipes(&pipes, i, cmd_count);
            execute_single_command(commands->head, envp);
        }
    }
    
    // Parent waits for all children
    wait_for_children(cmd_count);
    cleanup_pipes(&pipes);
}
```

#### Built-in Command Implementation
```c
// Built-in command dispatcher
int execute_builtin(char **args, char ***envp) {
    if (ft_strcmp(args[0], "echo") == 0)
        return builtin_echo(args);
    else if (ft_strcmp(args[0], "cd") == 0)
        return builtin_cd(args, envp);
    else if (ft_strcmp(args[0], "pwd") == 0)
        return builtin_pwd();
    else if (ft_strcmp(args[0], "export") == 0)
        return builtin_export(args, envp);
    else if (ft_strcmp(args[0], "unset") == 0)
        return builtin_unset(args, envp);
    else if (ft_strcmp(args[0], "env") == 0)
        return builtin_env(*envp);
    else if (ft_strcmp(args[0], "exit") == 0)
        return builtin_exit(args);
    
    return -1; // Not a built-in
}
```

---

## 🛡️ Signal Handling Mastery

### ⚡ Interactive Signal Management

```c
// Signal handler for interactive mode
void handle_interactive_signals(int sig) {
    if (sig == SIGINT) {
        // Ctrl+C pressed
        ft_putchar_fd('\n', STDOUT_FILENO);
        rl_on_new_line();
        rl_replace_line("", 0);
        rl_redisplay();
        g_exit_status = 130;
    }
}

// Setup signal handlers
void initialize_shell_signals(void) {
    signal(SIGINT, handle_interactive_signals);
    signal(SIGQUIT, SIG_IGN);  // Ignore Ctrl+\
}
```

### 🔧 Child Process Signals

```c
// Reset signals for child processes
void setup_child_signals(void) {
    signal(SIGINT, SIG_DFL);   // Default behavior
    signal(SIGQUIT, SIG_DFL);  // Default behavior
}
```

---

## 🌟 Advanced Features & Edge Cases

### 🎨 Quote Handling

```bash
# Single quotes preserve literal values
minishell$ echo 'The $USER variable is: $USER'
The $USER variable is: $USER

# Double quotes allow variable expansion
minishell$ echo "The $USER variable is: $USER"
The $USER variable is: dgessner

# Mixed quotes
minishell$ echo "User: '$USER' logged in"
User: 'dgessner' logged in
```

### 🌿 Variable Expansion Edge Cases

```bash
# Exit status variable
minishell$ ls /nonexistent; echo "Exit code: $?"
ls: /nonexistent: No such file or directory
Exit code: 2

# Empty variables
minishell$ echo "Empty: '$NONEXISTENT'"
Empty: ''

# Variable in different contexts
minishell$ export PATH="/bin" && echo $PATH"/ls"
/bin/ls
```

### 🔍 Wildcard Pattern Matching

```c
// Wildcard expansion implementation
char **expand_wildcards(const char *pattern, int *match_count) {
    DIR *dir = opendir(".");
    struct dirent *entry;
    char **matches = NULL;
    int count = 0;
    
    while ((entry = readdir(dir)) != NULL) {
        if (wildcard_match(pattern, entry->d_name)) {
            matches = resize_matches(matches, count, count + 1);
            matches[count] = ft_strdup(entry->d_name);
            count++;
        }
    }
    
    *match_count = count;
    closedir(dir);
    return matches;
}
```

---

## 📋 42 Standards Compliance

### ✅ Norminette Perfect

- **Function length**: Maximum 25 lines per function
- **File structure**: Maximum 5 functions per file
- **Naming conventions**: Consistent 42 style
- **Memory management**: Zero leaks, proper cleanup
- **Error handling**: Comprehensive error checking

### 🎯 Project Requirements

#### ✅ Mandatory Features
- **Prompt display** when waiting for new command
- **Command history** with working history functionality
- **Executable search** and launch (relative/absolute path or using PATH)
- **Built-in commands**: `echo`, `cd`, `pwd`, `export`, `unset`, `env`, `exit`
- **Quote handling**: Single and double quotes
- **Redirections**: `<`, `>`, `>>`
- **Pipes**: Command pipelines with `|`
- **Environment variables**: Expansion and manipulation
- **Exit status**: `$?` variable
- **Signal handling**: `Ctrl+C`, `Ctrl+D`, `Ctrl+\`

#### 🌟 Advanced Features
- **Here documents**: `<<` with delimiter
- **Wildcard expansion**: `*` pattern matching
- **Variable expansion**: Complex `$VAR` scenarios
- **Error messages**: Proper error reporting without `exit()`

---

## 🎓 Learning Outcomes

After conquering minishell, you master:

### 🧠 System Programming Concepts
- **Process management**: Fork, exec, wait system calls
- **Signal handling**: Proper signal management in interactive programs
- **File descriptors**: Low-level I/O and redirection
- **Environment manipulation**: Variable handling and inheritance

### 🔧 Advanced C Programming
- **Memory management**: Dynamic allocation and leak prevention
- **String manipulation**: Complex parsing and tokenization
- **Data structures**: Linked lists, abstract syntax trees
- **Error handling**: Robust error detection and recovery

### 🎭 Software Architecture
- **Modular design**: Clean separation of concerns
- **Parser implementation**: Lexical analysis and syntax parsing
- **State management**: Shell state and command history
- **Interface design**: User-friendly command-line interface

---

## 🌟 Real-World Applications

This shell mastery applies to:

- 🔧 **DevOps Engineering**: Build automation and deployment scripts
- 🐧 **System Administration**: Server management and monitoring
- 🔍 **Security Engineering**: Command-line security tools
- 📊 **Data Engineering**: ETL pipelines and data processing
- 🤖 **Automation**: Workflow orchestration and scripting
- 🌐 **Web Development**: Server setup and deployment automation

---

## 🎮 Interactive Examples

### 🔥 Power User Commands

```bash
# Complex data processing pipeline
minishell$ cat data.csv | cut -d, -f2 | sort -n | uniq -c | sort -rn | head -5

# System administration tasks
minishell$ ps aux | grep "python" | awk '{print $2}' | head -10

# Log analysis
minishell$ tail -f /var/log/system.log | grep "ERROR" | wc -l

# File management
minishell$ find . -name "*.c" | wc -l && ls *.h | sort
```

### 🧪 Testing Complex Scenarios

```bash
# Nested quotes and variables
minishell$ export MSG="Hello" && echo "Message: '$MSG from $USER'"

# Multiple redirections in pipeline
minishell$ cat < input.txt | grep "pattern" > output.txt && wc -l < output.txt

# Here document with variable expansion
minishell$ cat << EOF > config.txt
> User: $USER
> Home: $HOME
> Date: $(date)
> EOF
```

---

## 🎨 The Shell Aesthetic

```
▗▖  ▗▖▗▄▄▄▖▗▖  ▗▖▗▄▄▄▖ ▗▄▄▖▗▖ ▗▖▗▄▄▄▖▗▖   ▗▖       
▐▛▚▞▜▌  █  ▐▛▚▖▐▌  █  ▐▌   ▐▌ ▐▌▐▌   ▐▌   ▐▌       
▐▌  ▐▌  █  ▐▌ ▝▜▌  █   ▝▀▚▖▐▛▀▜▌▐▛▀▀▘▐▌   ▐▌       
▐▌  ▐▌▗▄█▄▖▐▌  ▐▌▗▄█▄▖▗▄▄▞▘▐▌ ▐▌▐▙▄▄▖▐▙▄▄▖▐▙▄▄▖     

42 Group Project by dabierma && dgessner
                    __   
         .,-;-;-,. /'_\        Instructions[▼]:
       _/_/_/_|_\_\) /           [run ./minishell]
     '-<_><_><_><_>=/\
       `/_/====/_/-'\_\
        ""     ""    ""
```

---

<div align="center">

**Made with ❤️ at 42 Heilbronn**

*Where system programming becomes second nature*

---

*"The shell is the soul of Unix - and now you've built one from scratch"*

</div>