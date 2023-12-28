# VSCode

## Docs
[Dev Containers](https://code.visualstudio.com/docs/devcontainers/containers)  
[Dev Containers Features](https://containers.dev/features)  
[VSCode shortcuts on Mac](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)  


## Setup
This is local clean setup. Also supports already existing project, remote ssh host, remote tunnels and opening pull request  in an isolated container volume (Docs - Overview).

1. Open directory in VSCode (`/Volume/T7/rmtdev`)
2. Create configuration for remote dev by: 
- Run command `Dev Containers: Add Dev Container Configuration Files...`
- Select a DevContainers template like `Node & TypeScript` and version
- Select additional features like `Docker in Docker`
3. Reopen directory by command `Dev Containers: Reopen in Container` **


**: First run and changes to `devcontainer.json` will trigger build of devcontainers, takes a few minutes.

### Optional
If container has more then single project, fix VSCode's working directories by running cmd `Preferences: Open Remote Settings (JSON): ...`

```JSON
"eslint.workingDirectories": [
       { "pattern": "/workspaces/{node|bun}-<MM><YY>/*" }
]
```

Add more features by editing `devcontainer.json`.
```JSON
"features": {
    "ghcr.io/devcontainers/features/docker-in-docker:2": {}
}
```

## VSCode Extensions
These extensions are installed via VSCode Sync.

- [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)
- [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
- [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)
- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) + [DO: Prettier in VSCode](https://www.digitalocean.com/community/tutorials/how-to-format-code-with-prettier-in-visual-studio-code)