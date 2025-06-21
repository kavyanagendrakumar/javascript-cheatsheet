**Shell** - You need Bash or Zsh (or another shell) because they are the command-line interface (CLI) between you and your operating system. 
Bash - Bash (Bourne Again Shell) - Old
Zsh (Z shell) - New

Shells load different config files:

Bash → .bashrc, .bash_profile

Zsh → .zshrc

If nvm is only in the Bash file, it won’t work in Zsh.

Solution: copy NVM init lines into .zshrc

You can open host file with command **cat /etc/hosts **. cat command reads a file
If "localhost" url is not working in browser, you can check if it is available in host file. If the entry for localhost is not present, localhost won't work. Add below to host file and save.
127.0.0.1        localhost
255.255.255.255  broadcasthost
::1              localhost
