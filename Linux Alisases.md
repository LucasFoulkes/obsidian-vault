# Linux Aliases

## Purpose
Learn how to create and use aliases in Linux for efficient command execution.

---

## Temporary Aliases

### Purpose
Temporary aliases provide a quick way to execute commands without permanently altering system configurations.

### Steps

1. **Create Temporary Alias**
    - **Sequential Execution**:  
      ```bash
      alias seq='echo "First" && echo "Second"'
      ```
      (Runs `Second` only if `First` succeeds)
    - **Unconditional Execution**:  
      ```bash
      alias all='echo "First"; echo "Second"'
      ```
      (Runs `Second` regardless of `First`)

### Examples

- **Temporary Alias**: `seq`

### Test

- Run `seq` in the terminal.

### Remove Alias

- **Temporary**: `unalias seq`

---

## Permanent Aliases

### Purpose
Permanent aliases are saved across sessions, providing convenience and customization to your command-line interface.

### Steps

1. **Create Permanent Alias**
    - Edit Shell Profile:  
      - Bash: `vim ~/.bashrc`  
      - Zsh: `vim ~/.zshrc`
    - Add Alias:  
      ```bash
      echo "alias perm='echo \"First\" && echo \"Second\"'" >> ~/.bashrc
      ```
    - Save and Exit

2. **Activate Changes**
    - Bash: `source ~/.bashrc`  
    - Zsh: `source ~/.zshrc`

### Examples

- **Permanent Alias**: `perm`

### Test

- Execute `perm` in the terminal.

### Remove Alias

- **Permanent**: Remove the respective line from the shell profile and re-source it.

---

