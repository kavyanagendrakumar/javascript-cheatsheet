**Shell** - You need Bash or Zsh (or another shell) because they are the command-line interface (CLI) between you and your operating system. 
Bash - Bash (Bourne Again Shell) - Old
Zsh (Z shell) - New

Shells load different config files:

Bash → .bashrc, .bash_profile

Zsh → .zshrc. Your terminal behavior is configured via ~/.zshrc. Main config file for interactive use (where you add PATHs, aliases, plugins)

If nvm is only in the Bash file, it won’t work in Zsh.

Solution: copy NVM init lines into .zshrc

You can open **host file** with command cat /etc/hosts . cat command reads a file
If "localhost" url is not working in browser, you can check if it is available in host file. If the entry for localhost is not present, localhost won't work. Add below to host file and save.

127.0.0.1        localhost

255.255.255.255  broadcasthost

::1              localhost


**node terminal in vscode** - Node.js interactive shell, also called the Node REPL. You can also open a terminal in VS Code and type: node to open node terminal
Now, you can:

Write and execute JavaScript one line at a time like in browser console.

Test functions, variables, async code, etc.

Use Node built-ins like fs, path, process

| Feature      | Regular Terminal          | Node Terminal                |
| ------------ | ------------------------- | ---------------------------- |
| Shell type   | Bash / Zsh / PowerShell   | Node.js REPL                 |
| Language     | Shell commands            | JavaScript                   |
| Use case     | Running CLI commands, Git | Testing or exploring JS code |
| How to start | Just open terminal        | Type `node` in terminal      |
