# Change to VSCode workspace directory inside terminal

I'm often wanting to get back to my workspace folder within the VSCode terminal.

After a bit of googling I couldn't find an answer so here is my current hack.

Edit VSCode Settings:

```json
  "terminal.integrated.env.linux": {
    "VSCODE_WORKSPACE": "${workspaceFolder}"
  },
  "terminal.integrated.env.osx": {
    "VSCODE_WORKSPACE": "${workspaceFolder}"
  }
```

Add alias to shell profile

```sh
alias cdw="cd ${VSCODE_WORKSPACE}"
```

Usage:

Just type `cdw` to change to the current workspace folder.

```sh
$ cdw
```