### Quick Guide: Chain Commands with Linux Aliases

---
#### **Purpose**
Execute multiple shell commands using a single alias.

---
#### **Steps**

1. **Create Temporary Alias**
    - **Sequential Execution**:  
      `alias seq='echo "First" && echo "Second"'`  
      (Runs `Second` only if `First` succeeds)
    - **Unconditional Execution**:  
      `alias all='echo "First"; echo "Second"'`  
      (Runs `Second` regardless of `First`)

2. **Create Permanent Alias**
    - Open Shell Profile:  
      - Bash: `vim ~/.bashrc`  
      - Zsh: `vim ~/.zshrc`
    - Add Alias:  
      `alias perm='echo "First" && echo "Second"'`
    - Save and Exit

3. **Activate Changes**
    - Bash: `source ~/.bashrc`  
    - Zsh: `source ~/.zshrc`

---

#### **Examples**

- **Temporary Alias**:  
  ```bash
  alias seq='echo "First" && echo "Second"'
  ```
- **Permanent Alias**:  
  ```bash
  echo "alias perm='echo \"First\" && echo \"Second\"'" >> ~/.bashrc
  ```

---

#### **Test**

- Run `seq` or `perm` in the terminal.

---

#### **Remove Alias**

- **Temporary**: `unalias seq`
- **Permanent**: Remove line from shell profile and `source` it again.

---
